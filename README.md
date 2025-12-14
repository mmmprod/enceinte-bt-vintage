# 🔊 Vintage Bluetooth Speaker

**Turn any vintage speaker into a modern wireless audio system.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/badge/Version-1.8-blue.svg)]()
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
| 🔧 Test-Ready | Breakout box for easy debugging |
| 💰 Budget Friendly | ~160€ total |

---

## 🧰 Hardware

| Component | Model |
|-----------|-------|
| Amplifier | Arylic Up2Stream Amp V4 |
| Battery | 14.8V 6Ah 4S pack with BMS |
| Charger | 16.8V 2A external adapter |
| Protection | Custom veroboard (NTC + PTC + TVS) |

---

## 📁 Documentation

| File | Description |
|------|-------------|
| [docs/](docs/) | Full build guides and schematics |
| [Circuit V1.8](docs/Circuit_Enceinte_BT_Vintage_V1_8.md) | Main build guide with BOM and wiring |
| [Breakout Box V1.4](docs/Breakout_Box_Enceinte_BT_V1_4.md) | Test jig for voltage monitoring (parallel observation) |
| Tests *(coming soon)* | Validation protocol |

---

## 🔌 Block Diagram

```
┌──────────┐    ┌────────────────┐    ┌─────────────┐    ┌─────────┐
│ BATTERY  │───▶│  PROTECTION    │───▶│  UP2STREAM  │───▶│ SPEAKER │
│ 4S 14.8V │    │ SW+F+NTC+PTC   │    │   AMP V4    │    │  MONO   │
└──────────┘    └────────────────┘    └─────────────┘    └─────────┘
```

---

## 📷 Gallery

*Coming soon — Build photos and final result*

---

## 🚀 Quick Start

1. **Order parts** — See BOM in Circuit V1.6
2. **Configure Up2Stream** — Move jumpers to MONO mode
3. **Build protection board** — 30 min soldering
4. **Wire everything** — Follow the guide step by step
5. **Enjoy** — Pair your phone and play music

---

## ⚠️ Safety

- **Check speaker impedance first** — Must measure ≥5.5Ω (DCR) for MONO mode
- **Always turn OFF before charging** — Never charge while playing
- **Wait 30s between OFF and ON** — Let NTC cool down
- **Double-check polarity** — Red = +, Black = -
- Keep NTC raised 10mm above PCB (it heats up)

---

## 📜 License

MIT — Do whatever you want with this.

---

## 🙏 Credits

Designed and documented with the help of Claude (Anthropic).

---

**Made with ❤️ for vintage audio lovers**
