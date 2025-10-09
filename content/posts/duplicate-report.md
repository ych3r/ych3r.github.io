+++
title = 'First Duplicate Report'
date = 2025-03-20T00:09:38-04:00
draft = false
toc = false
categories = ['web security']
tags = ['information disclosure']
series = ['']
+++

So, I almost submit my first valid bug report...

![screenshot](/duplicate-report.png)

### What Happened

The other night, I finally decided to give bug bounty a try. I found a VDP program and let ChatGPT write me a recon script. That recon script returned with several subdomains, and when I went through them, a weird domain caught my eye. What the hell is 'whoami.xx.xx.com'?

Out of curiosity, I opened that in my browser. Holy cow, it looks like a debugging page with an internal IP! I wasn't sure if that counts but ChatGPT said it was a valid information disclosure bug. Before embarrassing myself, I wanted to figure out what this 'whoami' subdomain does.

It turns out the whoami subdomain is typically mapped to a developer debug service. It echoes back how the server sees the request -- including headers, IP addresses, and internal network info. From my experience, I know that internal IP can chain with other vulnerabilities which means at least it's a 'low severity'.

So, I submitted the report and got a 'duplicate' a few hours later. But that makes sense! I only ran a basic script -- and chances are, many others had already found the same thing before me. The good thing is, that means I found a valid bug!

### What Is an Information Disclosure Bug

As the name suggests, any sensitive data leak can be information disclosure bug. But this information must be sensitive enough that the company don't want it to be public.

### Where to Find Info Leaks

Can be anywhere as long as it's in scope.

- Exposed Subdomains: dev, staging, test, debug, internal
- Public Files / Directories: credential files
- JavaScript Files: API keys, usernames, maybe passwords
- Response Headers: vulnerable software version
- Error Pages: File path, SQL error, debug messages
- Publicly Accessible API Responses: sensitive information

### My Recon Workflow

This type of bug heavily rely on recon and you must be faster than anyone else. Thus, writing a script is the only option.

1. Subdomains: find as much as possible and monitor their changes.
```sh
subfinder -d target.com -silent -o subs.txt
httpx -l subs.txt -silent -status-code -title -web-server -tech-detect -o live.txt
```
2. Headers: look for info leak
```sh
httpx -l live.txt -status-code -web-server -tech-detect -title -o headers.txt
```
3. Interesting Files & Directories
```sh
ffuf -u https://FUZZ.target.com -w /usr/share/seclists/Discovery/Web-Content/common.txt -mc 200,403 -t 20 -o ffuf.json
```
4. JS Files
```sh
gau target.com | grep '\.js$' | sort -u > jsfiles.txt
python3 LinkFinder/linkfinder.py -i https://target.com/app.js -o cli
cat jsfiles.txt | xargs curl -s | grep -Ei "secret|token|api|auth"
```
5. Error Page: look for debug info, stack traces, SQL errors, Path disclosure

### Final Thoughts

Last but not least, an information disclosure bug is important but it's not like other security bugs. You don't even need a technical background to understand it, maybe you accidentally see leaked information when casually browsing their website. 

Hopefully, my blog inspires you to some extent. If you're new to bug bounty like me, don't waste your time on tutorial -- do recon on real target and learn by doing. Even duplicates mean you're doing it right. Anyway, I have to go refine my recon tool, see you ;)