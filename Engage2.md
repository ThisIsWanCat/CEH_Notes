# Password cracking

sudo john --format=”<NAME>” “<FILENAME>”

# Steganography
Whitespace
./SNOW.EXE -C <Filedir>

Images
OpenStego -> Extract data -> input file dir

# Wireshark Stuff
If using COVERT_TCP
Use Statistics -> IPV4 Statistics -> Source and Destination Addresses -> use filter tcp.flags.syn == 1 and tcp.flags.ack == 0 to get potential IP src and target
Set display filter to tcp.flags.syn == 1 and tcp.flags.ack == 0 and ip.src==<SRC_IP> and ip.dst==<DST_IP>
Make sure to look at the ip.id hex value (Bytes 18-19)
Try matching required field with number of packets sent

# Malware Analysis
Finding filepos or memory pos (Use BinText)

Analyze ELF exe (Use DIE)

Check operating system registry for changes (Use Reg Organizer)
Tools -> Registry Snapshots -> Create and Compare with Current Registry

Windows Service Monitoring (Use SrvMan)

# DHCP Starvation Attack
1. sudo yersinia -G
2. Launch attack -> DHCP -> sending DISCOVER packet
3. Have wireshark listening
4. Search traffic for DHCP

# Detect ARP Spoofing
1. Set filter to arp
2. Edit -> Find packet -> String -> "duplicate use of"

# Detect ICMP traffic
1. Use ICMP as filter

# Find Passwords in network traffic
1. Filter with http.request.method==POST
2. Find a HTTP/1.1 Packet
3. Scroll down to 'HTML Form URL Encoded' and expand