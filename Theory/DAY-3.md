# 🌐 CCNA 200-301: Learning Journey

![CCNA Badge](https://img.shields.io/badge/Certification-CCNA%20200--301-blue?style=for-the-badge&logo=cisco)
![Day](https://img.shields.io/badge/Progress-Day%2002-brightgreen?style=for-the-badge)

## 📌 Day 02:IPv4 Addressing, Subnetting & Network Architecture


 IPv4 Addressing, Subnetting & Network Architecture

This repository contains comprehensive, highly structured study notes for **CCNA Day 3**. It serves as a professional reference guide covering IPv4 structures, classful addressing, public vs. private ranges, MAC and IP routing behaviors across network boundaries, subnet masking with slash (CIDR) notation, and practical binary calculations.

---

## 1. Introduction to IPv4 & Classful Addressing
IPv4 (Internet Protocol Version 4) is a **32-bit logical address** represented in dotted-decimal format, split into 4 octets (8 bits each).

$$\text{Total Address Space} = 2^{32} \approx 4,294,967,296 \text{ Addresses}$$

Historically, the address space was managed through **Classful Addressing**:

### Classful Breakdown Table
| Class | First Octet Range (Decimal) | Default Subnet Mask | Prefix Notation | Network/Host Bits | Number of Networks | Usable Hosts per Network |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Class A** | $1 - 126$ ($0$ and $127$ reserved) | $255.0.0.0$ | `/8` | $8 \text{ Net} / 24 \text{ Host}$ | $126$ ($2^7 - 2$) | $16,777,214$ ($2^{24} - 2$) |
| **Class B** | $128 - 191$ | $255.255.0.0$ | `/16` | $16 \text{ Net} / 16 \text{ Host}$ | $16,384$ ($2^{14}$) | $65,534$ ($2^{16} - 2$) |
| **Class C** | $192 - 223$ | $255.255.255.0$ | `/24` | $24 \text{ Net} / 8 \text{ Host}$ | $2,097,152$ ($2^{21}$) | $254$ ($2^8 - 2$) |
| **Class D** | $224 - 239$ | *N/A (Multicast)* | *N/A* | *N/A* | *N/A* | *Reserved for Multicasting* |
| **Class E** | $240 - 255$ | *N/A (Experimental)*| *N/A* | *N/A* | *N/A* | *Reserved for Research* |

### Core Mathematical Formulas
* **Usable Hosts on a Subnet:** $2^{H} - 2$ (where $H$ represents the number of host bits). We subtract $2$ because:
  1. The **first address** is the **Network ID** (all host bits are `0`).
  2. The **last address** is the **Broadcast IP** (all host bits are `1`).
* **Number of Subnets:** $2^{N}$ (where $N$ is the number of borrowed subnet bits).

---

## 2. Public vs. Private IP Addresses
To prevent the rapid depletion of IPv4 addresses, the IP space is bifurcated into Public and Private scopes.

### Comparison Table
| Feature | Private IP Addresses | Public IP Addresses |
| :--- | :--- | :--- |
| **Routing Scope** | Local Area Network (LAN) only; non-routable over the public internet. | Global Area Network (WAN); fully routable across the global internet. |
| **Uniqueness** | Must be unique *within* the local LAN, but can be reused across millions of external networks. | Globally unique. No two devices online can share the same public IP simultaneously. |
| **Allocation & Cost** | Free to use on internal networks without registration. | Registered and leased through ISPs (allocated globally by IANA/RIRs). |
| **Access Method**| Accesses the internet through **NAT (Network Address Translation)** on a gateway router. | Directly reachable from any device connected to the internet. |

---

## 3. IANA-Reserved Private IPv4 Addresses (RFC 1918)
The **Internet Assigned Numbers Authority (IANA)** reserved specific address blocks for private local networks under **RFC 1918**:

* **Class A Range:** `10.0.0.0` to `10.255.255.255` (`10.0.0.0/8`) | Total IPs: $16,777,216$
* **Class B Range:** `172.16.0.0` to `172.31.255.255` (`172.16.0.0/12`) | Total IPs: $1,048,576$
* **Class C Range:** `192.168.0.0` to `192.168.255.255` (`192.168.0.0/16`) | Total IPs: $65,536$

---

## 4. MAC vs. IP Address Roles (LAN vs. Internet)
Understanding how Layer 2 (MAC) and Layer 3 (IP) headers interact across different network boundaries is crucial.

```text
 [ Host A ] ------------> ( Local Switch ) ------------> [ Router (Gateway) ] ------------> ( Internet / ISP ) ------------> [ Target Server ]
 (IP: 192.168.1.10)        (Layer 2 MAC Transit)         (S: 192.168.1.1 | WAN Public)                                     (IP: 8.8.8.8)
 
 |_________________ Local LAN Segment _________________| |___________________________ Global WAN Segment ___________________________|
  - Envelopes packet with Switch MAC                      - Strips Layer 2 Header
  - Direct delivery via ARP                               - Modifies MAC Hop-by-Hop (IP stays constant)
```

### Behavior Inside the LAN
Layer 2 switches forward frames purely by **MAC address**. When Host A knows a destination IP but not its MAC, it triggers **ARP (Address Resolution Protocol)**:

1. Host A broadcasts: *"Who has 192.168.1.20? Tell 192.168.1.10."*
2. Host B replies directly (unicast) with its MAC address.
3. Host A caches the mapping in its **ARP table** and forwards the frame.

### Behavior Across the Internet
* The **IP address** (source and destination) remains **constant end-to-end** — it never changes for the life of the packet's journey.
* The **MAC address** is **rewritten at every Layer 3 hop**. Each router strips the old Layer 2 header and re-encapsulates the frame with its own outbound interface MAC as the new source, and the next hop's MAC as the new destination.

$$\text{IP}_{\text{src/dst}} = \text{constant} \qquad \text{MAC}_{\text{src/dst}} = f(\text{hop}_n)$$

---

## 5. Subnet Masking, Slash Notation & Bitwise ANDing
A **subnet mask** marks which bits of an IP address belong to the **Network ID** versus the **Host ID**, using a contiguous block of binary `1`s followed by `0`s.

### Slash (CIDR) Notation Reference
| Slash | Binary Mask | Decimal Mask |
| :---: | :--- | :--- |
| `/8` | `11111111.00000000.00000000.00000000` | $255.0.0.0$ |
| `/16` | `11111111.11111111.00000000.00000000` | $255.255.0.0$ |
| `/24` | `11111111.11111111.11111111.00000000` | $255.255.255.0$ |
| `/25` | `11111111.11111111.11111111.10000000` | $255.255.255.128$ |

### Worked Example: Bitwise AND Calculation
**Scenario:** Does `192.168.1.10/24` share a network with `192.168.1.20`?

A host determines this by performing a **logical AND** between each IP and the subnet mask, then comparing the resulting Network IDs.

```text
   192.168.1.10   →   11000000.10101000.00000001.00001010
 AND  /24 Mask     →   11111111.11111111.11111111.00000000
 ─────────────────────────────────────────────────────────
   Network ID A    →   11000000.10101000.00000001.00000000  →  192.168.1.0

   192.168.1.20   →   11000000.10101000.00000001.00010100
 AND  /24 Mask     →   11111111.11111111.11111111.00000000
 ─────────────────────────────────────────────────────────
   Network ID B    →   11000000.10101000.00000001.00000000  →  192.168.1.0
```

$$\text{Network}_{A} = 192.168.1.0 = \text{Network}_{B}$$

**Conclusion:** Since both results match, the two hosts are on the **same network**. Host A delivers the frame directly via ARP, bypassing the default gateway entirely. If the results had differed, Host A would forward the traffic to its **default gateway** for inter-network routing.

---

## CCNA Day 3 Revision Prompt
Use the prompt below with an AI assistant to self-quiz on today's material:

```text
Act as a CCNA exam instructor. Quiz me on the following Day 3 topics one question 
at a time, waiting for my answer before revealing the correct one and explaining 
any mistakes:

1. IPv4 classful addressing (Class A/B/C/D/E ranges, default masks, prefix notation, 
   and the usable host formula 2^H - 2, including why we subtract 2).
2. Public vs Private IP addresses (routing scope, uniqueness, cost, NAT).
3. RFC 1918 private address ranges for Class A, B, and C.
4. The difference between MAC and IP address roles — inside a LAN (ARP, switching) 
   versus across the Internet (IP stays constant, MAC changes per hop).
5. Subnet masking, slash notation, and manually performing a bitwise AND operation 
   to determine if two hosts are on the same network or different networks.

Mix in a few binary math and bitwise ANDing practice problems, and rate my overall 
readiness for the CCNA exam on these topics at the end.
```
