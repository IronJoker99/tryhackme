# TRY HACK ME CTF CHALLANGE (Lazy admin)

	it's linux base system that give a practice os a skills/. let's make nmap scan or vurnability scan.

```bash
nmap -sC -sV 10.10.111.162
```
we got 
```
Starting Nmap 7.80 ( https://nmap.org ) at 2024-03-13 17:17 IST
Nmap scan report for 10.10.111.162
Host is up (0.49s latency).
Not shown: 998 closed ports
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

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 17.76 seconds

```
we know there is a webserver for that, lets find the directories. we are using dirb tool.

```bash
dirb 10.10.111.162
```  
we got
==> DIRECTORY: http://10.10.111.162/content/as/
==> DIRECTORY: http://10.10.111.162/content/attachment/
==> DIRECTORY: http://10.10.111.162/content/images/
==> DIRECTORY: http://10.10.111.162/content/inc/

in /as directory there is login page
in /inc page there is bunch of files, specifically sql back up file is find the credential.
```
manager
42f749ade7f9e195bf475f37a44cafcb: Password123	
```
after that there is web page that we can reverse shell the web.
we use the php-reverse-shell.php5
