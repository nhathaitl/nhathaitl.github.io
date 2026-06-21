---
title: "Wifi Reference"
date: 2026-06-21 10:00:00 +0700
categories: [Networking]
tags: [Wifi, Wireless]
---

## 1. History of WiFi

WiFi did not originate from the telecommunications industry. It grew out of government research, academic radio experiments, and a pivotal regulatory decision that opened unlicensed spectrum to public use.

| Year | Milestone |
|------|-----------|
| **1971** | **ALOHAnet** — University of Hawaii built the first packet-switched wireless network across islands using UHF radio. The ALOHA protocol it invented directly inspired Ethernet and WiFi's MAC layer. |
| **1985** | **FCC opens ISM bands** — The 900 MHz, 2.4 GHz, and 5.8 GHz bands are deregulated for unlicensed use, creating the legal foundation for WiFi. |
| **1991** | **NCR WaveLAN** — First commercial wireless LAN at 900 MHz, 1–2 Mbps. Vic Hayes, an NCR engineer who chaired the IEEE 802.11 committee, is later called the "father of WiFi." |
| **1997** | **IEEE 802.11 ratified** — The first standard: 2.4 GHz, up to 2 Mbps. Too slow for practical use, but it established the MAC protocol, frame format, and modulation framework all future generations build upon. |
| **1999** | **802.11b & the WiFi Alliance** — 802.11b reaches 11 Mbps. The Wireless Ethernet Compatibility Alliance is formed, later renamed the WiFi Alliance, which coins the brand name "WiFi" as a play on "Hi-Fi." |
| **2003–2009** | **802.11g and 802.11n** — 802.11g brings 54 Mbps to the popular 2.4 GHz band. 802.11n introduces MIMO antennas and channel bonding, pushing speeds to 600 Mbps and enabling dual-band operation. WiFi becomes a household utility. |
| **2013** | **WiFi 5 (802.11ac)** — Focuses on 5 GHz with MU-MIMO and wider channels, reaching theoretical 3.5 Gbps. |
| **2019–2021** | **WiFi 6 / 6E (802.11ax)** — Shifts philosophy from peak speed to efficient multi-device sharing via OFDMA. WiFi 6E opens the 6 GHz band. |
| **2024** | **WiFi 7 (802.11be)** — Introduces Multi-Link Operation (MLO), 320 MHz channels, and 4096-QAM. Theoretical throughput reaches 46 Gbps. |

---

## 2. How WiFi Works

### The Fundamental Principle

WiFi encodes data onto radio waves by modulating a property of the wave — its amplitude, phase, or frequency. The router's antenna generates an electromagnetic wave oscillating at billions of cycles per second; by varying that wave in defined ways, it encodes binary data. The receiving device measures those variations and decodes the bits.

The core tradeoff: higher frequency = more data capacity, but shorter range and weaker wall penetration.

### Modulation

**Quadrature Amplitude Modulation (QAM)** encodes data in both amplitude and phase simultaneously. The higher the QAM order, the more bits per symbol — and the stronger the signal must be to distinguish the states reliably.

| QAM Order | Bits per Symbol | Requirement |
|-----------|----------------|-------------|
| BPSK | 1 | Very weak signal tolerated |
| QPSK | 2 | — |
| 16-QAM | 4 | — |
| 64-QAM | 6 | — |
| 256-QAM | 8 | Good signal needed |
| 1024-QAM | 10 | Strong signal needed (WiFi 6) |
| 4096-QAM | 12 | Excellent signal required (WiFi 7 only) |

### OSI Model — Where WiFi Lives

WiFi operates at **Layers 1 and 2** only. Everything above is unaware of whether the link is wireless or wired.

| Layer | Name | Role |
|-------|------|------|
| 7 | Application | HTTP, DNS, TLS |
| 6 | Presentation | Encryption, encoding |
| 5 | Session | TCP sessions |
| 4 | Transport | TCP/UDP |
| 3 | Network | IP, routing |
| **2** | **Data Link (MAC)** | **WiFi — channel access, framing, ACKs** |
| **1** | **Physical (PHY)** | **WiFi — radio, modulation, antenna** |

### CSMA/CA — How Devices Share the Air

WiFi is a shared medium. The MAC layer uses **Carrier Sense Multiple Access with Collision Avoidance (CSMA/CA)**: before transmitting, a device listens to confirm the channel is idle, waits a random backoff interval, then transmits. If no acknowledgment is received (indicating a collision), it waits a longer random interval before retrying. This is analogous to polite conversation — you wait for a pause before speaking.

### Frame Types

Every WiFi transmission is a **frame** containing a MAC header (addresses, frame type, sequence number), a variable-length payload, and an FCS (Frame Check Sequence) for error detection. There are three frame types: management (handles connections), control (handles channel access), and data (carries the payload).

---

## 3. Frequency Bands

The core physical tradeoff: lower frequency = longer range, better wall penetration, less data capacity. Higher frequency = shorter range, absorbs into obstacles, but far more bandwidth available.

| Band | Range | Non-Overlapping Channels | Characteristics |
|------|-------|--------------------------|-----------------|
| **2.4 GHz** | Long | 3 (ch. 1, 6, 11) | Legacy-congested; shared with Bluetooth, microwaves; only 83.5 MHz total |
| **5 GHz** | Medium | 25 | Less crowded, widely supported; 802.11ac focused here entirely |
| **6 GHz** | Shorter | 59 | Opened in 2020 (WiFi 6E+); 1,200 MHz of clean spectrum; no legacy devices |
| **60 GHz** | Same room | Many | Used in WiFi 7 for ultra-high-speed short-range links |

### Channel Bonding

Channels can be bonded for greater throughput: 20 → 40 → 80 → 160 → **320 MHz** (WiFi 7). Wider channels consume more spectrum and are impractical in 2.4 GHz (the entire band is only 83.5 MHz), but routine in 5 GHz and especially 6 GHz.

### Why 2.4 GHz Is Congested

Only channels 1, 6, and 11 are non-overlapping. Every legacy WiFi device, Bluetooth radio, baby monitor, microwave oven, and cordless phone competes on the same 83.5 MHz of spectrum. In a dense apartment building, it can be nearly unusable.

---

## 4. WiFi Generations — 5, 6, and 7

### Comparison Table

| Specification | WiFi 5 (802.11ac) | WiFi 6/6E (802.11ax) | WiFi 7 (802.11be) |
|---|---|---|---|
| Year | 2013 | 2019 / 2021 | 2024 |
| Max Theoretical Speed | 3.5 Gbps | 9.6 Gbps | 46 Gbps |
| Bands | 5 GHz only | 2.4 + 5 (+ 6 GHz in 6E) | 2.4 + 5 + 6 GHz simultaneously |
| Max Channel Width | 160 MHz | 160 MHz | 320 MHz |
| Modulation | 256-QAM | 1024-QAM | 4096-QAM |
| Max Spatial Streams | 8 | 8 | 16 |
| MU-MIMO | Downlink only | DL + UL (8×8) | DL + UL (16×16) |
| OFDMA | ✗ | ✓ Key feature | ✓ Enhanced |
| Multi-Link Operation | ✗ | ✗ | ✓ Core feature |
| Target Wake Time (TWT) | ✗ | ✓ | ✓ Enhanced |
| BSS Coloring | ✗ | ✓ | ✓ |

### WiFi 5 (802.11ac)

WiFi 5 bet entirely on 5 GHz, where wider channels were available, and abandoned 2.4 GHz. Its headline feature was **downlink MU-MIMO** — an AP could transmit to up to 4 clients simultaneously using beamforming. Still a "one conversation at a time" model: MU-MIMO was downlink only, and only one client could talk to the AP at once.

### WiFi 6 / 6E (802.11ax)

WiFi 6 shifted the philosophy from raw peak speed to **efficient sharing**. Its defining innovation was **OFDMA** (borrowed from 4G/5G cellular), which divides channels into sub-carriers called Resource Units and allows an AP to serve multiple devices simultaneously in both directions. Combined with uplink MU-MIMO, BSS Coloring, and TWT, WiFi 6 transformed the AP from a queue manager into a traffic orchestrator. WiFi 6E then added the clean, uncrowded 6 GHz band.

### WiFi 7 (802.11be)

WiFi 7's defining innovation is **Multi-Link Operation (MLO)**. All prior WiFi generations connected to exactly one band at a time. MLO aggregates multiple bands and channels into a single logical connection, dynamically shifting traffic across 2.4, 5, and 6 GHz simultaneously based on congestion, interference, and latency. Combined with 320 MHz channels and 4096-QAM, WiFi 7 reaches 46 Gbps theoretically. More practically, MLO reduces latency variance dramatically — critical for VR, gaming, and real-time video.

---

## 5. Key Techniques & Concepts

### MIMO & Beamforming

**MIMO** (Multiple Input Multiple Output) uses multiple antennas to transmit several independent data streams through the same channel simultaneously (spatial multiplexing), or to send redundant copies for reliability (spatial diversity).

**Beamforming** adjusts the phase and amplitude of signals across antennas to focus RF energy toward the target device like a spotlight — improving range and signal quality while reducing interference to other devices.

### OFDM & OFDMA

**OFDM** divides a channel into many narrow, mathematically orthogonal sub-carriers. Each sub-carrier carries a modulated signal independently. Because they are orthogonal, they do not interfere with each other even when overlapping. This solves multipath fading elegantly — narrow sub-carriers experience flat fading rather than frequency-selective distortion.

**OFDMA** (WiFi 6+) assigns different sub-carriers to different users within the same transmission. A "Resource Unit" can be as small as 26 sub-carriers (~2 MHz). The AP scheduler assigns RUs based on traffic, device needs, and channel conditions — eliminating the "one device at a time" limitation entirely.

### WiFi Offloading

WiFi offloading routes mobile data traffic — traffic that would otherwise travel over 4G/5G — through WiFi access points instead. Mobile operators do this because WiFi uses unlicensed spectrum at no cost. Industry estimates suggest 50–70% of all smartphone data is carried over WiFi.

Key enabling technologies:
- **Hotspot 2.0 / Passpoint** — automatic, secure WiFi authentication without user interaction (like cellular roaming)
- **ANDSF** — Access Network Discovery and Selection Function; cellular network policies that tell devices when and how to offload
- **LTE-WLAN Aggregation** — combining LTE and WiFi at the protocol layer for seamless handoff

### Mesh Networking

Traditional WiFi extenders halve throughput at each hop (they must receive and re-transmit on the same channel). Mesh networks use a **dedicated backhaul radio** — typically 5 GHz or 6 GHz — exclusively for AP-to-AP communication, keeping separate radios free for client devices. Self-healing path selection (802.11s) automatically re-routes traffic around failed or congested nodes. Combined with 802.11r fast roaming, devices move through a building without dropping connections.

### Target Wake Time (TWT)

Introduced in WiFi 6, TWT allows an AP to negotiate scheduled wake windows with IoT devices — for example, telling a sensor to wake at 3:00 AM every 15 minutes for 10 milliseconds, then sleep. Battery life can increase by orders of magnitude. TWT also reduces channel contention by preventing dozens of IoT devices from continuously monitoring the channel.

### BSS Coloring

In older WiFi, a device that heard any signal on its channel would defer transmission — even from a separate network through a wall. BSS Coloring tags every frame with a 6-bit color identifying the network (BSS = Basic Service Set). Devices now distinguish between their own network and foreign networks, applying a lower interference threshold for foreign signals — allowing simultaneous transmissions rather than unnecessary deferral.

### Multi-Link Operation (MLO)

MLO is the most architecturally significant WiFi change since MIMO. A single logical connection spans multiple bands simultaneously. The MAC and PHY layers are re-architected so a device can aggregate throughput across 2.4 + 5 + 6 GHz, load-balance traffic across links, and maintain connection continuity when one band experiences interference — with zero re-association required. Expected outcome: sub-1ms latency variance vs. the 10–50ms common in WiFi 6 under load.

---

## 6. RF Metrics & PHY Concepts

### dB — The Logarithmic Unit of Ratio

A **decibel (dB)** is a logarithmic ratio comparing two power values:

```
dB = 10 × log₁₀(P₂ / P₁)
```

Why logarithms? RF signals span an enormous dynamic range — watts of transmit power down to femtowatts received. Logarithms compress this into human-friendly numbers, and they turn multiplications into simple additions (essential for link budget calculations).

**Essential rules to memorize:**

| Change | Effect on Power |
|--------|----------------|
| +3 dB | Doubles |
| −3 dB | Halves |
| +10 dB | Multiplies by 10 |
| +20 dB | Multiplies by 100 |
| +30 dB | Multiplies by 1,000 |
| 0 dB | No change (ratio = 1) |

Because dB is a ratio, values can be chained: a cable losing 3 dB and an amplifier adding 10 dB yields a net of +7 dB — just add and subtract.

### dBm — Absolute Power Referenced to 1 mW

**dBm** is dB referenced to 1 milliwatt (1 mW = 0 dBm). It is an *absolute* power measurement:

```
dBm = 10 × log₁₀(Power in mW / 1 mW)
```

| Power Level | dBm | Context |
|------------|-----|---------|
| 1 W | +30 dBm | Max legal WiFi TX power (some bands) |
| 100 mW | +20 dBm | Typical router TX power |
| 32 mW | +15 dBm | Typical phone TX power |
| 1 mW | 0 dBm | Reference point |
| — | −50 dBm | Excellent received signal |
| — | −70 dBm | Good signal, most tasks work |
| — | −85 dBm | Weak, throughput degrades |
| — | −95 dBm | Near noise floor, barely functional |

### dBi — Antenna Gain

**dBi** measures antenna gain relative to a theoretical isotropic radiator (one that radiates equally in all directions). Gain does not create new power — it *redirects* it. A dipole (rubber duck antenna) has ~2.15 dBi. A high-gain Yagi may reach 14–18 dBi.

> **dBd vs dBi:** Some antennas are rated in dBd (relative to a dipole). Convert by adding 2.15: 5 dBd = 7.15 dBi.

### EIRP — Effective Isotropic Radiated Power

**EIRP** is the total effective power radiated in the peak direction of an antenna, accounting for TX power, cable losses, and antenna gain:

```
EIRP (dBm) = TX Power (dBm) − Cable Loss (dB) + Antenna Gain (dBi)
```

Example: 20 dBm TX − 1 dB cable loss + 3 dBi antenna = **22 dBm EIRP**

Regulatory bodies (FCC, ETSI) cap maximum **EIRP**, not just TX power. This is why attaching a high-gain antenna to a router does not legally boost range — the higher gain must be offset by reducing TX power to remain within the EIRP ceiling. Typical US limits: 30 dBm EIRP for 2.4 GHz point-to-multipoint; up to 53 dBm for certain 5 GHz point-to-point links.

### RSSI — Received Signal Strength Indicator

**RSSI** measures how strong the received WiFi signal is at the client device. Despite being ubiquitous, RSSI is poorly standardized — it is a vendor-specific unitless index. In practice, tools report it in **dBm**, which is the meaningful quantity.

| Signal Level | Quality | Typical Behaviour |
|---|---|---|
| −30 to −50 dBm | Excellent | Maximum MCS, full throughput |
| −51 to −60 dBm | Good | Streaming, gaming, video calls work well |
| −61 to −70 dBm | Fair | Lower MCS, throughput drops but usable |
| −71 to −80 dBm | Poor | Retransmissions, high latency, drops |
| Below −80 dBm | Critical | Near noise floor, likely disconnects |

**RSSI vs SNR:** Signal-to-Noise Ratio (SNR = Signal − Noise Floor in dBm) is often more meaningful than raw RSSI. A signal of −70 dBm with a −95 dBm noise floor (SNR = 25 dB) is workable. The same −70 dBm in a −72 dBm noise environment (SNR = 2 dB) is completely unusable.

### Spatial Streams

A **spatial stream** is an independent data stream transmitted simultaneously on the same frequency channel using MIMO. The receiver uses matrix algebra to separate streams that arrived via different multipath reflections.

Notation: **NxM:SS** — for example, 4×4:4 = 4 TX antennas, 4 RX antennas, 4 spatial streams. The stream count is always limited by the device with fewer antennas.

| Streams | Typical Device | Throughput Multiplier |
|---------|---------------|----------------------|
| 1SS | IoT sensors, budget phones | ×1 |
| 2SS | Most laptops, mid-range phones | ×2 |
| 3SS | High-end laptops | ×3 |
| 4SS | Access points, gaming routers | ×4 |
| 8SS | Enterprise APs (WiFi 6) | ×8 |
| 16SS | Enterprise APs (WiFi 7, theoretical) | ×16 |

Each stream adds the full single-stream PHY rate. In practice, streams require sufficient antenna separation (≥ λ/2) and rich multipath. Outdoors with line-of-sight and close antenna spacing, high stream counts degrade.

### MCS Index — The Master Control of WiFi Speed

The **Modulation and Coding Scheme (MCS) index** is a single number encoding the combination of modulation order and coding rate used for a transmission. The router's rate adaptation algorithm adjusts MCS continuously in real time based on signal quality.

**WiFi 6 MCS Table (1 spatial stream, 80 MHz, 800 ns GI):**

| MCS | Modulation | Coding Rate | Bits/Symbol | PHY Rate |
|-----|-----------|-------------|-------------|----------|
| 0 | BPSK | 1/2 | 1 | 8.6 Mbps |
| 1 | QPSK | 1/2 | 2 | 17.2 Mbps |
| 2 | QPSK | 3/4 | 2 | 25.8 Mbps |
| 3 | 16-QAM | 1/2 | 4 | 34.4 Mbps |
| 4 | 16-QAM | 3/4 | 4 | 51.6 Mbps |
| 5 | 64-QAM | 2/3 | 6 | 68.8 Mbps |
| 6 | 64-QAM | 3/4 | 6 | 77.4 Mbps |
| 7 | 64-QAM | 5/6 | 6 | 86.0 Mbps |
| 8 | 256-QAM | 3/4 | 8 | 103.2 Mbps |
| 9 | 256-QAM | 5/6 | 8 | 114.7 Mbps |
| 10 | 1024-QAM | 3/4 | 10 | 129.0 Mbps |
| 11 | 1024-QAM | 5/6 | 10 | 143.4 Mbps |
| 12 ✦ | 4096-QAM | 3/4 | 12 | 154.9 Mbps |
| 13 ✦ | 4096-QAM | 5/6 | 12 | 172.1 Mbps |

✦ *MCS 12–13 are WiFi 7 only. Multiply by spatial stream count for total link rate.*

**Coding rate** determines the fraction of bits that are actual data vs. error-correction overhead. Rate 1/2 = half the bits are redundant (robust but slow). Rate 5/6 = 83% is data (efficient but fragile — requires strong SNR).

### PHY Rate — What "866 Mbps" Actually Means

The **PHY rate** (Physical Layer Rate) is the raw bit rate at the radio level — the number your OS reports as your link speed. It is determined by four multiplied parameters:

```
PHY Rate ≈ Subcarriers × Bits/Symbol (MCS) × Coding Rate × Spatial Streams / Symbol Duration
```

| Parameter | Effect |
|-----------|--------|
| Channel Width ↑ | More OFDM subcarriers → higher rate (160 MHz ≈ 2× of 80 MHz) |
| MCS Index ↑ | Denser modulation → more bits per symbol |
| Spatial Streams ↑ | Each stream adds the full single-stream rate |
| Guard Interval ↓ | Shorter GI (e.g. 400 ns vs 800 ns) gives ~11% more throughput |

> **Critical caveat:** Real-world throughput is typically **40–60% of the PHY rate**. The gap is consumed by MAC layer overhead (ACKs, backoff, inter-frame spacing), protocol headers, retransmissions, and WiFi's half-duplex nature. A "1200 Mbps" WiFi 6 link delivers roughly 400–700 Mbps of actual TCP throughput under ideal conditions.

### Complete Signal Path Example

To tie all metrics together — a 4K streaming scenario from across the house:

| Stage | Value | Explanation |
|-------|-------|-------------|
| TX Power | +20 dBm | Router transmits at 100 mW on 5 GHz, 80 MHz |
| EIRP | +22 dBm | +20 dBm − 1 dB cable loss + 3 dBi antenna |
| Path Loss | −60 dB | 10 m through 2 walls |
| RSSI at client | **−65 dBm** | Fair/good signal |
| SNR | ~25 dB | Noise floor ~−90 dBm |
| MCS selected | **MCS 7** | 64-QAM 5/6 — appropriate for 25 dB SNR |
| PHY Rate | 172 Mbps | 2 spatial streams × 86 Mbps (MCS 7, 80 MHz) |
| Actual throughput | ~80–100 Mbps | After MAC and protocol overhead |

---

## 7. WiFi Security

### Protocol Evolution

| Protocol | Year | Encryption | Key Exchange | Status |
|----------|------|-----------|--------------|--------|
| WEP | 1999 | RC4 (40/104-bit) | Static PSK | **Broken — never use** |
| WPA | 2003 | TKIP (RC4-based) | PSK or 802.1X | Deprecated |
| WPA2-Personal | 2004 | AES-CCMP (128-bit) | PSK + 4-way handshake | Widely used |
| WPA2-Enterprise | 2004 | AES-CCMP (128-bit) | 802.1X / RADIUS / EAP | Widely used |
| WPA3-Personal | 2018 | AES-GCMP-256 | SAE (Dragonfly) | Current standard |
| WPA3-Enterprise | 2018 | AES-GCMP-256 | 802.1X + 192-bit suite | Current standard |

### Why WEP Failed

WEP used the RC4 stream cipher with a 24-bit Initialization Vector (IV). Because IVs were short, they repeated frequently. Researchers in 2001 showed that collecting enough packets with repeated IVs allowed statistical recovery of the key. By 2007, WEP could be cracked in under a minute with freely available tools. The design was fatally flawed from the start.

### WPA3's SAE (Dragonfly Handshake)

WPA2-Personal's 4-way handshake could be captured over the air and subjected to offline dictionary attacks — weak passwords could be cracked at leisure. WPA3's **Simultaneous Authentication of Equals (SAE)** is a zero-knowledge proof protocol: even if all handshake packets are captured, an offline dictionary attack is not possible. Each authentication attempt requires live interaction with the network. WPA3 also provides **forward secrecy** — even if a password is later compromised, previously captured sessions remain encrypted.

---

## 8. The Future of WiFi

### WiFi Sensing (802.11bf)

WiFi signals reflect off objects and people. By analysing how multipath reflections change over time, a WiFi 7 AP can detect motion, recognise gestures, monitor breathing rates, and estimate occupancy — without any wearable devices. 802.11bf is being standardised now. Future routers may double as passive sensors for smart home automation and health monitoring.

### WiFi 8 (802.11bn) — Ultra High Reliability

Expected around 2028, WiFi 8 targets **deterministic latency** — guaranteeing maximum latency bounds rather than minimising averages. This is critical for industrial automation, surgical robotics, and XR. It will also explore the 60 GHz millimeter-wave band more extensively for short-range multi-gigabit links.

### 5G and WiFi Convergence

The boundary between WiFi and cellular is blurring. **CBRS** (3.5 GHz in the US) allows enterprises to deploy private 5G networks alongside WiFi. **OpenRoaming** enables seamless, carrier-grade automatic offloading between 5G and WiFi globally. The end goal: a unified experience where the access technology is invisible and the device always uses the best available connection.

### Passive WiFi & Energy Harvesting

Research has demonstrated devices communicating over WiFi at tens of microwatts — 10,000× less power than conventional WiFi chips — by using **backscatter**: reflecting an existing WiFi signal rather than generating one. Combined with ambient RF energy harvesting from surrounding WiFi and cellular signals, this could produce battery-free WiFi sensors that run indefinitely with no maintenance.

---

## Quick Reference Cheat Sheet

| Term | Definition |
|------|-----------|
| **dB** | Logarithmic ratio of two power values: 10 × log₁₀(P2/P1) |
| **dBm** | Absolute power in dB relative to 1 mW |
| **dBi** | Antenna gain relative to a theoretical isotropic radiator |
| **EIRP** | TX Power − Cable Loss + Antenna Gain; the regulatory metric |
| **RSSI** | Received signal strength at the client device (reported in dBm) |
| **SNR** | Signal (dBm) − Noise Floor (dBm); more meaningful than raw RSSI |
| **MCS** | Modulation and Coding Scheme index — controls speed vs. robustness tradeoff |
| **PHY Rate** | Raw bit rate at the radio layer; actual throughput is ~40–60% of this |
| **Spatial Stream** | Independent data stream through MIMO; each stream multiplies total rate |
| **OFDM** | Divides channel into orthogonal sub-carriers to handle multipath |
| **OFDMA** | Assigns different sub-carriers to different users simultaneously (WiFi 6+) |
| **MU-MIMO** | AP transmits to multiple clients simultaneously using beamforming |
| **MLO** | Multi-Link Operation — aggregates multiple bands into one logical link (WiFi 7) |
| **TWT** | Target Wake Time — schedules IoT device wake windows to save battery |
| **BSS Coloring** | Tags frames by network to reduce unnecessary channel deferral |
| **CSMA/CA** | Channel access protocol — listen before transmit, backoff on collision |
| **WPA3 SAE** | Dragonfly handshake — prevents offline dictionary attacks on WiFi passwords |
| **WiFi Offloading** | Routing mobile traffic through WiFi instead of cellular to reduce cost |
| **Beamforming** | Focuses RF energy toward a target device using phased antenna arrays |
