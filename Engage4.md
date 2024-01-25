# Finding and Accessing Mobile Devices
1. sudo nmap -p 192.168.0.0/24
2. adb connect <target_ip>:5555
3. adb shell
4. Use ls, cd and pwd to navigate
5. adb pull to get certain files

# Encrypted Volumes
1. Use Veracrypt to decrypt the volume
2. Select File... -> Choose a Drive to mount on -> Mount
3. There is normally a password to decrypt. It should be provided somewhere.
4. Go to unlocked Drive, do your task.

# Cracking Hashes
1. Use www.hashes.com

# Remote Access Trojans (RAT)
1. CEH Module 7 Malware Threats -> Trojan Types -> RAT -> Theef
2. Try to find unusual ports by running

# Hash Tampering
1. Use MD5 Calculator to compare hashes

# Finding files in DVWA
If given a link (http://192.168.0.##:8080/DVWA)
And a path Eg. “C:\wamp64\www\DVWA\hackable\uploads\”
1. Take the tail of the path (\hackable\uploads\) and add it to the end of the link
2. Should show a file directory with target files.

