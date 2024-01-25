# Host Discovery

When trying to figure out the number of live hosts on a subnet, the following command will work

sudo nmap -T5 -sV <ip>/24

Note any ips that only show something like this:
53/tcp open  domain  Unbound
80/tcp open  http    nginx

This is likely not a host, but just a web application

# DNS Zone transfer

sudo dig axfr www.certifiedhacker.com zonetransfer.me
(replace www.certifiedhacker.com with whatever hostname)

If 'Transfer failed' log shows up, DNS zone transfer is not possible

# Finding Domain Controller, FQDN, NetBios, DNS Computer Name

sudo nmap -p 389 <target>
Whichever has STATE=open is the Domain Controller

After:
sudo nmap -T5 -A <ip> > nmap.txt
Can use 'cat nmap.txt | grep <keyword>' to find things

# Scanning for Services
nmap -T5 -sV -p <port> <ip>/24

FTP = 21
SSH = 22
SMTP = 25
DNS = 53
SMB = 139/445
LDAP = 389
NFS = 2049
SQL = 3306

# LDAP Enumerating
Refer to: https://vk9-sec.com/enumerating-ad-users-with-ldap/

To find which is running ldap
sudo nmap -T5 -sU -p 389 <ip>/24

Enumerating Version
ldapsearch -x -h <target-ip> -b “dc=<domainController>,dc=com" | grep LDAP

Enumerating users
ldapsearch -x -h <target-ip> -b “dc=<domainController>,dc=com" "objectclass=user” | grep distinguishedName | grep "CN=users"

# Enumerating DNS
dig ns www.certifiedhacker.com (ns=name servers)

# Vulnerability Scans
1. nmap -Pn --script vuln <ip>
2. search up CVE numbers to learn more

