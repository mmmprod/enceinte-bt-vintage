# 📚 Documentation

> Complete technical documentation for the Vintage Bluetooth Speaker project.

---

## 📋 Index

### Core Documents

| Document | Description | Version |
|----------|-------------|---------|
| [**Circuit_V2.1.md**](Circuit_Enceinte_BT_Vintage_V2_1.md) | Full schematic + BOM | v2.1 |
| [**Breakout_V3.1.md**](Breakout_Box_Enceinte_BT_V3_1.md) | Debug box design | v3.1 |

### Guides

| Guide | Description |
|-------|-------------|
| [Build Guide](Build_Guide.md) | Step-by-step assembly |
| [Testing](Testing.md) | Validation procedures |
| [Troubleshooting](Troubleshooting.md) | Common problems & fixes |

---

## 🔌 Block Diagram

```
┌─────────┐    ┌─────────┐    ┌─────────┐    ┌──────────┐
│ BATTERY │───▶│ PROTECT │───▶│  SOFT   │───▶│  FILTER  │
│   4S    │    │  CHAIN  │    │  START  │    │    LC    │
└─────────┘    └─────────┘    └─────────┘    └──────────┘
                                                   │
┌─────────┐    ┌─────────┐    ┌─────────┐         │
│ SPEAKER │◀───│  RELAY  │◀───│ ANTI-POP│◀────────┤
│         │    │  K_HP   │    │  LM393  │         │
└─────────┘    └─────────┘    └─────────┘         │
                                                   ▼
                                            ┌──────────┐
                                            │  ARYLIC  │
                                            │  MODULE  │
                                            └──────────┘
```

---

## ⚡ Protection Chain

```
                    ┌──────────────────────────────────────┐
                    │         PROTECTION CHAIN V2.1        │
                    └──────────────────────────────────────┘
                    
BATT+ ──▶ D1 ──▶ TVS ──▶ CROWBAR ──▶ Q_SS ──▶ SW1 ──▶ F1 ──▶ NTC ──▶ LC
          │       │        │          │                │
          │       │        │          │                │
       Reverse  Spike   Wrong     Soft-start       Fuse
       Block    Clamp   Charger   300ms            6.3A
```

| Stage | Component | Function |
|-------|-----------|----------|
| D1 | SB560 | Blocks reverse polarity |
| TVS | 1.5KE22CA | Clamps transients to 35V |
| CROWBAR | SCR + Zener | Shorts >18V → blows fuse |
| Q_SS | IRF9540N | 300ms soft-start |
| F1 | 6.3A Slow | Overcurrent protection |
| NTC | 2.5Ω | Limits inrush to 6A |
| LC | 10µH + 4700µF | Filters noise |

---

## 🔧 Key Specs

### Power

| Parameter | Value |
|-----------|-------|
| Input voltage | 12-16.8V |
| Quiescent current | <20mA |
| Max current | 5A |
| Inrush (limited) | 6A |

### Audio

| Parameter | Value |
|-----------|-------|
| Output power | 2×50W / 1×100W |
| THD+N | <0.1% |
| SNR | >95dB |
| Frequency response | 20Hz-20kHz |

### Protection

| Threat | Trigger | Action |
|--------|---------|--------|
| Reverse polarity | Immediate | Blocked |
| Overvoltage >18V | 20V | Crowbar → Fuse |
| Overcurrent | >12.6A | Fuse blows |
| Speaker pop | <300ms | Relay open |

---

## 📊 Version History

| Version | Date | Changes |
|---------|------|---------|
| **2.1** | Dec 2025 | Crowbar protection, TVS upgrade, hysteresis |
| 2.0 | Dec 2025 | Soft-start, anti-pop, LC filter |
| 1.x | Nov 2025 | Initial development |

### V2.1 Changelog

- ✅ TVS upgraded: 1.5KE18CA → 1.5KE22CA
- ✅ Added SCR crowbar (wrong charger protection)
- ✅ Added hysteresis to comparator (300mV)
- ✅ Relay resistor added (prevents overheat)
- ✅ Breakout box: triple protection + TVS

---

## 🧪 Testing Checklist

```
□ No short circuits (continuity test)
□ Voltages within spec (multimeter)
□ Soft-start ramp visible (scope/DMM)
□ Zero pop on ON/OFF (ears)
□ Crowbar triggers at 20V (lab supply)
□ Thermal OK after 1h (touch test)
```

---

## 📸 Add Your Build

Built the project? Add your photos!

1. Fork this repo
2. Add images to `docs/images/community/`
3. Submit a PR

---

## ❓ FAQ

**Q: Can I use a different amplifier module?**  
A: Yes, but adjust voltage specs. Most Class D amps work with 12-24V.

**Q: 4Ω vs 8Ω speaker?**  
A: 4Ω = stereo mode (one channel), 8Ω = mono bridge (full power).

**Q: How long does the battery last?**  
A: 6Ah pack = ~10h at medium volume.

**Q: What if I use a wrong charger?**  
A: Crowbar triggers, fuse blows, circuit survives. Replace fuse.

---

<p align="center">
  <a href="../README.md">← Back to main README</a>
</p>
