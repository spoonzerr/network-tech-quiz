# Topic 2: Communication & Protocols

---

## 1. Why Protocols Exist

Imagine two people trying to have a conversation — one speaks only English, the other only Mandarin. Without a shared language and rules, communication fails.

Networks face the same problem. **Protocols** are the agreed-upon rules that let devices communicate reliably, regardless of who made them.

Before any communication can happen, devices must agree on:
- **What method to use** (wired? wireless? which type?)
- **What language/format** (how data is structured)
- **Whether to confirm receipt** (does the sender need acknowledgment?)

---

## 2. Protocol Requirements

Every network protocol must define these five things:

| Requirement | What it controls |
|-------------|-----------------|
| **Message Encoding** | Converting data into a transmittable format (and back again) |
| **Message Formatting & Encapsulation** | The specific structure/wrapper a message must have |
| **Message Size** | Maximum size of each piece sent — long messages are broken into smaller chunks |
| **Message Timing** | Flow control, response timeouts, and access methods |
| **Message Delivery Options** | How many recipients get the message |

### Message Timing in detail:
- **Flow Control** — controls how fast data is sent so the receiver isn't overwhelmed
- **Response Timeout** — how long a sender waits before assuming the message was lost
- **Access Method** — determines when a device is allowed to send (prevents collisions — when two devices send at the same time and corrupt each other's data)

---

## 3. Message Delivery Options

| Mode | Meaning | Example |
|------|---------|---------|
| **Unicast** | One sender → one specific receiver | Sending an email to one person |
| **Multicast** | One sender → a specific group (not all) | Streaming to subscribers of a channel |
| **Broadcast** | One sender → all devices on the network | A fire alarm announcement (IPv4 only — IPv6 does not use broadcast) |

> **Note:** IPv6 uses **Anycast** instead of broadcast — a message is delivered to the nearest device in a group.

---

## 4. The TCP/IP Model (4 Layers)

The **TCP/IP model** is the practical model used by the internet. Think of it as a recipe for how data is handled at each stage of communication.

| Layer | Name | What it does (plain English) |
|-------|------|------------------------------|
| 4 | **Application** | Talks directly to the user's app; formats data for display (e.g. web browser, email) |
| 3 | **Transport** | Breaks data into manageable pieces; ensures reliable delivery between devices |
| 2 | **Internet** | Figures out the best route to get data to the destination (IP addresses live here) |
| 1 | **Network Access** | Controls the actual hardware — cables, Wi-Fi cards, switches — that physically sends data |

> **Memory trick:** "**A**ll **T**raffic **I**s **N**etworked" → Application, Transport, Internet, Network Access

---

## 5. The OSI Model (7 Layers)

The **OSI (Open Systems Interconnection) model** is a *reference model* — a more detailed framework used for understanding and troubleshooting networks. It doesn't match a specific protocol; it describes what needs to happen.

| Layer | Name | What it does (plain English) |
|-------|------|------------------------------|
| 7 | **Application** | The interface between the network and the app (HTTP, FTP, DNS) |
| 6 | **Presentation** | Translates, encrypts, or compresses data so both sides understand it |
| 5 | **Session** | Opens, manages, and closes conversations between devices |
| 4 | **Transport** | Segments data; ensures complete, in-order delivery (TCP/UDP) |
| 3 | **Network** | Routes data between different networks using IP addresses |
| 2 | **Data Link** | Handles data transfer between two directly connected devices using MAC addresses |
| 1 | **Physical** | The actual hardware — cables, signals, electrical pulses |

> **Memory trick (top → bottom):** "**A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing"

---

## 6. OSI vs. TCP/IP — How They Map Together

| OSI Layer | TCP/IP Layer |
|-----------|-------------|
| Application (7) | Application |
| Presentation (6) | Application |
| Session (5) | Application |
| Transport (4) | Transport |
| Network (3) | Internet |
| Data Link (2) | Network Access |
| Physical (1) | Network Access |

The TCP/IP model is simpler (4 layers vs 7) because it combines some OSI layers. Both describe the same underlying processes — OSI just breaks them down more granularly.

---

## 7. Data Encapsulation & PDUs

As data travels **down** through the model layers (from the application to the physical cable), each layer **wraps** the data with its own header — like putting a letter inside an envelope, then putting that envelope in a box. This is called **encapsulation**.

**Going down the stack (sending):**

```
Data (what the app wants to send)
  ↓ Transport layer adds header → Segment
  ↓ Internet layer adds header  → Packet
  ↓ Data Link adds header/trailer → Frame
  ↓ Physical layer converts      → Bits (sent over wire/air)
```

Each of these — Data, Segment, Packet, Frame, Bits — is called a **PDU (Protocol Data Unit)**.

**Going up the stack (receiving — de-encapsulation):**

```
Bits received from the wire
  ↑ → Frame (Data Link strips its header)
  ↑ → Packet (Network layer strips its header)
  ↑ → Segment (Transport layer strips its header)
  ↑ → Data (delivered to the application)
```

> **Analogy:** Encapsulation is like sending a parcel. Your message → envelope → box → shipping label. The receiver unpacks in reverse order.

---

## 8. IP Addresses vs. MAC Addresses

There are two types of addresses used to deliver data — they work at different layers and do different jobs:

| | IP Address | MAC Address |
|-|------------|------------|
| **Layer** | Layer 3 (Network / Internet) | Layer 2 (Data Link) |
| **Purpose** | Identifies the **final destination** anywhere on the internet | Identifies the **next hop** on the current local network |
| **Scope** | Global — stays the same end-to-end | Local — changes at every router hop |
| **Example** | 192.168.1.110 | AA-AA-AA-AA-AA-AA |
| **Assigned by** | Router (DHCP) or manually configured | Hardwired into the network card (NIC) by the manufacturer |

### IP Address Structure

An IP address has two parts:
- **Network portion** — identifies which network the device belongs to (same for all devices on a LAN)
- **Host portion** — identifies the specific device within that network (unique per device)

Example: `192.168.1.110`
- `192.168.1` = network portion
- `110` = host portion

---

## 9. The Default Gateway — Your "Door to the World"

When a device wants to send data to another device **on the same network**, it uses MAC addresses directly.

When the destination is on a **different network** (e.g. a website on the internet), the device doesn't know how to get there directly. Instead, it sends the data to the **Default Gateway** — which is the router's IP address on the local network. The router then takes responsibility for forwarding the data toward its final destination.

```
Same network:    PC → Switch → Destination (MAC address used)
Different network: PC → Router (default gateway) → Internet → Destination
```

**Key rule:** The IP address (Layer 3) stays the same for the entire journey. The MAC address (Layer 2) **changes at every router hop** because it only applies to the current link.
