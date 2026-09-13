add <ip-address> to hosts file

nmap -sCV -p- -O 10.129.84.62 -T4

PORT      STATE SERVICE       VERSION

53/tcp    open  domain        Simple DNS Plus
dig NS danglingtree.htb @<ip-address> +short
result < dc.danglingtree.htb

zone transfer: dig axfr danglingtree.htb @10.129.84.62 --> failed

80/tcp    open  http          Microsoft IIS httpd 10.0
|_http-title: IIS Windows Server
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0

88/tcp    open  kerberos-sec  Microsoft Windows Kerberos (server time: 2026-08-29 15:35:35Z)

nmap -p 88 --script krb5-enum-users --script-args krb5-enum-users.realm='danglingtree.htb' <ip-address>
result < administrator@danglingtree.htb
kinit username@DANGLINGTREE.HTB --> needs credentials

135/tcp   open  msrpc         Microsoft Windows RPC

139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
<nothing but 445 has things

389/tcp   open  ldap          Microsoft Windows Active Directory LDAP (Domain: danglingtree.htb, Site: Default-First-Site-Name)
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: 
| Subject Alternative Name: DNS:dc.danglingtree.htb, DNS:danglingtree.htb, DNS:DANGLINGTREE
| Not valid before: 2026-08-03T16:32:53
|_Not valid after:  2106-08-03T16:32:53

443/tcp   open  ssl/https?
| ssl-cert: Subject: commonName=danglingtree-DC-CA
| Not valid before: 2026-03-26T05:34:19
|_Not valid after:  2114-03-26T05:44:18
| tls-alpn: 
|   h2
|_  http/1.1
|_ssl-date: TLS randomness does not represent time

445/tcp   open  microsoft-ds?
netexec smb 10.129.84.143 -u 'anderson.w' -p 'R3dT3am@Acc3ss#01' -d danglingtree.htb

464/tcp   open  kpasswd5?

593/tcp   open  ncacn_http    Microsoft Windows RPC over HTTP 1.0

636/tcp   open  ssl/ldap      Microsoft Windows Active Directory LDAP (Domain: danglingtree.htb, Site: Default-First-Site-Name)
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: 
| Subject Alternative Name: DNS:dc.danglingtree.htb, DNS:danglingtree.htb, DNS:DANGLINGTREE
| Not valid before: 2026-08-03T16:32:53
|_Not valid after:  2106-08-03T16:32:53

3268/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: danglingtree.htb, Site: Default-First-Site-Name)
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: 
| Subject Alternative Name: DNS:dc.danglingtree.htb, DNS:danglingtree.htb, DNS:DANGLINGTREE
| Not valid before: 2026-08-03T16:32:53
|_Not valid after:  2106-08-03T16:32:53

3269/tcp  open  ssl/ldap      Microsoft Windows Active Directory LDAP (Domain: danglingtree.htb, Site: Default-First-Site-Name)
| ssl-cert: Subject: 
| Subject Alternative Name: DNS:dc.danglingtree.htb, DNS:danglingtree.htb, DNS:DANGLINGTREE
| Not valid before: 2026-08-03T16:32:53
|_Not valid after:  2106-08-03T16:32:53
|_ssl-date: TLS randomness does not represent time

3389/tcp  open  ms-wbt-server
| ssl-cert: Subject: commonName=dc.danglingtree.htb
| Not valid before: 2026-08-28T15:27:49
|_Not valid after:  2027-02-27T15:27:49
|_ssl-date: TLS randomness does not represent time
| rdp-ntlm-info: 
|   Target_Name: DANGLINGTREE
|   NetBIOS_Domain_Name: DANGLINGTREE
|   NetBIOS_Computer_Name: DC
|   DNS_Domain_Name: danglingtree.htb
|   DNS_Computer_Name: dc.danglingtree.htb
|   DNS_Tree_Name: danglingtree.htb
|   Product_Version: 10.0.26100
|_  System_Time: 2026-08-29T15:37:40+00:00

6600/tcp  open  ssl/mshvlm?
| ssl-cert: Subject: commonName=dc.danglingtree.htb
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1:<unsupported>, DNS:dc.danglingtree.htb
| Not valid before: 2026-03-26T05:41:20
|_Not valid after:  2027-03-26T05:41:20
|_ssl-date: TLS randomness does not represent time
| tls-alpn: 
|   h2
|_  http/1.1
| fingerprint-strings: 
|   GetRequest: 
|     HTTP/1.1 403 Forbidden
|     Connection: close
|     Date: Sat, 29 Aug 2026 15:35:55 GMT
|     Cache-Control: no-store
|     Cache-Control: max-age=0
|     Pragma: no-cache
|     Set-Cookie: .AspNetCore.Antiforgery.7Eyhia2WOxE=CfDJ8HsozULo80ZBsxvkNAKguokmkg17R_fVYzNjSpYa7sERd30jVYonB1XdSW5noRS_bc0G-dpns4t8nyfX0Z1io085g_u04_Uq5oNrTAkSroiH1x_dylH45_hYvf6H-jKcJr9_XZh6d0HJUN6sG7TNdO0; path=/; secure; samesite=none; Partitioned
|     Set-Cookie: WAC-SESSION=ebeb68a860564d17aefa56a2c0ac8c50; expires=Sun, 30 Aug 2026 15:35:56 GMT; path=/; secure; samesite=lax; httponly
|     Set-Cookie: WAC-TOKEN=; expires=Thu, 01 Jan 1970 00:00:00 GMT; path=/
|     Set-Cookie: WAC-AAD=; expires=Thu, 01 Jan 1970 00:00:00 GMT; path=/
|     Set-Cookie: XSRF-TOKEN=; expires=Thu, 01 Jan 1970 00:00:00 GMT; path=/
|     Strict-Transport-Security: max-age=5184000; includeSubDomains; preload
|     <!DOCTYPE html>
|     <html lang="en" xmlns="http://www.w3.org/1999/xhtml">
|     <head
|   HTTPOptions: 
|     HTTP/1.1 403 Forbidden
|     Connection: close
|     Date: Sat, 29 Aug 2026 15:35:56 GMT
|     Cache-Control: no-store
|     Cache-Control: max-age=0
|     Pragma: no-cache
|     Set-Cookie: .AspNetCore.Antiforgery.7Eyhia2WOxE=CfDJ8HsozULo80ZBsxvkNAKguom_TzojkgA--2gkWHsFvOzYSBz0xvZf3BCHpledOfvsHxRZ1KHpP4MGpd3qSGxETGNXrzGrSpXlcKI_z1R0Uy9zcMcLs2Igfsd2X5cyVnzrnE7Ob4mWZ3MYSqybte4_pGs; path=/; secure; samesite=none; Partitioned
|     Set-Cookie: WAC-SESSION=7b088adc3152432ca481a242c7ea2040; expires=Sun, 30 Aug 2026 15:35:57 GMT; path=/; secure; samesite=lax; httponly
|     Set-Cookie: WAC-TOKEN=; expires=Thu, 01 Jan 1970 00:00:00 GMT; path=/
|     Set-Cookie: WAC-AAD=; expires=Thu, 01 Jan 1970 00:00:00 GMT; path=/
|     Set-Cookie: XSRF-TOKEN=; expires=Thu, 01 Jan 1970 00:00:00 GMT; path=/
|     Strict-Transport-Security: max-age=5184000; includeSubDomains; preload
|     <!DOCTYPE html>
|     <html lang="en" xmlns="http://www.w3.org/1999/xhtml">
|_    <head

49664/tcp open  msrpc         Microsoft Windows RPC
49675/tcp open  msrpc         Microsoft Windows RPC
49678/tcp open  msrpc         Microsoft Windows RPC
49681/tcp open  msrpc         Microsoft Windows RPC
49690/tcp open  msrpc         Microsoft Windows RPC
49706/tcp open  msrpc         Microsoft Windows RPC
49719/tcp open  msrpc         Microsoft Windows RPC
49769/tcp open  msrpc         Microsoft Windows RPC
