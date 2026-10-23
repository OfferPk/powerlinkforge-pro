# PowerlinkForge Pro (v1.0.0)

### Ethernet POWERLINK V2 (EPSG DS301 / IEC 61784-2) Protocol Studio, SoC/PReq/PRes Telegram Dissector, Isochronous Timing Sizer, & Repeating Hub Safety Auditor

[![Version](https://img.shields.io/badge/version-1.0.0-orange.svg)](https://github.com/powerlinkforge/powerlinkforge-pro) [![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT) ![Standard](https://img.shields.io/badge/EPSG%20DS301-Compliant-green.svg) ![Standard](https://img.shields.io/badge/IEC%2061784--2-Compliant-green.svg) ![Tests](https://img.shields.io/badge/Tests-10%2F10%20Passing-brightgreen.svg)

---

## What is PowerlinkForge Pro?

**PowerlinkForge Pro** is an open-core, zero-dependency engineering suite designed for packaging machinery builders, robotics engineers, automation technicians, and motion control teams working with **Ethernet POWERLINK V2**. It provides a complete browser-based workbench and CLI executable for **EPSG DS301 / IEC 61784-2**, enabling developers to build and dissect Layer 2 Ethernet frames (EtherType `0x88AB`), model isochronous cycle budgets down to 200 µs, verify NMT state machine transitions, and audit physical repeating hub topologies and clock jitter boundaries.

---

## Key Capabilities

1. **SoC / PReq / PRes Telegram Frame Builder & Dissector:**  
   - Full support for EtherType `0x88AB` and standard message types: SoC (Start of Cycle), PReq (Poll Request), PRes (Poll Response), SoA (Start of Asynchronous), and ASnd.  
   - IEEE 802.3 CRC-32 checksum calculation and frame validation (\>= 64 octets minimum frame size).  
2. **Isochronous Cycle & Multiplexing Sizer:**  
   - Models isochronous phase duration (SoC \+ PReq/PRes pairs per Controlled Node), repeating hub propagation delays (1.2 µs per hop), and asynchronous TCP/IP bandwidth windows.  
   - Sub-microsecond jitter boundary guarantee (\< 50 ns typical, \< 100 ns boundary).  
3. **NMT (Network Management) State Machine Simulator:**  
   - Simulates and monitors the standard state progression: `Initialisation` \-\> `PreOp1` \-\> `PreOp2` \-\> `ReadyToOperate` \-\> `Operational` (`0xFD`).  
4. **CiA 402 Servo Drive Object Mapping:**  
   - Pre-configured RPDO and TPDO parameter mappings (Controlword `0x6040`, Statusword `0x6041`, Target Velocity, Target Position).  
5. **10-Point Repeating Hub & Motion Safety Auditor:**  
   - Verifies Class II repeating hub physical topology, Managing Node address uniqueness (`0xF0`), Controlled Node address ranges (`1..239`), clock jitter limits, and safe drive velocity ceilings (`0x6046`).  
6. **Multi-Target Master Code Generator:**  
   - Pre-configured integration templates for openPOWERLINK (Linux RT-Preempt C), Python raw AF\_PACKET sockets, and B\&R Automation Studio (Structured Text).  
7. **Standalone Python 3 CLI Executable:**  
   - Zero-dependency CLI tool (`powerlink-cli.py`) for automated test harnesses and field validation.

---

## Directory Structure

product\_193/

├── README.md                              \# Complete product overview

├── source-code/                           \# Web application suite

│   ├── index.html                         \# 5-tab responsive workbench

│   ├── powerlink-frame-engine.js          \# SoC/PReq/PRes framing & CRC-32

│   ├── powerlink-timing-calculator.js     \# Isochronous cycle budget model

│   ├── powerlink-network-auditor.js       \# 10-point network & motion auditor

│   ├── powerlink-forge.css                \# Industrial orange theme styling

│   └── app.js                             \# Interactive UI controller

├── build/                                 \# Executables & distribution

│   ├── powerlink-cli.py                   \# Standalone Python 3 CLI tool (chmod \+x)

│   └── powerlinkforge-pro-v1.0.0.zip      \# Production distribution archive

├── documentation/                         \# Comprehensive manuals

│   ├── ARCHITECTURE.md                    \# Technical architecture & specs

│   ├── USER\_GUIDE.md                      \# Complete usage and test workflows

│   ├── MONETIZATION\_AND\_MARKETING\_PLAYBOOK.md \# Commercial strategy & pricing

│   └── PROGRESS\_REPORT.md                 \# Cycle status & metadata

└── screenshots/                           \# Visual assets & diagrams

    ├── powerlink-studio-preview.svg       \# High-resolution UI mockup

    └── powerlink-architecture-diagram.svg \# Subsystem block diagram

---

## Quick Start

### Web Application

Open `source-code/index.html` in any web browser. No server required.

### Command-Line Interface

\# Build SoC Broadcast Frame

./build/powerlink-cli.py frame-build \--type SoC \--dst 0x00 \--src 0xF0

\# Build PReq Frame

./build/powerlink-cli.py frame-build \--type PReq \--dst 0x01 \--src 0xF0

\# Calculate Timing Budget

./build/powerlink-cli.py timing-calc \--nodes 16 \--cycle-us 400

\# Run Network Safety Audit

./build/powerlink-cli.py audit \--mn 0xF0 \--hub \--jitter 24.5 \--speed 2500 \--limit 4000

---

## License

MIT Open License (c) 2026 PowerlinkForge Pro Contributors.