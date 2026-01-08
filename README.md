# Home-SOC-lab
Conducted separate network-level and log-based attack simulations to analyze detection capabilities across different sources.

📌 Project Overview
This lab demonstrates the end-to-end process of simulating cyber attacks, capturing telemetry, and analyzing data within a Security Operations Center (SOC) environment. I performed various network-level and host-based attacks against a Windows target, ingested the logs into Splunk, and used Wireshark for deep packet inspection.

Network traffic analysis and SIEM detection were conducted in separate attack runs to focus on tool-specific visibility and detection capabilities.

🛠️ Toolset

SIEM: Splunk Enterprise 

Telemetry: Sysmon (Windows Target), Splunk Universal Forwarder

Network Analysis: Wireshark, TCPDump

Attack Tools: Nmap, Curl, SSH, ICMP

Environment: VMware/VirtualBox (Isolated Lab Network) - Kali Linux VM (attacker), Windows VM (target)

🛡️ Analysis Scenarios

1. Nmap (SYN) Scan
   
Performed a SYN scan using nmap and analyzed the traffic in Wireshark.

2. Nmap Port Scan
   
Performed a scan across the first 1000 ports to discover open services and analyzed in Wireshark.

3. Web & ICMP Enumeration
   
Performed web directory and host discovery using curl and ping.

4. Authentication attempts

Performed two separate attacks trying to connect to the target host over ssh. I analyzed the traffic in Wireshark and created visualizations in Splunk.

📊 Dashboards & Visualizations

Developed a Splunk dashboard with multiple visualizations to better understand and further analyze logs from simulated attacks.

💡 Key Learnings
Protocol Differences: This lab reinforced the differences between connection-oriented and connectionless protocols by analyzing TCP handshakes, port scans and encrypted SSH sessions at the packet level.

Log Ingestion: Gained hands-on experience analyzing Windows authentication and firewall logs in Splunk to detect brute-force behavior and understand how endpoint logs reflect attacker activity.

Visibility Gap: This lab highlighted the importance of defense-in-depth by demonstrating how network traffic, endpoint logs and firewall telemetry provide different views of malicious activity.

🚀 How to Use

Splunk Queries: Check the queries.md file for all SPL used in the visualizations.

Pcap Files: Sample traffic captures are located in the /pcaps directory.
