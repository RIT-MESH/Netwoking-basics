# Wireless Networking Guide

## **Wireless Standards (802.11a/b/g/n/ac/ax)**

### **Theory**
Wireless networking operates on different IEEE 802.11 standards that define wireless communication protocols. These standards vary in speed, range, and frequency.

### **Comparison of Wireless Standards:**
| Standard | Frequency | Max Speed | Range | Notes |
|----------|----------|-----------|-------|-------|
| **802.11a** | 5 GHz | 54 Mbps | Short | Less interference but limited range |
| **802.11b** | 2.4 GHz | 11 Mbps | Long | Prone to interference but good range |
| **802.11g** | 2.4 GHz | 54 Mbps | Long | Backward compatible with 802.11b |
| **802.11n** | 2.4/5 GHz | 600 Mbps | Long | Introduced MIMO (Multiple Input Multiple Output) |
| **802.11ac** | 5 GHz | 6.9 Gbps | Medium | Supports MU-MIMO (Multi-User MIMO) |
| **802.11ax (Wi-Fi 6)** | 2.4/5 GHz | 9.6 Gbps | Medium | Improved efficiency, lower latency |

---

## **Wireless Security (WPA, WPA2, WPA3)**

### **Theory**
Wireless security ensures data protection and access control. The **Wi-Fi Protected Access (WPA)** family of protocols is widely used.

### **Comparison of Wireless Security Protocols:**
| Security Standard | Encryption | Security Level | Notes |
|-------------------|------------|---------------|-------|
| **WPA** | TKIP | Medium | Vulnerable to attacks, no longer recommended |
| **WPA2** | AES-CCMP | High | Most commonly used, but susceptible to KRACK attack |
| **WPA3** | AES-GCMP | Very High | More secure, prevents offline dictionary attacks |

### **Example: Configuring WPA2 on a Cisco Access Point**
```cisco
AP# configure terminal
AP(config)# interface Dot11Radio0
AP(config-if)# ssid MyWiFi
AP(config-if-ssid)# authentication open
AP(config-if-ssid)# authentication key-management wpa version 2
AP(config-if-ssid)# wpa-psk ascii MySecurePassword
AP(config-if-ssid)# end
```

---

## **Wireless LAN Controllers (WLCs)**

### **Theory**
Wireless LAN Controllers (WLCs) manage multiple access points (APs) in a network, providing centralized control, security, and policy enforcement.

### **Key Features of WLCs:**
- Centralized AP management
- RF optimization and channel selection
- User authentication and security enforcement
- Guest network and VLAN segmentation

### **Example: Configuring a Wireless LAN Controller**
```cisco
WLC# configure terminal
WLC(config)# wlan MyWiFi 1 MyWiFiSSID
WLC(config-wlan)# security wpa wpa2
WLC(config-wlan)# wpa passphrase MySecurePassword
WLC(config-wlan)# enable
WLC(config)# end
```

---

## **Basic Wireless Configuration and Troubleshooting**

### **Wireless Configuration Steps:**
1. Enable the wireless interface.
2. Configure the SSID and authentication method.
3. Set encryption standards.
4. Assign an IP address and VLAN if necessary.
5. Apply and save the configuration.

### **Example: Basic Wireless Configuration on a Cisco AP**
```cisco
AP# configure terminal
AP(config)# interface Dot11Radio0
AP(config-if)# ssid HomeNetwork
AP(config-if-ssid)# authentication open
AP(config-if-ssid)# authentication key-management wpa version 2
AP(config-if-ssid)# wpa-psk ascii SecurePassword
AP(config-if)# end
```

### **Wireless Troubleshooting Steps:**
1. **Check Signal Strength:** Ensure the AP is within range.
2. **Verify SSID and Security Settings:** Confirm clients are using the correct SSID and password.
3. **Check for Interference:** Look for overlapping Wi-Fi channels or other wireless devices.
4. **Inspect DHCP and IP Configuration:** Ensure clients receive proper IP addresses.
5. **Use Debug and Show Commands:**
```cisco
AP# show wireless summary
AP# show dot11 associations
AP# debug dot11 events
```

---

This guide provides an overview of **wireless networking**, covering **standards, security, WLCs, and troubleshooting** with **real-world examples and Cisco configurations**. 
