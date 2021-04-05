---
title: John The Ripper
description: 
categories:
 - hacking
 - cheatsheet
tags:
 - password
 - tool
---

# 转换为 john 可识别的 hash
## Windows

```
john --format=nt --wordlist=[wordlist] [file]
```
## /etc/shadow
### unshadow

```
unshadow [passwd] [shadow]

Example Usage:
unshadow passwd shadow > unshadowed.txt
```

## Zip

```
unzip zipfile.zip
```

```
zip2john [options] [zip file] > [output file]

Example Usage:
zip2john zipfile.zip > hash.txt
```
## RAR

```
unrar e rarfile.rar
```

```
rar2john [rar file] > [output file]

Example Usage:
rar2john rarfile.rar > hash.txt
```
## SSH 私钥

```
ssh2john [id_rsa] > [output file]

Example Usage:
ssh2john id_rsa > hash.txt
```
# 暴力破解

解压 rockyou 字典

```
tar xvzf rockyou.txt.tar.gz
```

## 自动识别类型

```
john --wordlist=[wordlist] [file]

Example Usage:
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```
## 识别 Hash 类型

[online hash identifier](https://hashes.com/en/tools/hash_identifier)

## 指定 Format

```
john --list=formats
john --format=[format] --wordlist=[wordlist] [file]

Example Usage:
john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

## Single 模式

把相关信息放在 hash 前面
mike:xxxxxx
john 可以根据提供的信息自己生成字典用来破解

```
john --single --format=[format] [file]

Example Usage:
john --single --format=raw-sha256 hash.txt
```