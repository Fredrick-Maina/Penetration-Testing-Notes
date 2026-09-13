nmap --privileged -sCV -p- -O -oA scan -T4 <MACHINE-IP>

open ports 
22
8000/tcp open  http    Werkzeug httpd 2.0.3 (Python 3.8.10)
|_http-title:  Login 

CVE-2024-49766
CVE-2024-34069

directory fuzzing
[23:01:50] 302 -  218B  - /logout  ->  http://10.49.146.52:8000/login
[23:04:21] 200 -  966B  - /register
