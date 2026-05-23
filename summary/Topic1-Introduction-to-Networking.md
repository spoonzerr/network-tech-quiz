# Topic 1: Introduction to Networking

---

## 1. What is a Bit? What is a Byte?

Everything a computer does — storing files, sending messages, playing videos — comes down to **binary digits**: `0` and `1`. These are called **bits**.

Think of a bit like a light switch: it's either **OFF (0)** or **ON (1)**. That's it. Just two states.

A **byte** is a group of **8 bits**. Each letter, number, or symbol you type is stored as one byte using a system called **ASCII**:

| Character | Binary (8 bits) |
|-----------|----------------|
| A         | 01000001        |
| 9         | 00111001        |
| #         | 00100011        |

> **Plain English:** Your computer only speaks in 0s and 1s. A bit is one digit; a byte is 8 digits grouped together. Everything you see on screen — text, images, video — is secretly just a huge stream of bits.

---

## 2. How Data Travels Across a Network

Once data is turned into bits, those bits need to get from one device to another. They travel as **signals** through a **medium** (the physical path). There are three types of signals:

| Signal Type | Medium | How it works |
|-------------|--------|--------------|
| **Electrical** | Copper wire (cable) | Bits represented as electrical pulses |
| **Optical** | Fiber-optic cable | Bits converted into pulses of light |
| **Wireless** | Air | Bits encoded into radio waves or microwaves |

Signals may be converted multiple times on their journey — for example, from wireless to electrical to optical — before reaching the destination.

---

## 3. Bandwidth vs. Throughput

These two terms are easy to confuse:

| Term | What it means | Analogy |
|------|---------------|---------|
| **Bandwidth** | The *maximum* capacity of a connection (theoretical) | The width of a highway — how many lanes it has |
| **Throughput** | The *actual* speed you get (real-world) | How many cars are actually moving on that highway right now |

**Common bandwidth units:**

| Unit | Abbreviation | Size |
|------|-------------|------|
| Kilobits per second | Kbps | 1,000 bits/sec |
| Megabits per second | Mbps | 1,000,000 bits/sec |
| Gigabits per second | Gbps | 1,000,000,000 bits/sec |
| Terabits per second | Tbps | 1,000,000,000,000 bits/sec |

**Why is throughput lower than bandwidth?**
- Amount of data being sent at once
- Types of data (video uses more than text)
- **Latency** — delays caused by every device the data passes through
- Slowest link rule: throughput is limited by the **slowest segment** in the entire path

> **Example:** Your ISP advertises 1 Gbps, but your speed test shows 400 Mbps. That's because bandwidth is the ceiling; throughput is what you actually get after latency, congestion, and other factors.

---

## 4. Network Components

Every network is built from three types of hardware:

### End Devices
Devices that **send or receive** data — they are the starting and ending point of communication.
- Examples: PC, laptop, smartphone, IP phone, printer, file server

### Intermediary Devices
Devices that **connect and manage** the flow of data between end devices.
- Examples: Switch, Router, Wireless Access Point, Firewall
- Their jobs:
  - Regenerate and retransmit signals
  - Know the paths available in the network
  - Notify other devices of errors

### Network Media
The **physical path** data travels through.
- Copper wire → electrical impulses
- Fiber-optic cable → light pulses
- Wireless → electromagnetic waves

---

## 5. Network Types

Networks come in different sizes:

| Type | Description | Example |
|------|-------------|---------|
| **Small Home Network** | A few devices connected at home | Home Wi-Fi |
| **SOHO** (Small Office/Home Office) | Remote workers connecting to a corporate network | Working from home |
| **LAN** (Local Area Network) | Devices connected in a small area (one building) | School computer lab |
| **WAN** (Wide Area Network) | Connects multiple LANs across large distances | Corporate offices in different cities |
| **Internet** | Worldwide collection of interconnected LANs and WANs | The internet |

### LAN vs WAN at a glance:

| | LAN | WAN |
|-|-----|-----|
| Area covered | Small (building/campus) | Large (cities/countries) |
| Administered by | One organisation | Multiple service providers |
| Speed | High (fast) | Slower between LANs |

### The Internet
- Not owned by any one person or company
- Maintained by standards bodies: **IETF**, **ICANN**, **IAB**
- LANs connect to each other via WANs; WANs use fiber, copper, and wireless

---

## 6. ISP Connectivity

An **Internet Service Provider (ISP)** is the company that gives you access to the internet.

**Two ways to connect:**

| Option | How it works | Security |
|--------|-------------|----------|
| **Modem only** (direct connection) | Single PC plugs straight into modem | **Not secure** — your PC is exposed directly to the internet |
| **Router + Modem** (integrated router) | Router sits between your devices and the modem | **Secure** — router provides IP addressing, firewall, and Wi-Fi |

ISPs are connected to each other in a **hierarchy** — traffic takes the shortest path from source to destination. The backbone of the internet uses **fiber-optic cables** buried underground and under the sea.

---

## 7. Reliable Networks — The Four Pillars

A good network must meet four key characteristics:

### Fault Tolerance
- A network that keeps working even when something breaks
- Uses **packet switching**: data is broken into packets that can take different routes
- If one path fails, packets take another → no single point of failure
- Contrast: **circuit switching** creates a single dedicated path — if it breaks, the whole connection drops

### Scalability
- The network can grow (add new users/devices) **without slowing down** for everyone else
- Achieved by following standard protocols and designs

### Quality of Service (QoS)
- Prioritises important traffic (like video calls and voice) over less urgent traffic (like downloads)
- Without QoS: video calls break up when someone else starts downloading a large file
- With QoS: the router manages traffic flow to keep critical services smooth

### Security
Two areas of concern:

| Area | What it protects |
|------|-----------------|
| **Infrastructure security** | Physical devices — preventing unauthorised access to routers/switches |
| **Information security** | The data itself as it travels across the network |

Three goals of network security (CIA):
- **Confidentiality** — only the intended recipient can read the data
- **Integrity** — data is not altered during transmission
- **Availability** — authorised users can access data when needed
