# Automation and Programmability Guide

## **Network Automation Concepts**

### **Theory**
Network automation simplifies configuration, management, and troubleshooting by using scripts and APIs to reduce manual intervention. It enhances efficiency, consistency, and scalability in network operations.

### **Key Benefits:**
- Reduces human errors
- Increases deployment speed
- Ensures configuration consistency
- Enables programmability with APIs and scripts

**Example:** Automating VLAN creation across multiple Cisco switches using a Python script with SSH or REST APIs.

---

## **Basics of JSON, XML, and YAML**

### **Theory**
Data serialization formats like JSON, XML, and YAML are commonly used in network automation for exchanging and storing structured data.

### **Comparison of Formats:**
| Format | Description | Example |
|--------|------------|---------|
| **JSON** | Lightweight, human-readable, widely used in APIs | `{ "hostname": "router1", "ip": "192.168.1.1" }` |
| **XML** | More structured, used in legacy systems | `<device><hostname>router1</hostname><ip>192.168.1.1</ip></device>` |
| **YAML** | Simple syntax, used in automation tools | `hostname: router1
 ip: 192.168.1.1` |

### **Example Usage in Python:**
```python
import json

# Convert dictionary to JSON
network_device = {"hostname": "router1", "ip": "192.168.1.1"}
json_output = json.dumps(network_device, indent=4)
print(json_output)
```

---

## **REST APIs and Their Role in Network Automation**

### **Theory**
REST APIs allow network devices to be programmatically managed using standard HTTP methods (GET, POST, PUT, DELETE). 

**Common Use Cases:**
- Retrieving device information
- Modifying configurations remotely
- Automating monitoring tasks

### **Example: Using REST API with Python (Requests Module)**
```python
import requests

url = "http://192.168.1.1/api/v1/device"
headers = {"Content-Type": "application/json"}
response = requests.get(url, headers=headers, auth=("admin", "password"))
print(response.json())
```

---

## **Cisco DNA Center and SD-Access Overview**

### **Theory**
- **Cisco DNA Center** provides centralized management for enterprise networks using automation, AI-driven insights, and policy-based security.
- **SD-Access** (Software-Defined Access) simplifies network segmentation and access policies by using intent-based networking.

### **Key Features of Cisco DNA Center:**
- **Automation**: Zero-touch provisioning
- **Analytics**: AI-driven network monitoring
- **Security**: Identity-based segmentation

**Example:** Using Cisco DNA Center API to fetch network device inventory.

```python
import requests

url = "https://dnacenter/api/v1/network-device"
token = "YOUR_ACCESS_TOKEN"
headers = {"X-Auth-Token": token, "Content-Type": "application/json"}
response = requests.get(url, headers=headers, verify=False)
print(response.json())
```

---
## **Ansible for Network Automation**

Ansible is widely used for automating network devices because it is agentless and uses simple **YAML-based playbooks**. It connects to devices using SSH or APIs.

### **1. Automating VLAN Configuration on Cisco Switches**
```yaml
- name: Configure VLANs on Cisco Switch
  hosts: switches
  gather_facts: no
  tasks:
    - name: Create VLAN 10
      cisco.ios.ios_vlan:
        vlan_id: 10
        name: SALES
        state: present
```

### **2. Configuring Interface on Cisco Router**
```yaml
- name: Configure Interface on Cisco Router
  hosts: routers
  gather_facts: no
  tasks:
    - name: Assign IP to Interface
      cisco.ios.ios_interface:
        name: GigabitEthernet0/1
        description: Uplink to ISP
        enabled: yes
        state: present
```

### **3. Running Show Commands on Cisco Devices**
```yaml
- name: Gather Facts from Cisco Devices
  hosts: switches
  gather_facts: no
  tasks:
    - name: Run Show Commands
      cisco.ios.ios_command:
        commands:
          - show version
          - show ip interface brief
      register: output

    - name: Display Output
      debug:
        var: output.stdout_lines
```

### **4. Configuring SNMP on Cisco Devices**
```yaml
- name: Configure SNMP on Cisco Router
  hosts: routers
  gather_facts: no
  tasks:
    - name: Enable SNMP
      cisco.ios.ios_config:
        lines:
          - snmp-server community public RO
          - snmp-server community private RW
```

### **5. Automating Backup of Configurations**
```yaml
- name: Backup Running Configurations
  hosts: routers
  tasks:
    - name: Save Configuration Backup
      cisco.ios.ios_command:
        commands:
          - copy running-config startup-config
```

### **6. Configuring NTP on Cisco Devices**
```yaml
- name: Configure NTP Server
  hosts: routers
  gather_facts: no
  tasks:
    - name: Set NTP Server
      cisco.ios.ios_config:
        lines:
          - ntp server 192.168.1.100
```

### **7. Configuring BGP on Cisco Devices**
```yaml
- name: Configure BGP Neighbor
  hosts: routers
  gather_facts: no
  tasks:
    - name: Add BGP Neighbor
      cisco.ios.ios_config:
        lines:
          - router bgp 65000
          - neighbor 192.168.1.2 remote-as 65001
```

### **8. Automating OS Upgrades on Cisco Devices**
```yaml
- name: Upgrade Cisco IOS
  hosts: routers
  gather_facts: no
  tasks:
    - name: Load New IOS Image
      cisco.ios.ios_command:
        commands:
          - copy tftp://192.168.1.10/cisco_ios.bin flash:
```

### **9. Configuring Firewall Rules**
```yaml
- name: Configure ACL Rules on Cisco Firewall
  hosts: firewalls
  gather_facts: no
  tasks:
    - name: Allow SSH Traffic
      cisco.ios.ios_config:
        lines:
          - access-list 100 permit tcp any any eq ssh
```

### **10. Automating VLAN Trunking**
```yaml
- name: Configure Trunk Ports
  hosts: switches
  gather_facts: no
  tasks:
    - name: Set Trunk Mode
      cisco.ios.ios_interface:
        name: GigabitEthernet0/1
        mode: trunk
```

---


## **Puppet for Network Automation**

### **Theory**
Puppet is an **agent-based** configuration management tool that automates network and server configurations using a **declarative language**.

### **Use Cases:**
- Automating switch and router configurations
- Enforcing security policies across devices
- Managing network firmware updates

### **Example: Managing SNMP Configuration with Puppet**
```puppet
class snmp_config {
  ios_config { "Enable SNMP":
    command => "snmp-server community public RO",
  }
}
```

### **Example: Enforcing SSH on Cisco Devices**
```puppet
class ssh_enable {
  ios_config { "Enable SSH":
    command => "ip ssh version 2",
  }
}
```

---

## **Chef for Network Automation**

### **Theory**
Chef uses a **Ruby-based DSL** to define configurations in **cookbooks** and **recipes**. It is agent-based and follows an imperative approach.

### **Use Cases:**
- Managing switch and router configurations
- Automating firewall rule updates
- Deploying software patches on network devices

### **Example: Configuring an Interface on Cisco Router with Chef**
```ruby
cisco_interface 'GigabitEthernet1' do
  description 'Uplink to Core'
  switchport_mode 'trunk'
end
```

### **Example: Configuring OSPF on Cisco Router with Chef**
```ruby
cisco_ospf 'ospf1' do
  router_id '192.168.1.1'
  area '0'
end
```

---

This guide provides a structured approach to **network automation and programmability**, covering **data formats, REST APIs, Cisco DNA Center, and automation tools like Ansible, Puppet, and Chef**, with **expanded Ansible, Puppet, and Chef use cases and practical configurations**.
