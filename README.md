Nmap & Scapy Lab Documentation

1. Introduction
This lab focused on practicing network scanning, service enumeration, and packet sniffing using Nmap and Scapy.
All activities were performed on a controlled internal network.

Target System: 10.6.6.23
Network: 10.6.6.0/24

These exercises build foundational skills for ethical hacking and reconnaissance.


2. Lab Environment

Machine: Kali Linux
Network: 10.6.6.0/24

Tools Used:
	•	Nmap
	•	Scapy
	•	Wireshark
	•	SMBClient

3. Nmap Practical Work

3.1 Host Discovery (Ping Sweep)

Command
nmap -sn 10.6.6.0/24
Purpose: Identify live hosts on the network.
Result: 10.6.6.23 was detected as UP.

3.2 OS Detection

Command
sudo nmap -O 10.6.6.23
Purpose: Attempt to determine the operating system.
Result: Nmap returned an OS guess based on TCP/IP fingerprinting.

3.3 Service & Version Detection (FTP)

Command
nmap -p21 -sV -A -T4 10.6.6.23
Purpose: Identify services and versions running on port 21.
Result: FTP service and version details were discovered.

3.4 SMB Enumeration (Port 445)

Command
nmap --script smb-enum-shares.nse -p445 10.6.6.23
Purpose: List SMB shares and check access permissions.
Result: Shares were listed along with permission levels.

3.5 Manual SMB Access Test

Command
smbclient //10.6.6.23/print$ -N
Purpose: Test anonymous SMB login.
Outcome: Anonymous login successful → potential misconfiguration.
(Use exit to quit.)

4. Scapy Practical Work

All work was performed inside the Scapy interactive shell.

4.1 Starting Scapy
sudo su
scapy

4.2 Sniffing All Traffic

Command
sniff()
Purpose: Capture traffic on the internal bridge network.

Triggered traffic by:

Opening browser → visiting 10.6.6.23
Doing network pings
Saved results:
paro2 = _
paro2.summary()
4.4 Filtering Only ICMP

Command:

sniff(iface="br-internal", filter="icmp", count=5)
Test traffic:

ping 10.6.6.23
Captured exactly 5 ICMP packets.

Stored and inspected:

paro3 = _
paro3.summary()
paro3[3]
 5. Key Learnings
Nmap can detect live hosts, services, versions, and OS fingerprints.
SMB enumeration revealed possible anonymous access weaknesses.
Scapy allows live packet sniffing and analyzing ICMP, DNS, ARP, and more.
Using filters makes packet capture more targeted and efficient.
Hands-on testing shows how attackers gather information early in a penetration test.
🏁 6. Conclusion
This lab strengthened my practical understanding of reconnaissance using Nmap and packet analysis using Scapy. Scanning, enumeration, and sniffing are critical steps in ethical hacking, and these exercises improved my confidence with real cybersecurity tools.
