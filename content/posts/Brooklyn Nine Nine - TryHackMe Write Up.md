+++ 
categories = ["Hugo"] 
date = "2020-12-31" 
description = "Brooklyn Nine Nine - TryHackMe Writeup"

featuredalt = "" 
featuredpath = "date" 
linktitle = "" 
title = "Brooklyn Nine Nine - TryHackMe Writeup" 
slug = "Brooklyn Nine Nine - TryHackMe Writeup" 
type = "post" 
+++


![Brooklyn Nine Nine TryHackMe](https://miro.medium.com/max/2060/1*naUTNIfWRBuM49rvVkD9pg.png)



Welcome to my WriteUp. Ok So before starts question we need to enumerate the mechine. So Let's do it with **nmap**

## Enumurate The Mechine



```
# nmap -sC -sV -oN nmap/initial $ip                                                                                                                                1 ⚙
Starting Nmap 7.91 ( https://nmap.org ) at 2021-03-17 02:32 +06
Nmap scan report for 10.10.2.40
Host is up (0.42s latency).
Not shown: 997 closed ports
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_-rw-r--r--    1 0        0             119 May 17  2020 note_to_jake.txt
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.6.43.245
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 4
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 16:7f:2f:fe:0f:ba:98:77:7d:6d:3e:b6:25:72:c6:a3 (RSA)
|   256 2e:3b:61:59:4b:c4:29:b5:e8:58:39:6f:6f:e9:9b:ee (ECDSA)
|_  256 ab:16:2e:79:20:3c:9b:0a:01:9c:8c:44:26:01:58:04 (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 54.26 seconds
```

**We Get**
```
Port Open
21 FTP (Anonymous Login Allow)
22 SSH 
80 HTTP 
```



## Enumurate FTP


The server allow us to login anonymously so just login and get what is inside.
```
	Username : Anonymous
	Password : Anonymous
	
```
	
File name is **note_to_jake.txt**

```
From Amy,

Jake please change your password. It is too weak and 
holt will be mad if someone hacks into the nine nine

```


## Enumurate HTTTP / Port 80



After visiting the website there is just a picture and some text in the bottom, Nothing usefull here. If you go to the code of the website then you can see at the bottom there is a text **<!-- Have you ever heard of steganography? -->**



So, Let's download the picture and do some steganography on it 

```
	wget $ip/brooklyn99.jpg
	I used steghide for cracking stuff if it ask for any password then use stegcracker first then steghide.
	If you don't know how to use steghide use the command steghide --help and at the bottom you will have some exmple I hope it will help you.
```


After cracking we have a file called **note.txt**


	
```
		H***ts Pass***rd:
		flu***og12@ni***ine

Enjoy!!
```
It looks like a username with password. We already check FTP and HTTP It's time to do something with SSH/Port 22. Use credintials from **note.txt** and login on SSH.

## Get into The Mechine


After Login

```
h**t@brookly_nine_nine:~$ ls
nano.save user.txt
h**t@brookly_nine_nine:~$ cat user.txt
ee1****19052**0b*7aa****060c23e*

```

Now we have user.txt It's time to root the mechine 

I used the command **sudo -l** to see what do we need to be **sudo**


```
holt@brookly_nine_nine:~$ sudo -l
Matching Defaults entries for holt on brookly_nine_nine:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User holt may run the following commands on brookly_nine_nine:
    (ALL) NOPASSWD: /bin/nano
holt@brookly_nine_nine:~$ 
```

Here you can see **nano** can be sudo with no password. Now, you have to find how you can exploit a mechine VIA nano.

I always use **GTFObins** it's such a resourceful and helpful website for this type of exploit.

So, after you go to GTFObins search for nano then find sudo and do those things as it says.


After Being sudo


```
# cd /root && ls        
root.txt
# cat root.txt
-- Creator : Fsociety2006 --
Congratulations in rooting Brooklyn Nine Nine
Here is the flag: 63***0ea7bb9***0796b6*****4818*5

Enjoy!!
# 
```

## The End

If you having any problem on the mechine fell free to ping me on Twitter it's  @lifeofdekisugi

Thank You for reading my write up. Don't forget to tell me your experiance tag me on twitter @lifeofdekisugi.












