# Topic 3: Physical Layer

---

## 1. What is the Physical Layer?

The **Physical Layer** is Layer 1 — the foundation of all networking. It deals with the actual, physical transmission of raw bits across a medium (cable, fiber, or air).

Its job: take a complete **frame** from the Data Link layer above it, convert it into **signals** (electrical, light, or radio), and send those signals out onto the medium.

Before any communication can happen, a **physical connection** must exist — either wired or wireless. The device that connects you to the network is called a **NIC (Network Interface Card)**.

---

## 2. The Three Physical Layer Standards Areas

The Physical Layer is defined by three things:

| Area | What it covers |
|------|---------------|
| **Physical Components** | The hardware — NICs, cables, connectors, ports |
| **Encoding** | How bits are converted into a recognisable pattern before sending |
| **Signalling** | How 1s and 0s are actually represented on the medium (voltage, light pulse, radio wave) |

### Encoding vs. Signalling — what's the difference?

- **Encoding** = translating the raw bitstream into a structured pattern so the receiver can recognise where bits start and end. Examples: Manchester encoding, 4B/5B, 8B/10B.
- **Signalling** = the physical representation of those bits on the medium:
  - Copper cable → changes in **electrical voltage**
  - Fiber-optic → pulses of **light**
  - Wireless → **microwave/radio waves**

> **Analogy:** Encoding is like morse code (the pattern system). Signalling is whether you transmit it with sound, light flashes, or flags.

---

## 3. The Three Media Types

Modern networks use three types of physical media:

| Media | Signal Type | Key Characteristic |
|-------|------------|-------------------|
| **Metal wires (copper cable)** | Electrical impulses | Cheap, common, short-to-medium distance |
| **Glass/plastic fiber (fiber-optic)** | Pulses of light | Very fast, very long distances, immune to interference |
| **Wireless (air)** | Electromagnetic waves (radio/microwave) | No cables needed, but limited range and vulnerable to interference |

### Choosing the right media — four questions to ask:
1. What is the **maximum distance** it needs to cover?
2. What is the **environment** (indoors? outdoors? near electrical machinery?)
3. How much **data** needs to be sent, and how fast?
4. What is the **cost** of the media and installation?

---

## 4. Twisted-Pair Cable (Copper)

The most common network cable. Ethernet networks almost always use it.

**How it works:** Wires are grouped in **pairs** and **twisted together**. The twisting cancels out electromagnetic interference (EMI) — each wire in a pair picks up the same interference, and since they carry opposite signals, the interference cancels out when the signal is read.

- Each pair is colour-coded so you can identify both ends
- One wire is a solid colour; its partner has the same colour striped on white

**Types:** UTP (Unshielded Twisted Pair) is the most common for LANs.

---

## 5. Fiber-Optic Cable

Fiber uses **light** instead of electricity. Because it's light-based, **electrical interference has no effect on it**.

Key uses:
- Backbone networks (connecting buildings or data centres)
- Long-distance links (undersea cables, city-to-city)
- High-bandwidth environments (large data centres, hospitals)

### Fiber vs. Copper — Comparison Table

| Feature | UTP (Copper) | Fiber-Optic |
|---------|-------------|-------------|
| **Bandwidth** | 10 Mb/s – 10 Gb/s | 10 Mb/s – 100 Gb/s |
| **Distance** | 1 – 100 metres | 1 – 100,000 metres |
| **EMI/RFI immunity** | Low | High (completely immune) |
| **Electrical hazard immunity** | Low | High (completely immune) |
| **Media & connector cost** | Lowest | Highest |
| **Installation skill needed** | Lowest | Highest |
| **Safety precautions** | Lowest | Highest |

> **Summary:** Fiber wins on performance and distance; copper wins on cost and ease of installation.

---

## 6. Wireless Media

Wireless transmits data using **electromagnetic waves** (radio or microwave frequencies) through the air. No cables needed — great for mobility.

### Limitations of Wireless:

| Limitation | What it means |
|-----------|--------------|
| **Coverage area** | Physical obstacles (walls, metal, machinery) reduce range and signal quality |
| **Interference** | Other wireless devices (microwaves, baby monitors, neighbouring Wi-Fi) can disrupt the signal |
| **Security** | Anyone within range can potentially intercept the signal — no physical barrier |
| **Shared medium / half-duplex** | Only **one device** can send or receive at a time on the same channel; more users = less bandwidth each |

---

## 7. Wireless Standards

| Standard | IEEE Spec | Technology | Primary Use |
|----------|-----------|-----------|-------------|
| **Wi-Fi** | 802.11 | WLAN | General wireless networking (home, office) |
| **Bluetooth** | 802.15 | WPAN | Short-range personal devices (headphones, keyboards) |
| **WiMAX** | 802.16 | Point-to-multipoint | Broadband wireless over longer distances |
| **Zigbee** | 802.15.4 | Low-power WPAN | IoT devices (smart home sensors, industrial) |

---

## 8. Setting Up a Wireless LAN (WLAN)

To set up a WLAN, you need two things:

| Device | Role |
|--------|------|
| **Wireless Access Point (AP)** | Collects wireless signals from all connected devices and connects them to the wired network |
| **Wireless NIC Adapter** | Installed in each device (laptop, PC) to give it wireless capability |

**Security note:** WLANs are inherently more vulnerable than wired networks. Network administrators must apply strict security policies (encryption, passwords, access control) to prevent unauthorised access.

When buying WLAN equipment, always check for **compatibility and interoperability** — devices must support the same 802.11 standard to work together.
