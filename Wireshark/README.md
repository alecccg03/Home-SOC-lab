# **Wireshark Analysis**

This section documents packet-level observations only. Deeper analysis is provided in the Investigation Notes folder.

## **Nmap SYN Scan**

*Capture:* Nmap SYN Scan.png
*Filter:* tcp.flags.syn == 1
*Observation:* Large volume of SYN packets being sent from the Kali machine to the Windows target over various ports. No ACK packets, many SYN ACK packets followed by RST packets.

## **Nmap Port Scan**

*Capture:* Nmap Port Enumeration.png
*Filter:* tcp && ip.src == 192.168.202.132 (Kali VM)
*Observation:* Flood of SYN packets from the Kali machine to the Windows target to ports 1-1000. Windows machine responded with SYN ACK packets for open ports.

## **Web Enumeration**

*Capture:* Web Enumeration.png
*Filter:* tcp.port == 80
*Observation:* Multiple TCP SYN packets and retransmissions observed from the Kali machine, indicating repeated connection attempts to identified services.

## **ICMP Recon**

*Capture:* ICMP Recon.png
*Filter:* icmp
*Observation:* Repeated ICMP echo requests and replies from the Kali machine to the Windows target
