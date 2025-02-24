# Security Fundamentals Guide

## **Security Concepts (Threats, Vulnerabilities, Exploits)**

### **Theory**
Security concepts revolve around protecting networks, systems, and data from cyber threats. The three core elements are:

- **Threats**: Potential dangers that can exploit a vulnerability, such as malware, phishing, and denial-of-service (DoS) attacks.
- **Vulnerabilities**: Weaknesses in a system that can be exploited, such as outdated software or weak passwords.
- **Exploits**: Methods used by attackers to take advantage of vulnerabilities, such as SQL injection or buffer overflow attacks.

**Example:** A hacker finds a weakness in an outdated web application (vulnerability) and uses an SQL injection attack (exploit) to gain unauthorized access to the database.

---

## **Access Control Lists (ACLs)**

### **Theory**
ACLs are used to filter network traffic and enforce security policies by permitting or denying packets based on IP addresses, protocols, or port numbers.

**Example:** A company allows only internal users (192.168.1.0/24) to access the web server (192.168.2.10) but blocks external users.

### **How to Configure ACLs on a Cisco Device**
```cisco
Router# configure terminal
Router(config)# access-list 100 permit tcp 192.168.1.0 0.0.0.255 host 192.168.2.10 eq 80
Router(config)# access-list 100 deny ip any any
Router(config)# interface gigabitEthernet 0/1
Router(config-if)# ip access-group 100 in
Router(config-if)# exit
Router(config)# end
```

---

## **Port Security**

### **Theory**
Port security is a feature that restricts network access by limiting the number of MAC addresses that can connect to a switch port.

**Example:** In an office environment, IT restricts each desk switch port to a single MAC address to prevent unauthorized devices from connecting.

### **How to Configure Port Security on a Cisco Switch**
```cisco
Switch# configure terminal
Switch(config)# interface fastEthernet 0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport port-security
Switch(config-if)# switchport port-security maximum 2
Switch(config-if)# switchport port-security violation restrict
Switch(config-if)# switchport port-security mac-address sticky
Switch(config-if)# end
```

---

## **VPN (Virtual Private Network) Basics**

### **Theory**
A VPN provides a secure encrypted connection over a public network, allowing remote users to securely access private resources.

**Example:** A remote employee uses a VPN to securely connect to the company’s internal network from home.

### **How to Configure a Site-to-Site VPN on a Cisco Router**
```cisco
Router# configure terminal
Router(config)# crypto isakmp policy 10
Router(config-isakmp)# encryption aes 256
Router(config-isakmp)# hash sha256
Router(config-isakmp)# authentication pre-share
Router(config-isakmp)# group 2
Router(config-isakmp)# exit
Router(config)# crypto isakmp key mykey address 192.168.2.1
Router(config)# crypto ipsec transform-set MYSET esp-aes esp-sha-hmac
Router(config)# crypto map MYMAP 10 ipsec-isakmp
Router(config-crypto-map)# set peer 192.168.2.1
Router(config-crypto-map)# set transform-set MYSET
Router(config-crypto-map)# match address 101
Router(config-crypto-map)# exit
Router(config)# interface gigabitEthernet 0/1
Router(config-if)# crypto map MYMAP
Router(config-if)# exit
Router(config)# end
```

---

## **Authentication, Authorization, and Accounting (AAA)**

### **Theory**
AAA is a framework for controlling network access:
- **Authentication** verifies user identity (e.g., username/password, biometrics).
- **Authorization** determines what resources a user can access.
- **Accounting** logs user activities for monitoring and auditing.

**Example:** A corporate network uses AAA to restrict access based on roles—managers can access sensitive data, while employees have limited access.

### **How to Configure AAA on a Cisco Router**
```cisco
Router# configure terminal
Router(config)# aaa new-model
Router(config)# aaa authentication login default local
Router(config)# aaa authorization exec default local
Router(config)# username admin privilege 15 secret mysecurepassword
Router(config)# end
```

---

## **Device Hardening Techniques**

### **Theory**
Device hardening involves securing network devices to minimize vulnerabilities. Common practices include:
- Disabling unused services
- Implementing strong passwords
- Enabling logging and auditing
- Applying software updates regularly

**Example:** A network administrator disables Telnet and enforces SSH for secure remote management.

### **How to Harden a Cisco Router**
```cisco
Router# configure terminal
Router(config)# service password-encryption
Router(config)# no ip http server
Router(config)# ip ssh version 2
Router(config)# login block-for 60 attempts 3 within 30
Router(config)# enable secret strongpassword
Router(config)# end
```

---

This guide provides an in-depth understanding of **security fundamentals**, including **threats, ACLs, VPNs, AAA, and device hardening**, with **real-world examples and Cisco configurations**.
