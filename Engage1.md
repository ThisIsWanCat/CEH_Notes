# Host Discovery

When trying to figure out the number of live hosts on a subnet, the following command will work<br/>

sudo nmap -T5 -sV <ip>/24<br/>

Note any ips that only show something like this:<br/>
53/tcp open  domain  Unbound<br/>
80/tcp open  http    nginx<br/>

This is likely not a host, but just a web application

# DNS Zone transfer

sudo dig axfr www.certifiedhacker.com zonetransfer.me<br/>
(replace www.certifiedhacker.com with whatever hostname)<br/>

If 'Transfer failed' log shows up, DNS zone transfer is not possible

# Finding Domain Controller, FQDN, NetBios, DNS Computer Name

sudo nmap -p 389 <target><br/>
Whichever has STATE=open is the Domain Controller

After:
sudo nmap -T5 -A <ip> > nmap.txt<br/>
Can use 'cat nmap.txt | grep <keyword>' to find things

# Scanning for Services
nmap -T5 -sV -p <port> <ip>/24

FTP = 21<br/>
SSH = 22<br/>
SMTP = 25<br/>
DNS = 53<br/>
SMB = 139/445<br/>
LDAP = 389<br/>
NFS = 2049<br/>
SQL = 3306<br/>

# LDAP Enumerating
Refer to: https://vk9-sec.com/enumerating-ad-users-with-ldap/

To find which is running ldap<br/>
sudo nmap -T5 -sU -p 389 <ip>/24

Enumerating Version
ldapsearch -x -h <target-ip> -b “dc=<domainController>,dc=com" | grep LDAP

Enumerating users
ldapsearch -x -h <target-ip> -b “dc=<domainController>,dc=com" "objectclass=user” | grep distinguishedName | grep "CN=users"

# Enumerating DNS
dig ns www.certifiedhacker.com (ns=name servers)
