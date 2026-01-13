# **Investigation Notes**


## **Nmap SYN Scan Analysis**


Src IP: 192.168.202.132

Dst IP: 192.168.202.134

```bash
nmap -sS 192.168.202.134
```

*What protocol is being used?*

	When doing an nmap scan against a host, a flood of SYN packets is sent to various ports using TCP
	
*What ports?*

	Depending on your nmap scan command, you can scan various ports or a certain range of ports. Some ports included in this scan are 25, 80, 111, 143, 145, 443, 256, 22, 23, 4, 53, 21.
	
*How many packets?*

	An nmap scan can generate hundreds to thousands of packets. This one generated about 1900 packets because a lot of the ports were closed, resulting in about 2 packets for each port scanned: 1 SYN packet by the attacker and 1 RST by the target. If there were more open ports, it would result in more packets overall because the flow would then be: SYN packet by the attacker, SYN ACK by the target, and RST by the attacker, giving you three packets instead of only two.
	
*How is this different than normal browsing?*

	When doing an nmap SYN scan, there is no complete three-way handshake. The host performing the scan sends SYN packets to all ports on the target host. The target responds with a SYN ACK packet for ports that are open. The enumerating host then sends a RST packet back to end the connection, not an ACK like a normal three-way handshake. This is because the enumerating host is trying to find available services on the target, not directly connect to it. Normal browsing completes the three-way handshake with SYN >> SYN ACK >> ACK to confirm the connection and start sending data.



## **Nmap Port Scan Analysis**


Src IP: 192.168.202.132

Dst IP: 192.168.202.134

```bash
nmap -p 1-1000 192.168.202.134
```

*Repetition:* The source host sends two SYN packets to each port specified in the scan (1-1000) to the target host
*Speed:* Each packet takes about .003 seconds, evidence of an automated attack and not being done by a human
*Protocol:* TCP is used for an nmap port scan

*How many packets?*

	This scan generated about 2000 packets


## **Web Enumeration Analysis**

```bash
curl http://192.168.202.134
```

*What protocol is being used?*

	Since curl is primarily used for transferring data from urls, it uses TCP to ensure data arrives reliably and in the correct order
	
*What ports?*

	Since the curl command was using an http link, it uses port 80
	
*How many packets?*

	This command generate about 16 packets, which is around the typical amount for curl to an http site


## **ICMP Recon Analysis**

```bash
ping -c 10 192.168.202.134
```

*What protocol is being used?*

	ICMP recon uses the ICMP (internet control message protocol) protocol
	
*What ports?*

	ICMP does not use a port because it operates on the network layer (layer 3) of the OSI model. This is different than TCP or UDP which operates at the transport layer (layer 4). ICMP is used for diagnostics and reporting, not delivering data so it doesn't use a port.
	
*How many packets?*

	This specific command generated 10 packets (-c 10). Sometimes it will only be a few like 3-4, but it can also be dozens or hundreds when using Nmap's ICMP scan.
	

	ICMP is normal, but a large volume of ICMP packets should be cause for suspicion

