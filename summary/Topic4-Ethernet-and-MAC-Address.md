# Topic 4: Ethernet & MAC Addresses

---

## 1. The Data Link Layer — What it Does

The **Data Link Layer (Layer 2)** sits between the Physical Layer (cables/signals) and the Network Layer (IP addresses). Its job is to handle communication between directly connected devices on the same network segment.

Key responsibilities:
- Allows upper-layer protocols to access the physical medium
- Encapsulates Layer 3 packets (IPv4/IPv6) into **frames** for transmission
- Performs **error detection** and discards corrupt frames
- Controls **media access** (who gets to transmit and when)

> **Analogy:** Think of Layer 2 as the postal service for a single city block — it handles local delivery. Once a parcel leaves the block and enters the national system, Layer 3 (IP routing) takes over.

---

## 2. The Two Sublayers of the Data Link Layer

The IEEE divides Layer 2 into two sublayers:

| Sublayer | Full Name | What it does |
|----------|-----------|--------------|
| **LLC** | Logical Link Control | Communicates with Layer 3 above — identifies which network protocol (IPv4, IPv6) is being carried |
| **MAC** | Media Access Control | Handles frame encapsulation, physical addressing, and controls access to the shared medium |

---

## 3. Ethernet Frame Structure

Every Ethernet frame has the same structure — three main sections: **Header**, **Data**, and **Trailer**.

| Field | Size | Purpose |
|-------|------|---------|
| **Preamble** | 8 bytes | Synchronises the receiver's clock before the frame arrives (not shown in Wireshark) |
| **Destination MAC Address** | 6 bytes | MAC address of the receiving device (or broadcast/multicast) |
| **Source MAC Address** | 6 bytes | MAC address of the sending device (always unicast) |
| **Frame Type (EtherType)** | 2 bytes | Identifies the Layer 3 protocol in the payload (e.g. 0x0800 = IPv4, 0x0806 = ARP) |
| **Data (Payload)** | 46–1500 bytes | The encapsulated Layer 3 packet |
| **FCS (Frame Check Sequence)** | 4 bytes | Error detection — the receiver recalculates this to verify the frame arrived intact |

> **Key rule:** The source MAC address is **always unicast**. The destination can be unicast, broadcast, or multicast.

---

## 4. MAC Addresses

### What is a MAC Address?
A **MAC (Media Access Control) address** is the Layer 2 physical address hardwired into every NIC by the manufacturer. It uniquely identifies a device on a local network.

- **48 bits** long = **6 bytes** = **12 hexadecimal digits**
- Example: `F0-1F-AF-50-FD-C8`

### OUI — The Manufacturer Code

A MAC address is split into two halves:

| Portion | Length | Identifies |
|---------|--------|-----------|
| **OUI (Organizationally Unique Identifier)** | First 3 bytes (6 hex digits) | The **manufacturer** (e.g. Intel, Dell, Apple) — assigned by IEEE |
| **Vendor-Assigned** | Last 3 bytes (6 hex digits) | The **specific NIC** — assigned by the manufacturer |

> Example: `F0-1F-AF` is Intel's OUI; `50-FD-C8` is the device serial number.

### Hexadecimal Notation

MAC addresses use **hexadecimal (base 16)**:
- Each byte (8 bits) is shown as two hex digits: `00` to `FF`
- Leading zeroes are always shown: binary `0000 1010` → hex `0A`
- Hex values are often written with a `0x` prefix (e.g. `0x0A`) or with an `H` suffix (e.g. `0AH`)

---

## 5. Three Types of MAC Address Delivery

| Type | Destination MAC | Who receives it |
|------|----------------|-----------------|
| **Unicast** | Specific device's MAC | One device only |
| **Broadcast** | `FF-FF-FF-FF-FF-FF` | All devices on the local network |
| **Multicast** | `01-00-5E-xx-xx-xx` (IPv4) or `33-33-xx-xx-xx-xx` (IPv6) | A specific group of devices |

### Key Rules:
- **Broadcast** frames are flooded to all switch ports except the incoming one — **not forwarded by routers**
- **Multicast** frames are flooded similarly unless the switch uses **multicast snooping**
- The **source** MAC address is **always unicast** — a device cannot claim a broadcast/multicast address as its source

---

## 6. ARP — Resolving IP to MAC

When a device knows the destination **IP address** but needs the destination **MAC address** for the frame, it uses:

| Protocol | Used for |
|----------|----------|
| **ARP (Address Resolution Protocol)** | Finding the MAC address for a known **IPv4** address |
| **ND (Neighbor Discovery)** | Finding the MAC address for a known **IPv6** address |

**How ARP works:**
1. Device sends a **broadcast** ARP request: "Who has IP 192.168.1.1? Tell me your MAC."
2. The device with that IP replies with a **unicast** ARP reply containing its MAC address.
3. The sender caches this result in its **ARP table** to avoid asking again.

> **Why does the first ping always trigger an ARP?** Before sending any frame, the device must know the destination MAC. If it's not in the ARP cache, it broadcasts first.

---

## 7. Frame Processing by a NIC

When an Ethernet frame arrives at a NIC:
1. The NIC reads the **destination MAC address**
2. If it matches the NIC's own MAC, the device **accepts** the frame and passes it up the stack
3. If it **doesn't match**, the frame is **discarded**
4. Exception: the NIC also accepts **broadcast** frames and **multicast** frames for groups it has joined

At each router hop along a path:
1. Router **accepts** the incoming frame
2. **De-encapsulates** it to extract the IP packet
3. **Re-encapsulates** the packet into a new frame (with new source/destination MACs for the next link)
4. **Forwards** the new frame on the next interface

> **Key insight:** The **IP address** never changes hop-to-hop. The **MAC address** changes at every router.

---

## 8. Network Topologies

### Physical vs Logical Topology

| Type | What it shows |
|------|--------------|
| **Physical topology** | How devices are physically connected — cables, ports, actual layout |
| **Logical topology** | How data flows logically — virtual connections, IP addressing |

### WAN Topologies

| Topology | Description |
|----------|-------------|
| **Point-to-point** | Simplest — a direct permanent link between two endpoints |
| **Hub and spoke** | A central site connects to branch sites via point-to-point links (star-like) |
| **Mesh** | Every site connects to every other — maximum redundancy, high cost |

### LAN Topologies

| Topology | Description |
|----------|-------------|
| **Star** | All devices connect to a central switch — most common modern LAN topology |
| **Extended star** | Multiple switches connected in a hierarchy |
| **Bus** | All devices on a single cable (legacy — one break kills the whole segment) |
| **Ring** | Devices form a closed loop (legacy Token Ring) |

---

## 9. Half-Duplex vs Full-Duplex

| Mode | What it means | Where used |
|------|--------------|-----------|
| **Half-duplex** | Only one device can send OR receive at a time | WLANs (Wi-Fi), legacy hubs |
| **Full-duplex** | Both devices can send AND receive simultaneously | Modern Ethernet switches |

> **Analogy:** Half-duplex is like a walkie-talkie — you press to talk, release to listen. Full-duplex is like a phone call — both people can speak at once.

Modern Ethernet switches operate in **full-duplex**, which eliminates collisions and doubles effective throughput compared to half-duplex.

---

## 10. Using Wireshark to Examine Ethernet Frames

**Wireshark** is a free network protocol analyser (packet sniffer) that captures and displays live network traffic.

### Key Wireshark Concepts

| Concept | Detail |
|---------|--------|
| **Packet list pane** | Top section — lists every captured frame with summary info |
| **Packet details pane** | Middle section — shows the full decoded contents of the selected frame |
| **Packet bytes pane** | Bottom section — shows the raw hex and ASCII of the frame |
| **Display filter** | Filters what is *shown* (not what is captured). Example: type `icmp` to show only ping traffic |

### Common EtherType Values

| Hex value | Protocol |
|-----------|---------|
| `0x0800` | IPv4 |
| `0x0806` | ARP |
| `0x86DD` | IPv6 |

### What Wireshark Shows in an Ethernet Frame

When you click a frame in Wireshark:
- **Preamble** — not shown (processed by the NIC before the frame reaches the OS)
- **Destination MAC** — who the frame is addressed to
- **Source MAC** — who sent it
- **EtherType** — what's inside (IPv4, ARP, etc.)
- **Data** — the encapsulated Layer 3 packet
- **FCS** — usually not shown (verified and stripped by the NIC)

### Wireshark and ARP

When you ping a device for the first time:
1. Wireshark shows an **ARP Request** — broadcast (`FF:FF:FF:FF:FF:FF`) asking for the target's MAC
2. Then an **ARP Reply** — unicast, containing the target's MAC address
3. Then the actual **ICMP Echo Request/Reply** ping traffic

### Wireshark and Remote Traffic

When pinging a remote host (on a different network):
- **Destination MAC** = your **default gateway's MAC** (not the remote host's)
- **Destination IP** = the actual remote host's IP
- This is because Layer 2 only handles the local hop — the router takes it from there

---

## 11. Viewing NIC Information on Windows

### Using `ipconfig /all`
```
Physical Address. . . . . . . . . : F0-1F-AF-50-FD-C8   ← MAC address
IPv4 Address. . . . . . . . . . . : 192.168.1.147
Default Gateway . . . . . . . . . : 192.168.1.1
DHCP Enabled. . . . . . . . . . . : Yes
```

### Using the Network and Sharing Center (Windows)
- **Control Panel → Network and Sharing Center → Change adapter settings**
- Right-click a NIC → **Status** → **Details** to see MAC, IP, DHCP server, DNS servers
- Can enable/disable individual NICs from here

### Using the System Tray
- Click the network icon → shows available Wi-Fi SSIDs and connection status
- A crossed-out network icon = adapter disabled
- A warning (!) icon = adapter enabled but no connectivity

### Key NIC Information Fields

| Field | Meaning |
|-------|---------|
| **SSID** | Name of the Wi-Fi network you are connected to |
| **Physical Address** | The NIC's MAC address |
| **DHCP Enabled** | Whether the IP address is assigned automatically |
| **DNS Servers** | Multiple DNS servers listed = redundancy (if one fails, use the other) |
