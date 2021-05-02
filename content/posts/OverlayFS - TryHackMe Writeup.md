+++
categories = ["Hugo"]
date = "2020-12-31"
description = "OverlayFS - TryHackMe Writeup"

featuredalt = ""
featuredpath = "date"
linktitle = ""
title = "OverlayFS - TryHackMe Writeup"
slug = "OverlayFS - TryHackMe Writeup"
type = "post"
+++

![OverlayFS TryHackMe](https://images.unsplash.com/photo-1569235186275-626cb53b83ce?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=752&q=80)






## OverlayFS - CVE-2021-3493


Welcome to OverlayFS AKA CVE-2021-3493. I'm learning how to writeup so please pardon my mistakes.
Let's be honest this room dosen't need any writeup but don't know why I made it haha and Let's kick things of with some recources to know what is this CVE about.

https://ubuntu.com/security/CVE-2021-3493

https://ssd-disclosure.com/ssd-advisory-overlayfs-pe/

https://github.com/briskets/CVE-2021-3493


Ok so after knowing what all this about now we can dirty our hands on it.


SSH creds :

```
Username: overlay

Password: tryhackme123
```


Get the `exploit.c` from [github](https://raw.githubusercontent.com/briskets/CVE-2021-3493/main/exploit.c) or [here](https://ssd-disclosure.com/ssd-advisory-overlayfs-pe/)

Get the exploit file to SSH mechine and compile it.

Probably I would tell you how to compile a **.c** file but this is not a walkthrough :D :D

So, after compile give the file execute permission and the execute it with `./filename`

tada Run `whoami` in the terminal and magic now you are root


## How to get the root flag ?

```
Root flag is too close to root :)
```

After completing this room don't forget to thanks **[NinjaJc01](https://twitter.com/NinjaJc01)** creator of this room.

#happyhacking #tryhackme
