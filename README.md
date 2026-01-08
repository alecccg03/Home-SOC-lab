# Home-SOC-lab
Conducted separate network-level and log-based attack simulations to analyze detection capabilities across different sources

📌 Project Overview
This lab demonstrates the end-to-end process of simulating cyber attacks, capturing telemetry, and analyzing data within a Security Operations Center (SOC) environment. I performed various network-level and host-based attacks against a Windows target, ingested the logs into Splunk, and used Wireshark for deep packet inspection.

🛠️ Toolset

SIEM: Splunk Enterprise (on Ubuntu VM)

Telemetry: Sysmon (Windows Target), Splunk Universal Forwarder

Network Analysis: Wireshark, TCPDump

Attack Tools: Nmap, Curl, SSH, ICMP

Environment: VMware/VirtualBox (Isolated Lab Network)

🛡️ Analysis Scenarios

1. Nmap Stealth (SYN) Scan
   
The Attack: Executed a SYN scan (nmap -sS) to identify open ports without completing the three-way handshake.

Wireshark Analysis: Observed a high volume of SYN packets followed by RST packets from the attacker to the target.

Splunk Detection: Created a dashboard to visualize spikes in destination ports per source IP.

Query: index=sysmon EventCode=3 | stats dc(dest_port) by src_ip | where 'dc(dest_port)' > 50

2. Failed SSH Brute Force
   
The Attack: Simulated connection attempts to port 22 on a closed service to observe "connection reset" behavior.

Key Finding: Confirmed that failed connections to closed ports generate repetitive RST, ACK flags.

Documentation: Verified that while a single failure is low-noise, automated attempts generate hundreds of logs in seconds.

3. Web & ICMP Enumeration
   
The Attack: Used curl for web directory discovery and ping for host discovery.

Analysis: Captured the 84-byte ICMP packets (Linux default) and analyzed the CommandLine arguments in Sysmon Event ID 1 to identify the specific curl strings used.

📊 Dashboards & Visualizations

I developed a Splunk dashboard to provide "at-a-glance" situational awareness:

Top 10 Scanned Ports: Visualizing where the majority of SYN packets are landing.

Command Line Activity: Tracking suspicious process arguments (e.g., -enc, curl, nmap).

Network Map: Correlating Source IPs with destination port frequency.

💡 Key Learnings
Protocol Differences: Deepened understanding of why SSH/HTTP require TCP (reliability) while diagnostics use ICMP (Layer 3).

Log Ingestion: Configured the Splunk Universal Forwarder and inputs.conf to streamline Sysmon data flow.

Data Sanitization: Practiced professional OPSEC by identifying and masking internal IP structures in reports.

🚀 How to Use
Sysmon Config: Find my sysmon-config.xml in the /configs folder.

Splunk Queries: Check the queries.md file for all SPL used in the visualizations.

Pcap Files: Sample traffic captures are located in the /pcaps directory.
