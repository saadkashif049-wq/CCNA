# 🌐 CCNA 200-301: Learning Journey

![CCNA Badge](https://img.shields.io/badge/Certification-CCNA%20200--301-blue?style=for-the-badge&logo=cisco)
![Day](https://img.shields.io/badge/Progress-Day%2004-brightgreen?style=for-the-badge)

## 📌 Day 04: IP Address Functions, Classless Routing (CIDR) & NAT/ARP Packet Flow

This repository contains structured technical study notes for **CCNA Day 4**. It covers the operational roles of Network, Broadcast, and Host addresses, the architectural shift from Classful to Classless (CIDR) addressing, and a step-by-step trace of packet movement — including NAT and ARP — across a residential LAN out to the public internet.

---

## 1. Functional Roles of IPv4 Address Types

Every allocated IP subnet is defined by three structural address components:

### 1.1 Network Address (The Subnet Identifier)
- **Definition:** The **first IP address** in a subnet's range.
- **Rule:** Never assignable to a host or interface.
- **Purpose:** Identifies the subnet as a whole. Upstream routers use this prefix in their routing tables to reach entire network segments without tracking individual hosts.
- **Example (`192.168.1.0/24`):** `192.168.1.0`

### 1.2 Broadcast Address (The Network "Megaphone")
- **Definition:** The **last IP address** in a subnet's range.
- **Rule:** Reserved for network-wide transmission; never assignable to a host.
- **Purpose:** Enables **one-to-all** local signaling. A packet sent to this address is flooded by Layer 2 switches out every port, so every active host on the LAN receives it (e.g., DHCP Discover broadcasts).
- **Example (`192.168.1.0/24`):** `192.168.1.255`

### 1.3 Host Addresses (The Usable Interface IPs)
- **Definition:** The contiguous range of addresses **between** the Network and Broadcast addresses.
- **Rule:** Valid, routable, and fully assignable.
- **Purpose:** Assigned to network endpoints — PCs, mobile devices, printers, servers, and router interfaces (default gateways) — for direct communication.
- **Example (`192.168.1.0/24`):** `192.168.1.1` – `192.168.1.254`

---

## 2. Classful vs. Classless Addressing

### 2.1 Classful Networking
The internet's original addressing scheme grouped IP space into fixed classes with immutable default masks:

| Class | Default Mask | Prefix | Usable Hosts |
|:-----:|:-------------|:------:|--------------:|
| A | `255.0.0.0`       | `/8`  | 16,777,214 |
| B | `255.255.0.0`     | `/16` | 65,534 |
| C | `255.255.255.0`   | `/24` | 254 |

> ⚠️ **The Depletion Problem:** This rigid model wasted huge blocks of address space. An organization needing 500 addresses couldn't fit in a Class C (max 254), so it was forced into a Class B — leaving over 65,000 addresses reserved but unused.

### 2.2 Classless Networking (CIDR)
Classless Inter-Domain Routing (CIDR) replaced fixed class boundaries with a flexible, bit-level subnet mask (`/25`, `/26`, `/29`, etc.), which:
- Removes fixed-boundary requirements, letting the mask be sized to match actual need.
- Forms the foundation of **subnetting** — dividing a block into smaller, isolated, right-sized broadcast domains.

---

## 3. End-to-End Packet Flow: Residential Internet Access

When an internal host (e.g., a phone on a home LAN) requests an external resource (e.g., `google.com`), Layer 2 and Layer 3 work together to translate and route the traffic:

```text
 [ Private Host ] ------------> [ Home Router (CPE) ] ------------> [ ISP Edge Router ] ------------> [ Google Web Server ]
  192.168.1.5/24                  (LAN) 192.168.1.1                   (Prefix: 39.40.50.0/24)             (Public Server Target)
                                  (WAN) 39.40.50.1 (Public Host)
                                         |
 |____ Local Broadcast Domain ____|      |_________________________ Core Internet Routing _________________________|
   - Matched against subnet mask          - NAT translates private → public IP   - Routes on the destination network prefix
   - MAC resolved via local ARP           - Router acts as a single WAN host     - Delivers to the exact public host
```

**Step-by-step:**
1. **Local ARP resolution:** The host checks if the destination is local (via its subnet mask). Since Google is external, it ARPs for its default gateway's MAC address instead.
2. **NAT translation:** The home router rewrites the packet's private source IP (`192.168.1.5`) to its public WAN IP (`39.40.50.1`) and tracks the mapping in its NAT table.
3. **Core routing:** ISP and upstream routers forward the packet using only the destination network prefix — they don't need to know about the private LAN behind it.
4. **Return traffic:** The response comes back to the router's public IP, which consults its NAT table to forward it to the correct internal host.
