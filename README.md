# 🔊 Vintage Bluetooth Speaker

**Turn any vintage speaker into a modern wireless audio system.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/badge/Version-1.10-blue.svg)]()
[![Status: In Development](https://img.shields.io/badge/Status-In%20Development-orange.svg)]()

---

## ✨ What is this?

A complete DIY guide to breathe new life into your old speaker cabinet. Stream music via **Bluetooth** or **WiFi** while keeping that beautiful vintage aesthetic.

**No woodworking. No speaker replacement. Just electronics.**

---

## 🎯 Features

| Feature | Description |
|---------|-------------|
| 🔋 Battery Powered | 4S 18650 pack (~6h playtime) |
| 📡 Bluetooth 5.0 | Instant pairing from any phone |
| 📶 WiFi Streaming | AirPlay, Spotify Connect, DLNA |
| 🛡️ Full Protection | Inrush NTC, fuse, TVS, snubber, reverse diode |
| 🔧 Test-Ready | Breakout box for safe debugging |
| 💰 Budget Friendly | ~175€ total |

---

## 🧰 Hardware

| Component | Model |
|-----------|-------|
| Amplifier | Arylic Up2Stream Amp V4 |
| Battery | 14.8V 6Ah 4S pack with BMS |
| Charger | 16.8V 2A external adapter |
| Protection | Custom veroboard (see docs) |

---

## 📁 Documentation

| File | Description |
|------|-------------|
| [docs/](docs/) | Full build guides and schematics |
| [Circuit V1.10](docs/Circuit_Enceinte_BT_Vintage_V1_10.md) | **Latest** — Main build guide with BOM and wiring |
| [Breakout Box V1.6](docs/Breakout_Box_Enceinte_BT_V1_6.md) | Test jig — Protected sense lines (1kΩ, fire-safe) |

---

## 🔌 Block Diagram (V1.10)

```
┌──────────┐    ┌────────────────────────────┐    ┌─────────────┐    ┌─────────┐
│ BATTERY  │───▶│      PROTECTION BOARD      │───▶│  UP2STREAM  │───▶│ SPEAKER │
│ 4S 14.8V │    │ D1(SB560)+SW+F+NTC+TVS+C3  │    │   AMP V4    │    │  8Ω+    │
└──────────┘    └────────────────────────────┘    └─────────────┘    └─────────┘
                         │
                    ┌────┴────┐
                    │ BREAKOUT│ (optional)
                    │  BOX    │
                    └─────────┘
```

---

## 📊 Specs (V1.10)

| Parameter | Value |
|-----------|-------|
| Input voltage | 12.0V - 16.8V (4S Li-Ion) |
| **Output power** | **30W typ, 40W peak @ 8Ω** |
| Max current | 3A typ, 5A peak |
| Reverse protection | SB560 Schottky 5A |
| Surge protection | TVS P6KE22CA |
| Overcurrent | 6.3A slow-blow fuse |
| Inrush limiting | NTC 2.5Ω 7A |
| Arc suppression | 47Ω + 100nF film 100V snubber |
| Bass stability | 1000µF bulk cap at amp |
| Min speaker impedance | 8Ω (DCR ≥ 5.5Ω) |

---

## 📷 Gallery

*Coming soon — Build photos and final result*

---

## 🚀 Quick Start

1. **Order parts** — See BOM in Circuit V1.10
2. **Check speaker** — Measure DCR ≥ 5.5Ω
3. **Configure Up2Stream** — Move jumpers to MONO mode
4. **Build protection board** — 50 min soldering
5. **Wire everything** — Follow the guide step by step
6. **Enjoy** — Pair your phone and play music

---

## ⚠️ Critical Warnings

| # | Warning |
|---|---------|
| 1 | **Speaker ≥ 8Ω only** — Measure DCR ≥ 5.5Ω before use |
| 2 | **Turn OFF before charging** — Noise/cutoffs otherwise |
| 3 | **Wait 30s between OFF/ON** — NTC must cool down |
| 4 | **16.8V 2A charger ONLY** — 24V charger destroys circuit |
| 5 | **Disconnect if storing > 2 weeks** — IND1 drains battery |
| 6 | **Ensure ventilation** — Module max 40°C |
| 7 | **Small "pop" at power-off is normal** — No damage |

---

## 🔄 Changelog

| Version | Date | Changes |
|---------|------|---------|
| **V1.10** | Dec 2025 | External audit: D1→SB560(5A), NTC→7A, +C3 bulk, power spec fixed |
| V1.9 | Dec 2025 | Snubber 100V film, R_sense 10kΩ fire-safe breakout |
| V1.8 | Dec 2025 | Certified audit: PTC removed, snubber added, NTC raised 10mm |
| V1.7 | Dec 2025 | D1 reverse protection, TVS 22CA, decoupling, ferrite |

---

## 📜 License

MIT — Do whatever you want with this.

---

## 🙏 Credits

Designed and documented with the help of Claude (Anthropic).

---

**Made with ❤️ for vintage audio lovers**
