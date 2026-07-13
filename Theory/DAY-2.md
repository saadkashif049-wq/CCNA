# 🌐 CCNA 200-301: Learning Journey

![CCNA Badge](https://img.shields.io/badge/Certification-CCNA%20200--301-blue?style=for-the-badge&logo=cisco)
![Day](https://img.shields.io/badge/Progress-Day%2002-brightgreen?style=for-the-badge)

## 📌 Day 02: Core Network Components & Devices

Today, I explored the physical and logical layers of networking hardware. Understanding how Hubs, Switches, Routers, and other foundational components process data is critical for proper network design and troubleshooting.

---

### 🎛️ Detailed Explanation of Core Network Components

#### 1. 📢 Hub (The Legacy Device)
* **OSI Layer:** Layer 1 (Physical Layer).
* **How it works:** A Hub is a non-intelligent device with no database. When it receives data on one port, it does not read any addresses; it simply duplicates the electrical signal and **broadcasts** it out of all other active ports.
* **Collision Domain:** Consists of a single large collision domain. If two devices transmit data at the same time, a data collision occurs.
* **Transmission Mode:** Half-Duplex (Devices cannot send and receive data at the same exact time).

#### 2. ⚡ Switch (The Smart LAN Controller)
* **OSI Layer:** Layer 2 (Data Link Layer).
* **How it works:** A Switch is an intelligent device that maintains a **MAC Address Table**. When a frame enters a port, the switch reads the Destination MAC address and forwards the data *only* to the specific port where that destination device is connected (**Unicast**).
* **Collision Domain:** Every single port on a switch represents its own separate collision domain. This completely eliminates data collisions.
* **Transmission Mode:** Full-Duplex (Devices can send and receive data simultaneously).

#### 3. 🗺️ Router (The Gateway to the Internet)
* **OSI Layer:** Layer 3 (Network Layer).
* **How it works:** A Router is the brain of inter-network communication. It reads **IP Addresses** instead of MAC addresses. It connects completely different local networks (LANs) together and maintains a **Routing Table** to determine the absolute best path for data packets to travel across the internet.
* **Broadcast Boundary:** Routers break up broadcast domains. They do not pass Layer 2 broadcasts from one network to another, preventing network congestion.

#### 4. 🪵 Other Critical Infrastructure Components
* **Wireless Access Point (WAP):** Acts as a wireless switch. It connects wireless devices (laptops, phones) to the wired local network via radio waves.
* **Firewall:** A dedicated security device that monitors and filters incoming and outgoing network traffic based on an organization's previously established security policies. It sits at the edge of the network to block unauthorized outside access.
* **Endpoint Devices:** The actual source or destination of network traffic (e.g., PCs, Servers, IP Phones, Printers).

---

### 🔄 Architectural Deep Dive: Key Differences

#### 1. ⚔️ Router vs. Switch
The fundamental difference lies in their operational scope and the layer of the OSI model they handle.

* **Layer & Logic:** Routers operate at **Layer 3 (Network)** using logical IP addresses. Switches operate at **Layer 2 (Data Link)** using physical MAC addresses.
* **Network Boundary:** A Switch works **inside** a single network (LAN) to connect individual endpoints together. A Router works **between** networks (WAN/Internet) to connect multiple separate LANs together.
* **Data Unit:** Routers process **Packets** (which contain IP headers). Switches process **Frames** (which contain MAC headers).

#### 2. ⚔️ Switch vs. Hub
The fundamental difference lies in intelligence, security, and bandwidth utilization.

* **Intelligence:** A Hub is "blind" and floods data everywhere. A Switch is "aware" and sends data explicitly to the targeted destination port.
* **Performance:** On a Hub, total bandwidth is shared among all connected devices, causing slower speeds. On a Switch, every connected device gets its own dedicated maximum bandwidth link.
* **Security:** Hubs are highly insecure because any device connected to a hub can intercept and read traffic meant for other computers. Switches isolate traffic to specific ports, securing local communication channels.

---

### 📊 Comparative Breakdown Table

| Feature | 📢 Hub | ⚡ Switch | 🗺️ Router |
| :--- | :--- | :--- | :--- |
| **OSI Layer** | Layer 1 (Physical) | Layer 2 (Data Link) | Layer 3 (Network) |
| **Addressing Used** | None (Electrical Signals) | MAC Address | IP Address |
| **Collision Domains** | 1 Shared Domain | 1 per Port (Isolated) | 1 per Port (Isolated) |
| **Broadcast Domains** | 1 Shared Domain | 1 Shared Domain | 1 per Port (Breaks Broadcasts) |
| **Device Purpose** | Connects a local segment | Connects devices inside LAN | Connects different networks |
| **Traffic Type** | Always Broadcasts | Unicast, Multicast, Broadcast | Unicast, Multicast |

> ⚠️ **Important Interview Insight:** If a switch does not have a destination MAC address inside its MAC Address Table yet, it will temporarily act like a Hub by flooding the frame out of all ports except the source port. This process is known as **Unknown Unicast Flooding**.
