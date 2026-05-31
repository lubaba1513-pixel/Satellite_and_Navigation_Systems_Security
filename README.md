<div align="center">
بِسْمِ اللهِ الرَّحْمٰنِ الرَّحِيْمِ
🛰️ Satellite & Navigation Systems Security
Understanding Architecture, Threats & Attack Simulation in GNSS Systems
Presented by: Lubaba Zafar
Diploma in Cloud Cyber Security | RQF Level 3
Show Image
Show Image
Show Image
Show Image
Show Image
</div>


"Modern navigation depends on invisible signals — and when those are compromised, the consequences are real."


📋 Table of Contents
#Section1Key Learning Objectives2Satellite Communication & GNSS3GNSS Systems Architecture4How GNSS Works & Why Signals Are Weak5GNSS Signal and Data Flow6Vulnerabilities7Common Attacks8GNSS Spoofing — Signal-Level Attack9Real-World Case Study: Black Sea 201710Encryption & Authentication11Open-Source Tools12Spoofing Detection — Live Simulation13ISO/IEC 2703314Failure & Recovery Scenarios15Countermeasures16Conclusion17Repository Structure

🎯 Key Learning Objectives

Understand Satellite communication and GNSS networks
Explore GNSS architecture and system components
Understand how the system works including signal flow and data computation
Identify vulnerabilities at signal, network, and receiver level
Analyze attacks: Jamming, Spoofing and Meaconing
Visualize spoofing using a signal-level attack diagram
Examine a real-world GNSS spoofing case
Learn how encryption and authentication secure satellite links
Explore open-source tools: GNU Radio, GQRX and SatNOGS
Demonstrate spoofing detection using open-source tools
Understand failure and recovery for these attack scenarios
Examine ISO/IEC 27033 and apply countermeasures


🛰️ Satellite Communication & GNSS
1. Satellite Communication

Wireless link between Earth and Satellite
Used for TV, internet, defense & telecom

2. Global Navigation Satellite System (GNSS)

Includes GPS, GLONASS, Galileo, BeiDou
Provides Position, Navigation & Timing (PNT)
Used by aviation, ships, telecom and IoT

3. Why It's Critical
ApplicationDependency on GNSSBankingTimestamps for transactionsPower GridPrecise timing synchronizationAviation & ShippingSafe routing and navigation

🏗️ GNSS Systems Architecture
SegmentComponentsKey RiskSpace SegmentSatellites in orbit · Transponders · GNSS satellites broadcast precise timingJamming attacksGround SegmentControl centers & uplink stations · IT and network infrastructure⚠️ Main target for cyberattacksUser SegmentPhones, cars, aircraft, ships, receivers · Often trust any strong GNSS signal⚠️ Receivers easily spoofed

📡 How GNSS Works & Why Signals Are Weak
How It Works

Uplink from ground → satellite → downlink back to user
GNSS satellites broadcast one-way timing & navigation data

Frequencies & Protocols
BandUseRiskL-band (1–2 GHz)GNSS signalsPrimary attack surfaceS, C, Ku, Ka BandsTV, Broadband, Telecom—ProtocolsDVB-S2, IP, UDP, TCPEncrypted command/control links
Why GNSS Signals Are Weak

Very low power when they arrive at Earth
Easily affected by noise, jamming or spoofing
Receivers often lock onto the strongest signal — even if it's fake


🔄 GNSS Signal and Data Flow
SPACE SEGMENT        GROUND SEGMENT           USER SEGMENT
─────────────        ──────────────────       ────────────────
GNSS Satellite  ───► Control Station    ────► GNSS Receiver
GPS / GLONASS        Uplink commands          Phone / Ship
Galileo              ⚠️ Main attack target    ⚠️ Easily spoofed
⚠️ L-band (weak)    ISO/IEC 27033 applies    Locks to strongest signal
How a GNSS Position Is Computed
StepActionNIST CSF1Satellite sends timing signalIdentify2Receiver picks up ≥4 satellitesProtect3Calculates time differenceDetect4Trilateration computes positionRespond5PNT output delivered to userRecover

⚠️ Vulnerabilities
LevelVulnerabilitySignal LevelExtremely weak GNSS signals · Civil GNSS has no built-in authenticationNetwork LevelGround stations run on IP networks · If hacked, attackers can disrupt satellite operationsReceiver LevelDevices lock to strongest signal · Vulnerable firmware or poor validationOperational LevelMisconfiguration · Weak or poorly managed keys and passwords

⚔️ Common Attacks
#AttackWhat It Does1JammingSends noise on GNSS frequencies · Blocks or degrades satellite signals2SpoofingTransmits fake GNSS signals · Tricks receivers into wrong position or time3MeaconingRebroadcasts real signals with delay · Causes gradual position error4InterferenceAccidental or intentional signal overlap · Reduces accuracy and reliability

🎭 GNSS Spoofing — Signal-Level Attack
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

The spoofer transmits a fake signal stronger than the real satellite signal
The receiver locks onto the fake signal
The receiver reports the wrong position or time without knowing it has been deceived


🌊 Real-World Case Study: Black Sea Spoofing (2017)
DetailsWhat happened24+ ships showed GPS location at Gelendzhik Airport while sailing in the Black SeaImpactNavigation confusion · Safety concerns · Port delaysWhy it mattersProved large-scale GNSS spoofing is real, not just theoreticalKey lessonsUse multiple GNSS constellations · Monitor for anomalies · Keep backup navigation

Reference: Inside GNSS — Black Sea Spoofing Report


🔐 Encryption & Authentication
Encryption

Protects data transmitted between ground station and satellite
Stops attackers from reading or modifying commands
AES-256 used for securing satellite data links

Authentication

Confirms that a signal or command comes from a trusted source
Helps prevent spoofed signals and fake control messages
Digital signatures verify message integrity

Civil vs Military GNSS
TypeAuthenticationRisk LevelCivil signalsNo authentication⚠️ Easier to spoofMilitary signalsEncrypted & authenticated✅ Much harder to attack

🛠️ Open-Source Tools
ToolPurposeUsed In This ProjectGNU RadioSignal processing toolkit · Simulate GNSS signals · Demonstrate jamming and spoofing✅ Yes — all simulationsGQRXSoftware-defined radio receiver · Real-time spectrum visualization · Detect abnormal signal strengthReference toolSatNOGSGlobal satellite ground station network · Monitors satellite signals worldwide · Identifies anomaliesReference tool

🔬 Spoofing Detection — Live Simulation

Tool: GNU Radio Companion on Kali Linux (VirtualBox)

Simulation 1 — Spoofing Only (4 Blocks)
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
Spectrum Output
Show Image
ObservationMeaningPeak at 0.77 kHz, 73.81 dBSpoofed signal clearly presentAuthentic GNSS signals are much weakerReceiver would lock to fake signalSharp clean spikeConfirms deliberate spoofing

Simulation 2 — Combined Attack (Jamming + Spoofing + Mitigation)
Show Image
[Signal Source — Real GNSS]──────────────────────────────►┐
 Freq: 1000 Hz | Amp: 0.5 | Cosine                        │
                                                     [Add1]─►┐
[Noise Source — Jammer]──────────────────────────────────►┘  │
 Gaussian | Amp: 3                                            ├──►[Add2]──►[Low Pass Filter]──►[Throttle]
                                                              │   Cutoff: 1500 Hz                  │
[Signal Source — Fake GNSS]──────────────────────────────────►┘   Window: Hamming            ├──►[QT GUI Frequency Sink]
 Freq: 1005 Hz | Amp: 2 | Cosine                                                              ├──►[QT GUI Waterfall Sink]
                                                                                               └──►[QT GUI Time Sink]
Output Analysis
SinkObservationMeaningFrequency SinkDominant peak + elevated noise floorSpoofing + Jamming both activeWaterfall SinkBright band sustained over timeAttack is continuousTime SinkTwo overlapping waveformsReal + Spoofed signals both present

📜 ISO/IEC 27033

Network Communication Security Standard

What It DoesHow It Applies HereDesigns secure network communicationProtects ground station networksSegments critical networksSeparates control vs office trafficEncrypts important data pathsSecures satellite command linksProtects command & control trafficPrevents attacker from hijacking satellite

💥 Failure & Recovery Scenarios
AttackFailureRecoveryJammingSignal lost · Navigation disabledBackup navigation (INS) · Directional antenna · Multi-frequency GNSSSpoofingWrong position reported · Black Sea 2017RAIM integrity monitoring · Multi-constellation cross-check · Authenticate nav messagesMeaconingGradual position drift · Timing errorsMonitor anomalies (GQRX) · Compare almanac data · Manual navigationGround HackSatellite commands hijacked · Full outageISO/IEC 27033 segmentation · AES-256 links · Wazuh SIEM Rule 5712

Defence-in-Depth: Signal Layer → Network Layer → Receiver Layer → Operational Layer
NIST CSF: Protect · Detect · Respond


🛡️ Countermeasures
Anti-Jamming

Adaptive / Directional antennas
Spectrum monitoring for interference
Use multiple GNSS frequencies

Anti-Spoofing

Authenticate navigation messages
Compare signals from multiple GNSS systems
RAIM to check integrity of GNSS data

System Hardening

Secure ground networks (ISO/IEC 27033)
Strong encryption & key management (AES-256)
Backup navigation if GNSS looks untrustworthy


✅ Conclusion

"Satellite and GNSS systems are critical to global infrastructure, supporting sectors such as aviation, shipping, banking and power grids. However, their weak and unauthenticated signals make them highly vulnerable to attacks like jamming, spoofing and meaconing.
Through GNU Radio simulation, these vulnerabilities were practically demonstrated, highlighting how easily signals can be manipulated. Therefore, implementing encryption, authentication, monitoring tools and standards such as ISO/IEC 27033 is essential to ensure the security and resilience of these vital systems."


📁 Repository Structure
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

<div align="center">
Lubaba Zafar
Cybersecurity Student | Aspiring SOC Analyst | Pakistan
Diploma in Cloud Cyber Security | RQF Level 3
Show Image
Show Image
⚠️ For educational purposes only. All simulations conducted in an isolated virtual environment. No real GNSS signals were transmitted or interfered with.
</div>
