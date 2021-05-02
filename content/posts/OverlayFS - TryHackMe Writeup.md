+++
categories = ["Hugo"]
date = "2021-05-03"
description = "OverlayFS - TryHackMe Writeup"

featuredalt = ""
featuredpath = "date"
linktitle = ""
title = "OverlayFS - TryHackMe Writeup"
slug = "OverlayFS - TryHackMe Writeup"
type = "post"
+++



![Bounty Hacker TryHackMe](static/image/OverlayFS.png)



##OverlayFS - CVE-2021-3493


Welcome to OverlayFS AKA CVE-2021-3493. I'm learning how to writeup so please pardon my mistakes.
Let's be honest this room dosen't need any writeup but don't know why I made it haha and Let's kick things of with some recources to know what is this CVE about.

https://ubuntu.com/security/CVE-2021-3493
https://ssd-disclosure.com/ssd-advisory-overlayfs-pe/
https://github.com/briskets/CVE-2021-3493


SSH creds :

```
Username: overlay

Password: tryhackme123
```


Get the `exploit.c` from github or here --> [https://ssd-disclosure.com/ssd-advisory-overlayfs-pe/]

Get the exploit file to SSH mechine and compile it.

Probably I would tell you how to compile a **.c** file but this is not a walkthrough :D :D

So, after compile give the file execute permission and the execute it with `./filename`

tada Run `whoami` in the terminal and magic now you are root


## How to get the root flag ?

```
Root flag is too close to root :)
```
