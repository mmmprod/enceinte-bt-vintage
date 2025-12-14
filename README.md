<p align="center">
  <img src="docs/images/banner.png" alt="Vintage Bluetooth Speaker" width="800">
</p>

<h1 align="center">🎵 Vintage Bluetooth Speaker</h1>

<p align="center">
  <strong>Transform any vintage speaker into a premium wireless audio system</strong>
</p>

<p align="center">
  <a href="#-features"><img src="https://img.shields.io/badge/Power-2x50W-blue?style=for-the-badge" alt="Power"></a>
  <a href="#-quick-start"><img src="https://img.shields.io/badge/DIY-Friendly-green?style=for-the-badge" alt="DIY"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge" alt="License"></a>
  <a href="#-cost"><img src="https://img.shields.io/badge/Cost-~€200-orange?style=for-the-badge" alt="Cost"></a>
</p>

<p align="center">
  <a href="#-features">Features</a> •
  <a href="#-quick-start">Quick Start</a> •
  <a href="#-documentation">Docs</a> •
  <a href="#-gallery">Gallery</a> •
  <a href="#-contributing">Contributing</a>
</p>

---

## ✨ Why This Project?

Found a beautiful vintage speaker at a flea market? **Give it a second life.**

This project turns any passive speaker into a **high-end portable Bluetooth system** — battery powered, premium audio, bulletproof protection.

<p align="center">
  <img src="docs/images/demo.gif" alt="Demo" width="600">
</p>

---

## 🚀 Features

| | Feature | Details |
|---|---------|---------|
| 🔋 | **10h+ Battery** | 4S Li-ion, charge while playing |
| 🎶 | **Hi-Fi Audio** | 2×50W, aptX HD, zero noise |
| 📱 | **Stream Anything** | Bluetooth, WiFi, AirPlay 2, Spotify Connect |
| 🔇 | **Silent ON/OFF** | Soft-start + relay = zero pop |
| ⚡ | **Idiot-Proof** | Wrong charger? Protected. Reversed battery? Protected. |
| 🔧 | **Debug Box** | 7 test points for easy troubleshooting |

---

## 🎯 Quick Start

### You Need

```
□ Vintage speaker (4-8Ω)         ~€20
□ Arylic Up2Stream Amp V4        ~€65
□ 4S Li-ion battery + BMS        ~€60  
□ Electronic components          ~€25
□ Soldering iron + 2h time
```

### Build It

```bash
git clone https://github.com/YOUR_USERNAME/vintage-bluetooth-speaker.git
cd vintage-bluetooth-speaker
# Open docs/Circuit_V2.1.md and follow the build guide
```

---

## 🛡️ Protection System

**This isn't your average DIY project.** Full protection chain:

```
Battery → Anti-reverse → TVS → Crowbar → Soft-start → Fuse → Filter → Amp
                           ↓
                    Wrong charger?
                    Circuit survives.
                    Just replace fuse.
```

| Threat | Protection | Result |
|--------|------------|--------|
| Reversed battery | Schottky diode | No damage |
| 24V laptop charger | SCR crowbar | Fuse blows, circuit OK |
| Voltage spikes | TVS 1500W | Clamped |
| Inrush current | NTC limiter | Soft start |
| Speaker pop | Delayed relay | Silent |

---

## 📁 Documentation

| File | What's Inside |
|------|---------------|
| [`Circuit_V2.1.md`](docs/Circuit_V2.1.md) | Full schematic, BOM, calculations |
| [`Breakout_V3.1.md`](docs/Breakout_V3.1.md) | Debug box with 7 test points |
| [`Build_Guide.md`](docs/Build_Guide.md) | Step-by-step assembly |
| [`Testing.md`](docs/Testing.md) | Validation procedures |

---

## 🖼️ Gallery

<p align="center">
  <img src="docs/images/build-01.jpg" width="280" alt="Step 1">
  <img src="docs/images/build-02.jpg" width="280" alt="Step 2">
  <img src="docs/images/build-03.jpg" width="280" alt="Step 3">
</p>

<p align="center"><em>Built one? <a href="#contributing">Add your photos!</a></em></p>

---

## 💰 Cost Breakdown

| Item | Price |
|------|-------|
| Arylic Up2Stream Amp V4 | €65 |
| 4S Battery 6Ah + BMS | €60 |
| All components | €25 |
| Vintage speaker | €10-50 |
| **Total** | **€160-200** |

> *Less than a Sonos Move. Better sound. You built it.*

---

## 🔊 Speaker Compatibility

| Impedance | Mode | Power |
|-----------|------|-------|
| 4Ω | Stereo (L only) | 50W |
| 6Ω | Stereo (L only) | 50W |
| 8Ω | Mono Bridge | 100W |

---

## 🤝 Contributing

- 🐛 **Bug?** → [Open issue](../../issues)
- 💡 **Idea?** → [Discussion](../../discussions)  
- 📸 **Built one?** → [PR with photos!](../../pulls)

---

## 📜 License

**MIT** — Use it, modify it, sell it. Just give credit.

---

<p align="center">
  <strong>If this helped you, drop a ⭐</strong>
</p>

<p align="center">
  <a href="../../stargazers">
    <img src="https://img.shields.io/github/stars/YOUR_USERNAME/vintage-bluetooth-speaker?style=social" alt="Stars">
  </a>
  <a href="../../network/members">
    <img src="https://img.shields.io/github/forks/YOUR_USERNAME/vintage-bluetooth-speaker?style=social" alt="Forks">
  </a>
</p>

---

<p align="center">Made with 🔊 by Mehdi</p>
