# IP Connectivity Guide

## **Routing Concepts (Static vs. Dynamic Routing)**

### **Theory**
Routing is the process of forwarding packets between networks. There are two main types of routing:

### **Static Routing:**
- Manually configured by network administrators.
- Suitable for small and stable networks.
- No automatic failover.

### **Dynamic Routing:**
- Uses protocols to automatically discover and update routes.
- Scales better for large networks.
- Provides automatic failover.

**Example of Static vs. Dynamic Routing:**
| Feature | Static Routing | Dynamic Routing |
|---------|---------------|----------------|
| Configuration | Manual | Automatic |
| Adaptability | Does not change | Adapts to topology changes |
| Overhead | Low | Higher due to updates |
| Scalability | Limited | Highly scalable |

---

## **Routing Protocols (RIP, OSPF, EIGRP)**

### **RIP (Routing Information Protocol):**
- Uses **hop count** as a metric.
- Maximum of **15 hops**.
- **Slow convergence**, not suitable for large networks.

**Example: Configuring RIP on a Cisco Router:**
```cisco
Router# configure terminal
Router(config)# router rip
Router(config-router)# version 2
Router(config-router)# network 192.168.1.0
Router(config-router)# network 10.0.0.0
Router(config-router)# end
```

### **OSPF (Open Shortest Path First):**
- Uses **cost** (bandwidth-based metric).
- **Link-state protocol**, maintains a complete topology.
- **Faster convergence** and supports VLSM.

**Example: Configuring OSPF on a Cisco Router:**
```cisco
Router# configure terminal
Router(config)# router ospf 1
Router(config-router)# network 192.168.1.0 0.0.0.255 area 0
Router(config-router)# end
```

### **EIGRP (Enhanced Interior Gateway Routing Protocol):**
- Uses **bandwidth and delay** as composite metrics.
- **Fast convergence**, supports unequal cost load balancing.
- **Cisco proprietary protocol** (though now partially open).

**Example: Configuring EIGRP on a Cisco Router:**
```cisco
Router# configure terminal
Router(config)# router eigrp 100
Router(config-router)# network 192.168.1.0 0.0.0.255
Router(config-router)# end
```

---

## **IPv4 and IPv6 Static Routing**

### **Configuring IPv4 Static Routing**
```cisco
Router# configure terminal
Router(config)# ip route 192.168.2.0 255.255.255.0 10.1.1.1
Router(config)# end
```

### **Configuring IPv6 Static Routing**
```cisco
Router# configure terminal
Router(config)# ipv6 route 2001:db8:1::/64 2001:db8:2::1
Router(config)# end
```

---

## **Router Operation and Configuration**

### **Basic Router Configuration Steps:**
1. Set a hostname.
2. Configure interfaces.
3. Set up routing.
4. Secure access with passwords.
5. Save configuration.

**Example: Basic Cisco Router Setup**
```cisco
Router# configure terminal
Router(config)# hostname MyRouter
Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config)# exit
Router(config)# end
```

---

## **Troubleshooting IP Connectivity**

### **Common Issues and Solutions:**
| Issue | Cause | Solution |
|--------|--------|----------|
| No connectivity | Incorrect IP or subnet | Verify IP settings with `show ip interface brief` |
| Routing failure | Missing routes | Check `show ip route` and add necessary routes |
| High latency | Network congestion | Use `ping` and `traceroute` to diagnose |

### **Example: Useful Troubleshooting Commands**
```cisco
! Check interface status
Router# show ip interface brief

! Check routing table
Router# show ip route

! Test connectivity
Router# ping 8.8.8.8

! Trace packet path
Router# traceroute 8.8.8.8
```

---

This guide provides a structured approach to **IP connectivity**, covering **routing concepts, protocols, configuration, and troubleshooting** with **real-world examples and Cisco configurations**. 
