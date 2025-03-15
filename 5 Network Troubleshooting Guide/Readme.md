# Network Troubleshooting Guide


https://github.com/user-attachments/assets/7c32defa-ff20-41f3-8368-2963f98457ea


## **Troubleshooting Methodologies**

### **Theory**
Effective troubleshooting follows a structured approach to identify and resolve network issues efficiently. Common methodologies include:

1. **Identify the Problem** – Gather information from users, logs, and monitoring tools.
2. **Establish a Theory** – Hypothesize potential causes (e.g., misconfiguration, hardware failure, congestion).
3. **Test the Theory** – Use troubleshooting tools and commands to verify the cause.
4. **Develop and Implement a Solution** – Apply a fix based on findings.
5. **Verify Resolution** – Confirm the issue is resolved and the network operates normally.
6. **Document the Findings** – Keep records for future reference and prevent recurrence.

**Example:** If users report slow internet, a network administrator may first check bandwidth usage and router logs before testing configurations and implementing QoS policies.

---

## **Troubleshooting Common Network Issues**

### **1. Connectivity Issues**

- **Causes:** Faulty cables, incorrect IP configurations, DNS failures.
- **Solution:** Check physical connections, verify IP settings, and restart network services.

### **How to Diagnose and Fix Connectivity Issues**
```cisco
! Check physical link status
Router# show interfaces status

! Verify IP configuration
Router# show ip interface brief

! Restart network services (example for Linux systems)
sudo systemctl restart networking

! Flush DNS cache (Windows example)
ipconfig /flushdns
```

---

### **2. Performance Issues**

- **Causes:** Network congestion, high CPU usage, outdated firmware.
- **Solution:** Analyze bandwidth usage, enable QoS, upgrade firmware.

### **How to Diagnose and Fix Performance Issues**
```cisco
! Check interface traffic statistics
Router# show interfaces

! Monitor CPU usage
Router# show processes cpu sorted

! Enable QoS for VoIP traffic
Router(config)# class-map match-any VOIP
Router(config-cmap)# match protocol rtp
Router(config-cmap)# exit
Router(config)# policy-map QOS_POLICY
Router(config-pmap)# class VOIP
Router(config-pmap-c)# priority 1000
Router(config-pmap)# exit
Router(config)# interface serial 0/0/0
Router(config-if)# service-policy output QOS_POLICY
Router(config-if)# end
```

---

### **3. Security Issues**

- **Causes:** Unauthorized access, malware, misconfigured firewalls.
- **Solution:** Review firewall rules, scan for threats, enforce access controls.

### **How to Diagnose and Fix Security Issues**
```cisco
! Verify firewall rules
Router# show access-lists

! Check for unauthorized logins
Router# show login failures

! Scan for threats using security logs
Router# show logging

! Enforce SSH for secure remote management
Router(config)# ip ssh version 2
Router(config)# line vty 0 4
Router(config-line)# transport input ssh
Router(config-line)# exit
Router(config)# end
```

---

## **Using Tools Like Ping, Traceroute, and Show Commands**

### **Theory**
Network troubleshooting relies on various tools to diagnose issues efficiently.

- **Ping** – Tests network connectivity by sending ICMP echo requests.
- **Traceroute** – Tracks the path of packets to identify slow or failing hops.
- **Show Commands** – Displays device configurations, logs, and statistics.

### **Example Usage in Cisco IOS**
```cisco
! Check if a device is reachable
Router# ping 8.8.8.8

! Trace packet route
Router# traceroute 8.8.8.8

! View interface status
Router# show ip interface brief

! Display routing table
Router# show ip route
```

---

## **Analyzing Network Traffic with Packet Capture Tools**

### **Theory**
Packet capture tools allow administrators to inspect network traffic, identify anomalies, and troubleshoot issues.

- **Wireshark** – Graphical packet analyzer for deep traffic analysis.
- **Tcpdump** – Command-line packet capture tool.
- **SPAN (Switch Port Analyzer)** – Used on Cisco switches to mirror traffic for analysis.

### **Example Usage**
```bash
# Capture packets on a Linux system using tcpdump
sudo tcpdump -i eth0 -nn -c 100 -w capture.pcap

# Open capture in Wireshark for analysis
wireshark capture.pcap
```

**Example:** If VoIP calls have poor quality, capturing RTP packets with Wireshark can help detect jitter and packet loss.

---

This guide provides a structured approach to **network troubleshooting**, covering **methodologies, common issues, diagnostic tools, and traffic analysis** with **real-world examples and practical configurations**.

