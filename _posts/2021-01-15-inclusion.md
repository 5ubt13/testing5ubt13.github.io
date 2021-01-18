---
layout: post
title:  "TryHackMe - Inclusion (Easy)"
description: "A beginner level LFI challenge"
author: 0x5ubt13
date: 2021-01-15 16:10:00 +0000
categories: Write-Ups
tags: write-up OSCP Pentesting Ethical-Hacking LFI GTFObins Easy
---

# Welcome and link to the room

![room_logo](/assets/images/write-ups/tryhackme/inclusion/inclusion_logo.png)

Welcome to my first write-up, this time based on the room Inclusion. This is the first of a series of rooms I will be covering on my personal Road to OSCP journey.

You can find the room for free in the following link: [TryHackMe - Inclusion](https://tryhackme.com/room/inclusion)

<p>&nbsp;</p>

# Recon

Doing a quick scan with nmap, we find ports 22 and 80 are the only ones open:

![1](/assets/images/write-ups/tryhackme/inclusion/1.png)

Let's dive into that website and see if we can find a user and password to later on SSH into it:

![2](/assets/images/write-ups/tryhackme/inclusion/2.png)

When we connect to the website, we see a plan blog website. There are several articles in it, with no apparent signs of vulnerabilities in the first contact. However, if we look closer to the url after navigating to one of the articles, we can see a PHP parameter:

![3](/assets/images/write-ups/tryhackme/inclusion/3.png)

<p>&nbsp;</p>

# The Local File Inclusion

We can try and manipulate the URL. If we find directory traversal, we can navigate through the folders as if it was a CLI. We can try and open other files in the same directory or, more interestingly, navigate through different folders and see how far can we reach. 

In this instance, we can go back all the way to the root folder and cat the /etc/passwd file:

![PoC](/assets/images/write-ups/tryhackme/inclusion/lfiPoC.png)

If we look even closer, we can see a comment in the file that includes the password for a username. It's our lucky day!

![Password](/assets/images/write-ups/tryhackme/inclusion/password_found.png)

<p>&nbsp;</p>

# Find Password, Use Password!

We can now go ahead and try to connect via SSH.

```sh
ssh -l falconfeast -p 22 $ip
```
We are in.

<p>&nbsp;</p>

# Privilege Escalation

When we do `id` we can observe we landed in an unprivileged user, however we find we are included in the admin and sudo groups. We can enumerate whether we have sudo access to any file:

`sudo -l` 

And we can see we can call without password the binary `socat`.

![sudo_-l](/assets/images/write-ups/tryhackme/inclusion/pass_working_and_sudol.png)

A quick GTFObins research gives us the command to pop a root shell with the access we currently have:

![GTFObins](/assets/images/write-ups/tryhackme/inclusion/gtfobins.png)

```sh
sudo socat stdin exec:/bin/sh
```

<p>&nbsp;</p>

# Flags:

![flags](/assets/images/write-ups/tryhackme/inclusion/flags_and_privesc.png)

Thank you for reading!

<p>&nbsp;</p>

# References and further reading material:

OWASP Foundation - "Path Traversal" [Online] \
Available at: [https://owasp.org/www-community/attacks/Path_Traversal](https://owasp.org/www-community/attacks/Path_Traversal) \
Visited on: 15th January 2021 

Raj Chandel, 3rd July 2020. Hacking Articles - "Comprehensive Guide on Local File Inclusion (LFI)" [Online] \
Available at: [https://www.hackingarticles.in/comprehensive-guide-to-local-file-inclusion/](https://www.hackingarticles.in/comprehensive-guide-to-local-file-inclusion/) \
Visited on: 15th January 2021 

Anon., 2021. HackingLoops - "Local file inclusion tutorial" [Online] \
Available at: [https://www.hackingloops.com/local-file-inclusion-tutorial/](https://www.hackingloops.com/local-file-inclusion-tutorial/) \
Visited on: 15th January 2021 


<p>&nbsp;</p>

