# 📁 Documentation - Vintage Bluetooth Speaker

## 📋 Latest Versions

| Document | Version | Status |
|----------|---------|--------|
| **Circuit** | [V1.10](Circuit_Enceinte_BT_Vintage_V1_10.md) | ✅ Current |
| **Breakout Box** | [V1.6](Breakout_Box_Enceinte_BT_V1_6.md) | ✅ Current |

---

## 🔄 Version History

### Circuit Enceinte BT Vintage

| Version | Date | Key Changes |
|---------|------|-------------|
| **V1.10** | Dec 2025 | **External audit V2**: D1→SB560(5A real), NTC→7A, C3 1000µF bulk, power 30W (not 60W), R_sense 1kΩ |
| V1.9 | Dec 2025 | Fire-safe breakout: R_sense 10kΩ, snubber 100V film |
| V1.8 | Dec 2025 | Certified audit: PTC removed, snubber added, IND1 before SW1, NTC 10mm raised |
| V1.7 | Dec 2025 | D1 reverse protection, TVS P6KE22CA, decoupling, ferrite |
| V1.6 | Dec 2025 | Explicit refs, clear order |
| V1.5 | Dec 2025 | DCR check, mono PBTL |
| V1.4 | Dec 2025 | BMS managed pack |
| V1.3 | Dec 2025 | Inrush NTC 2.5Ω |
| V1.2 | Dec 2025 | TVS 1.5KE18CA added |
| V1.1 | Dec 2025 | PTC added (later removed) |
| V1.0 | Dec 2025 | Initial version |

### Breakout Box

| Version | Date | Key Changes |
|---------|------|-------------|
| **V1.6** | Dec 2025 | R_sense 1kΩ 0.5W (industry standard) |
| V1.5 | Dec 2025 | R_sense 10kΩ fire-safe |
| V1.4 | Dec 2025 | Direct wires (DANGEROUS - do not use) |

---

## ⚠️ Important Notes

### Why V1.10?

External audit identified critical issues:

| Issue | Problem | Fix |
|-------|---------|-----|
| D1 1N5822 | Rated 3A, system needs 5A | → SB560 (5A real) |
| NTC 5A | At ceiling, accelerated aging | → NTC 7A |
| Power "60W" | False (needs 24V, we have 14.8V) | → 30W typ |
| Bass brownout | No bulk cap near amp | → C3 1000µF |
| R_sense 10kΩ | Works but not industry standard | → 1kΩ 0.5W |

### Breakout Box Safety

| Version | Short-circuit risk | Status |
|---------|-------------------|--------|
| V1.4 | 200A → FIRE HAZARD | ❌ DO NOT USE |
| V1.5+ | 17mA max (safe) | ✅ OK |

**V1.5+ requires Circuit V1.9+ with integrated R_sense resistors.**

---

## 📐 Block Diagram V1.10

```
BATT+ ─┬─ IND1+ (always on - disconnect if storing)
       │
       ├─ R_s1 (1kΩ) ─── TP1 ═══ Breakout V_BATT
       │
       └─ J1+ → D1(SB560) ─┬─ R_s2 (1kΩ) ─── TP2 ═══ Breakout V_D1
                           │
                           └─ [SW1 // Snubber] → F1 ─┬─ R_s3 (1kΩ) ─── TP3
                                    │                │
                               47Ω+100nF(100V)       └─ NTC1(7A) → J2+ ─┬─ R_s4 ─ TP4
                                                                        │
                                                                        └─ C3(1000µF) → AMP

BATT- ── J1- ── TP_GND ═══════════════════════════════════════════════ J2- → AMP
                                                                  TVS + C1 + C2
```

---

## 🛡️ Protection Chain V1.10

| Fault | Protection | Response |
|-------|------------|----------|
| Reverse polarity | D1 SB560 blocks | Instant |
| Overvoltage >22V | TVS P6KE22CA clamps | <1µs |
| Overcurrent | F1 6.3A fuse | 10ms-2s |
| Inrush | NTC 2.5Ω 7A limits | 50ms |
| Switch arc | 47Ω+100nF snubber | 5µs |
| Bass brownout | C3 1000µF absorbs | Continuous |
| Breakout short | R_sense 1kΩ limits to 17mA | Instant |

---

## 📖 How to Use

1. **Start with Circuit V1.10** — Main build guide
2. **Check speaker impedance** — Must be ≥ 5.5Ω DCR
3. **Configure Up2Stream** — Jumpers to MONO
4. **Build protection board** — Follow step by step
5. **Optional: Build Breakout V1.6** — For debugging

---

**Always use latest versions. Older versions may have safety issues.**
