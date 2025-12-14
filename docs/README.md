# 📚 Documentation

**Everything you need to build your vintage Bluetooth speaker.**

---

## 📋 Documents

| Document | Version | Description |
|----------|---------|-------------|
| [Circuit](Circuit_Enceinte_BT_Vintage_V1_9.md) | V1.9 | Complete build guide — BOM, wiring, step-by-step |
| [Breakout Box](Breakout_Box_Enceinte_BT_V1_5.md) | V1.5 | Test jig — Protected sense lines (fire-safe) |
| Test Protocol | *Soon* | Validation procedures |

---

## 🗂️ Document Structure

### Circuit V1.6

| Section | What you'll find |
|---------|------------------|
| Parts list | Everything to order with search terms |
| Up2Stream config | How to set MONO mode (jumpers) |
| Protection board | Soldering order, connections |
| Wiring | All cables with lengths and colors |
| Breakout integration | How to add test points |

### Breakout Box V1.2

| Section | What you'll find |
|---------|------------------|
| Components | 7 terminal blocks, 1 enclosure |
| Build order | Drill → Mount → Wire → Label |
| Internal wiring | Every connection explained |
| Test points | What voltage to expect at each point |

---

## 🔢 Version History

| Version | Date | Changes |
|---------|------|---------|
| V1.9 | Dec 2025 | Fire safety: R_sense 10kΩ on breakout lines, C_snub 100V film |
| V1.8 | Dec 2025 | Certified audit: PTC removed, SW1 snubber, IND1 before SW1, NTC 10mm, HP DCR threshold |
| V1.7 | Dec 2025 | Full audit fixes: anti-reverse diode, TVS 22CA, PTC 5A, fuse 6.3A, decoupling, HP check |
| V1.6 | Dec 2025 | Explicit refs in parentheses, clear build order |
| V1.5 | Dec 2025 | Breakout box integration |
| V1.4 | Dec 2025 | Table format, veroboard |
| V1.3 | Dec 2025 | External charger, pre-built battery |
| V1.2 | Dec 2025 | MONO mode |
| V1.1 | Dec 2025 | Explicit format |
| V1.0 | Dec 2025 | Initial version |

---

## 🛠️ How to Use

1. **Read Circuit V1.6 first** — Understand the full system
2. **Order parts** — Use the search terms provided
3. **Build in order** — Follow "Tu commences par" / "Tu finis par"
4. **Optional: Build Breakout Box** — For easier debugging
5. **Test** — Protocol coming soon

---

## 📝 Language Note

Documents are in **French** (original build notes). 

Key terms translation:

| French | English |
|--------|---------|
| Tu commences par | You start with |
| Tu finis par | You end with |
| Bornier | Terminal block |
| Fil | Wire |
| Souder | Solder |
| Brancher | Connect |
| Entree | Input |
| Sortie | Output |

---

**Happy building! 🔧**
