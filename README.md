<div align="center">

# بِسْمِ اللهِ الرَّحْمٰنِ الرَّحِيْمِ

# 🛰️ Satellite & Navigation Systems Security

### Understanding Architecture, Threats & Attack Simulation in GNSS Systems

**Presented by: Lubaba Zafar**
Diploma in Cloud Cyber Security | RQF Level 3

![Kali Linux](https://img.shields.io/badge/Kali_Linux-557C94?style=flat&logo=kalilinux&logoColor=white)
![GNU Radio](https://img.shields.io/badge/GNU_Radio-FF6600?style=flat&logo=gnu&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![VirtualBox](https://img.shields.io/badge/VirtualBox-183A61?style=flat&logo=virtualbox&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-success?style=flat)

</div>

---

> *"Modern navigation depends on invisible signals — and when those are compromised, the consequences are real."*

---

## 📋 Table of Contents

| # | Section |
|---|---------|
| 1 | [Key Learning Objectives](#-key-learning-objectives) |
| 2 | [Satellite Communication & GNSS](#-satellite-communication--gnss) |
| 3 | [GNSS Systems Architecture](#-gnss-systems-architecture) |
| 4 | [How GNSS Works & Why Signals Are Weak](#-how-gnss-works--why-signals-are-weak) |
| 5 | [GNSS Signal and Data Flow](#-gnss-signal-and-data-flow) |
| 6 | [Vulnerabilities](#-vulnerabilities) |
| 7 | [Common Attacks](#-common-attacks) |
| 8 | [GNSS Spoofing — Signal-Level Attack](#-gnss-spoofing--signal-level-attack) |
| 9 | [Real-World Case Study: Black Sea 2017](#-real-world-case-study-black-sea-spoofing-2017) |
| 10 | [Encryption & Authentication](#-encryption--authentication) |
| 11 | [Open-Source Tools](#-open-source-tools) |
| 12 | [Spoofing Detection — Live Simulation](#-spoofing-detection--live-simulation) |
| 13 | [ISO/IEC 27033](#-isoiec-27033) |
| 14 | [Failure & Recovery Scenarios](#-failure--recovery-scenarios) |
| 15 | [Countermeasures](#-countermeasures) |
| 16 | [Conclusion](#-conclusion) |
| 17 | [Repository Structure](#-repository-structure) |

---

## 🎯 Key Learning Objectives

- Understand Satellite communication and GNSS networks
- Explore GNSS architecture and system components
- Understand how the system works including signal flow and data computation
- Identify vulnerabilities at signal, network, and receiver level
- Analyze attacks: **Jamming**, **Spoofing** and **Meaconing**
- Visualize spoofing using a signal-level attack diagram
- Examine a real-world GNSS spoofing case
- Learn how encryption and authentication secure satellite links
- Explore open-source tools: **GNU Radio**, **GQRX** and **SatNOGS**
- Demonstrate spoofing detection using open-source tools
- Understand failure and recovery for these attack scenarios
- Examine **ISO/IEC 27033** and apply countermeasures

---

## 🛰️ Satellite Communication & GNSS

### 1. Satellite Communication
- Wireless link between Earth and Satellite
- Used for TV, internet, defense & telecom

### 2. Global Navigation Satellite System (GNSS)
- Includes **GPS, GLONASS, Galileo, BeiDou**
- Provides **Position, Navigation & Timing (PNT)**
- Used by aviation, ships, telecom and IoT

### 3. Why It's Critical

| Application | Dependency on GNSS |
|-------------|-------------------|
| Banking | Timestamps for transactions |
| Power Grid | Precise timing synchronization |
| Aviation & Shipping | Safe routing and navigation |

---

## 🏗️ GNSS Systems Architecture

| Segment | Components | Key Risk |
|---------|-----------|----------|
| **Space Segment** | Satellites in orbit · Transponders · GNSS satellites broadcast precise timing | Jamming attacks |
| **Ground Segment** | Control centers & uplink stations · IT and network infrastructure | ⚠️ Main target for cyberattacks |
| **User Segment** | Phones, cars, aircraft, ships, receivers · Often trust any strong GNSS signal | ⚠️ Receivers easily spoofed |

---

## 📡 How GNSS Works & Why Signals Are Weak

### How It Works
- Uplink from ground → satellite → downlink back to user
- GNSS satellites broadcast **one-way** timing & navigation data

### Frequencies & Protocols

| Band | Use | Risk |
|------|-----|------|
| **L-band (1–2 GHz)** | GNSS signals | Primary attack surface |
| S, C, Ku, Ka Bands | TV, Broadband, Telecom | — |
| Protocols | DVB-S2, IP, UDP, TCP | Encrypted command/control links |

### Why GNSS Signals Are Weak
- Very low power when they arrive at Earth
- Easily affected by noise, jamming or spoofing
- Receivers often lock onto the **strongest signal — even if it's fake**

---

## 🔄 GNSS Signal and Data Flow

```
SPACE SEGMENT        GROUND SEGMENT           USER SEGMENT
─────────────        ──────────────────       ────────────────
GNSS Satellite  ───► Control Station    ────► GNSS Receiver
GPS / GLONASS        Uplink commands          Phone / Ship
Galileo              ⚠️ Main attack target    ⚠️ Easily spoofed
⚠️ L-band (weak)    ISO/IEC 27033 applies    Locks to strongest signal
```

### How a GNSS Position Is Computed

| Step | Action | NIST CSF |
|------|--------|----------|
| 1 | Satellite sends timing signal | Identify |
| 2 | Receiver picks up ≥4 satellites | Protect |
| 3 | Calculates time difference | Detect |
| 4 | Trilateration computes position | Respond |
| 5 | PNT output delivered to user | Recover |

---

## ⚠️ Vulnerabilities

| Level | Vulnerability |
|-------|--------------|
| **Signal Level** | Extremely weak GNSS signals · Civil GNSS has no built-in authentication |
| **Network Level** | Ground stations run on IP networks · If hacked, attackers can disrupt satellite operations |
| **Receiver Level** | Devices lock to strongest signal · Vulnerable firmware or poor validation |
| **Operational Level** | Misconfiguration · Weak or poorly managed keys and passwords |

---

## ⚔️ Common Attacks

| # | Attack | What It Does |
|---|--------|-------------|
| 1 | **Jamming** | Sends noise on GNSS frequencies · Blocks or degrades satellite signals |
| 2 | **Spoofing** | Transmits fake GNSS signals · Tricks receivers into wrong position or time |
| 3 | **Meaconing** | Rebroadcasts real signals with delay · Causes gradual position error |
| 4 | **Interference** | Accidental or intentional signal overlap · Reduces accuracy and reliability |

---

## 🎭 GNSS Spoofing — Signal-Level Attack

```
     🛰️ Satellite        🛰️ Satellite        🛰️ Satellite
           \                  |                  /
            \                 |                 /
         Real GNSS signals (weak - - - - - - -)
                         |
                   📍 GNSS Receiver ──────► ❌ Wrong Position
                         ▲
                         |
           Fake GNSS signal (STRONG — attacker)
                         |
                  📡 Spoofer Device
```

- The spoofer transmits a **fake signal stronger** than the real satellite signal
- The receiver locks onto the fake signal
- The receiver reports the **wrong position or time** without knowing it has been deceived

---

## 🌊 Real-World Case Study: Black Sea Spoofing (2017)

| | Details |
|-|---------|
| **What happened** | 24+ ships showed GPS location at Gelendzhik Airport while sailing in the Black Sea |
| **Impact** | Navigation confusion · Safety concerns · Port delays |
| **Why it matters** | Proved large-scale GNSS spoofing is real, not just theoretical |
| **Key lessons** | Use multiple GNSS constellations · Monitor for anomalies · Keep backup navigation |

> Reference: [Inside GNSS — Black Sea Spoofing Report](https://insidegnss.com/reports-of-mass-gps-spoofing-attack-in-the-black-sea-strengthen-calls-for-pntbackup/)

---

## 🔐 Encryption & Authentication

### Encryption
- Protects data transmitted between ground station and satellite
- Stops attackers from reading or modifying commands
- **AES-256** used for securing satellite data links

### Authentication
- Confirms that a signal or command comes from a trusted source
- Helps prevent spoofed signals and fake control messages
- **Digital signatures** verify message integrity

### Civil vs Military GNSS

| Type | Authentication | Risk Level |
|------|---------------|-----------|
| Civil signals | No authentication | ⚠️ Easier to spoof |
| Military signals | Encrypted & authenticated | ✅ Much harder to attack |

---

## 🛠️ Open-Source Tools

| Tool | Purpose | Used In This Project |
|------|---------|---------------------|
| **GNU Radio** | Signal processing toolkit · Simulate GNSS signals · Demonstrate jamming and spoofing | ✅ Yes — all simulations |
| **GQRX** | Software-defined radio receiver · Real-time spectrum visualization · Detect abnormal signal strength | Reference tool |
| **SatNOGS** | Global satellite ground station network · Monitors satellite signals worldwide · Identifies anomalies | Reference tool |

---

## 🔬 Spoofing Detection — Live Simulation

> **Tool:** GNU Radio Companion on Kali Linux (VirtualBox)

### Simulation 1 — Spoofing Only (4 Blocks)

```
[Variable: samp_rate = 32000]

[Signal Source 1]──┐
 Real GNSS          ├──►[Add]──►[QT GUI Sink]
 Freq: 1000 Hz      │          FFT: 1024 | BW: 32k
 Sine | Amp: 1      │
                    │
[Signal Source 2]──┘
 Spoofed GNSS
 Freq: 1200 Hz
 Sine | Amp: 1
```

### Spectrum Output

![Spoofing Detection](screenshots/spoofing_spectrum_output.png)

| Observation | Meaning |
|-------------|---------|
| Peak at **0.77 kHz, 73.81 dB** | Spoofed signal clearly present |
| Authentic GNSS signals are much weaker | Receiver would lock to fake signal |
| Sharp clean spike | Confirms deliberate spoofing |

---

### Simulation 2 — Combined Attack (Jamming + Spoofing + Mitigation)

![GNU Radio Flowgraph](screenshots/gnuradio_flowgraph.png)

```
[Signal Source — Real GNSS]──────────────────────────────►┐
 Freq: 1000 Hz | Amp: 0.5 | Cosine                        │
                                                     [Add1]─►┐
[Noise Source — Jammer]──────────────────────────────────►┘  │
 Gaussian | Amp: 3                                            ├──►[Add2]──►[Low Pass Filter]──►[Throttle]
                                                              │   Cutoff: 1500 Hz                  │
[Signal Source — Fake GNSS]──────────────────────────────────►┘   Window: Hamming            ├──►[QT GUI Frequency Sink]
 Freq: 1005 Hz | Amp: 2 | Cosine                                                              ├──►[QT GUI Waterfall Sink]
                                                                                               └──►[QT GUI Time Sink]
```

### Output Analysis

| Sink | Observation | Meaning |
|------|-------------|---------|
| **Frequency Sink** | Dominant peak + elevated noise floor | Spoofing + Jamming both active |
| **Waterfall Sink** | Bright band sustained over time | Attack is continuous |
| **Time Sink** | Two overlapping waveforms | Real + Spoofed signals both present |

---

## 📜 ISO/IEC 27033

> Network Communication Security Standard

| What It Does | How It Applies Here |
|-------------|-------------------|
| Designs secure network communication | Protects ground station networks |
| Segments critical networks | Separates control vs office traffic |
| Encrypts important data paths | Secures satellite command links |
| Protects command & control traffic | Prevents attacker from hijacking satellite |

---

## 💥 Failure & Recovery Scenarios

| Attack | Failure | Recovery |
|--------|---------|----------|
| **Jamming** | Signal lost · Navigation disabled | Backup navigation (INS) · Directional antenna · Multi-frequency GNSS |
| **Spoofing** | Wrong position reported · Black Sea 2017 | RAIM integrity monitoring · Multi-constellation cross-check · Authenticate nav messages |
| **Meaconing** | Gradual position drift · Timing errors | Monitor anomalies (GQRX) · Compare almanac data · Manual navigation |
| **Ground Hack** | Satellite commands hijacked · Full outage | ISO/IEC 27033 segmentation · AES-256 links · Wazuh SIEM Rule 5712 |

> **Defence-in-Depth:** Signal Layer → Network Layer → Receiver Layer → Operational Layer
> **NIST CSF:** Protect · Detect · Respond

---

## 🛡️ Countermeasures

### Anti-Jamming
- Adaptive / Directional antennas
- Spectrum monitoring for interference
- Use multiple GNSS frequencies

### Anti-Spoofing
- Authenticate navigation messages
- Compare signals from multiple GNSS systems
- **RAIM** to check integrity of GNSS data

### System Hardening
- Secure ground networks (ISO/IEC 27033)
- Strong encryption & key management (AES-256)
- Backup navigation if GNSS looks untrustworthy

---

## ✅ Conclusion

> *"Satellite and GNSS systems are critical to global infrastructure, supporting sectors such as aviation, shipping, banking and power grids. However, their weak and unauthenticated signals make them highly vulnerable to attacks like jamming, spoofing and meaconing.*
>
> *Through GNU Radio simulation, these vulnerabilities were practically demonstrated, highlighting how easily signals can be manipulated. Therefore, implementing encryption, authentication, monitoring tools and standards such as ISO/IEC 27033 is essential to ensure the security and resilience of these vital systems."*

---

## 📁 Repository Structure

```
gnss-spoofing-simulation/
│
├── README.md
│
├── presentation/
│   └── Lubaba_GNSS_presentation.pdf
│
├── screenshots/
│   ├── spoofing_spectrum_output.png
│   └── gnuradio_flowgraph.png
│
├── demo-video/
│   └── demo_video_link.md
│
└── code/
    ├── 01_install_gnuradio.md
    ├── 02_spoofing_simulation.md
    └── 03_combined_attack_flowgraph.md
```

---

<div align="center">

**Lubaba Zafar**
Cybersecurity Student | Aspiring SOC Analyst | Pakistan
Diploma in Cloud Cyber Security | RQF Level 3

[![GitHub](https://img.shields.io/badge/GitHub-lubaba1513--pixel-181717?style=flat&logo=github)](https://github.com/lubaba1513-pixel)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0077B5?style=flat&logo=linkedin)](https://linkedin.com/in/YOUR_LINKEDIN)

*⚠️ For educational purposes only. All simulations conducted in an isolated virtual environment. No real GNSS signals were transmitted or interfered with.*

</div>
