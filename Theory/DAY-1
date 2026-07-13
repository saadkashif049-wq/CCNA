# 🌐 CCNA 200-301: Learning Journey

![CCNA Badge](https://img.shields.io/badge/Certification-CCNA%20200--301-blue?style=for-the-badge&logo=cisco)
![Day](https://img.shields.io/badge/Progress-Day%2001-brightgreen?style=for-the-badge)

## 📌 Day 01: Network Communication Modes & Addressing

Today, I built my core foundation on how data travels across a network and the distinct roles played by Layer 2 (Data Link) and Layer 3 (Network) addresses.

---

### 📡 Ways of Communication (Modes of Transmission)

There are three primary methods used to transmit data across a network topology:

1. **👤 Unicast (One-to-One)**
   - **Concept:** A single sender transmits data targeted exclusively to a single, specific receiver.
   - **Example:** Web browsing (Your PC requesting a page from a Google Server) or a private direct message.

2. **👥 Multicast (One-to-Many / Selective)**
   - **Concept:** A single sender transmits data to a specific, closed group of devices (subscribers) rather than the entire network.
   - **Example:** Video streaming, routing protocol updates (e.g., OSPF hello packets), or online multiplayer gaming lobbies.

3. **📢 Broadcast (One-to-All)**
   - **Concept:** A single device broadcasts data to **every single active device** within the local network segment. No local device can opt out of processing it.
   - **Example:** ARP requests (Address Resolution Protocol) or DHCP discovery packets when a PC requests an IP address.

---

### 🆔 Addressing Fundamentals: IP Address vs. MAC Address

To identify and deliver packets to a device, networks utilize two distinct types of addresses working at different layers:

#### 1. 🎛️ MAC Address (Media Access Control)
* **OSI Layer:** Layer 2 (Data Link Layer).
* **Nature:** This is the **Physical Address** hardcoded (burned-in) into the Network Interface Card (NIC) during manufacturing. It is permanent and unchangeable.
* **Format:** 48-bit hexadecimal format (e.g., `00:1A:2B:3C:4D:5E`).
* **Role:** Used exclusively for delivery **within the local network (LAN)** from one node to the next. It does not travel across internet routers.

#### 2. 🗺️ IP Address (Internet Protocol)
* **OSI Layer:** Layer 3 (Network Layer).
* **Nature:** This is a **Logical Address** assigned dynamically by a DHCP server or statically by a network administrator. It changes depending on the network the device is connected to.
* **Format:** 32-bit dotted-decimal format for IPv4 (e.g., `192.168.1.1`).
* **Role:** Responsible for **End-to-End Routing** and identifying devices globally across different interconnected networks.

---

### 🔄 Summary of Key Differences

| Feature | 🎛️ MAC Address | 🗺️ IP Address |
| :--- | :--- | :--- |
| **Alternative Name** | Physical / Hardware Address | Logical / Network Address |
| **OSI Layer** | Layer 2 (Data Link) | Layer 3 (Network) |
| **Scope** | Local Link Only (Inside the LAN) | Global (Across different networks/Internet) |
| **Device Analogy** | Like your Fingerprint (Unique & Permanent) | Like your Mailing Address (Changes if you move) |

> ⚠️ **Important Interview Insight:** Routers forward packets based on the **Destination IP Address** (Layer 3) to move data between networks, whereas Switches forward frames based on the **Destination MAC Address** (Layer 2) to deliver data within a single network. Both work in tandem to complete a network hop.
