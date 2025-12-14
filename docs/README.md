# DOCUMENTATION TECHNIQUE V2.1 — INDEX

**Projet:** Enceinte Bluetooth Vintage
**Version Documentation:** 2.1
**Date:** Decembre 2025

---

## INDEX DES FICHIERS

### Documentation Circuit

| Fichier | Version | Lignes | Description |
|---------|---------|--------|-------------|
| Circuit_Enceinte_BT_Vintage_V2_1.md | 2.1 | 693 | **ACTUEL** - Schema + BOM + Guide |
| Circuit_Enceinte_BT_Vintage_V2_0.md | 2.0 | 893 | Soft-start + anti-pop |
| Circuit_Enceinte_BT_Vintage_V1_10.md | 1.10 | - | Corrections audit V2 |
| Circuit_Enceinte_BT_Vintage_V1_9.md | 1.9 | - | Archive |
| Circuit_Enceinte_BT_Vintage_V1_8.md | 1.8 | - | Archive |

### Documentation Breakout Box

| Fichier | Version | Lignes | Description |
|---------|---------|--------|-------------|
| Breakout_Box_Enceinte_BT_V3_1.md | 3.1 | 606 | **ACTUEL** - Triple protection |
| Breakout_Box_Enceinte_BT_V2_0.md | 2.0 | - | R_sense integrees |
| Breakout_Box_Enceinte_BT_V1_6.md | 1.6 | - | Archive |

### README

| Fichier | Description |
|---------|-------------|
| README_V2.1.md | Guide utilisateur principal |
| docs_README_V2.1.md | Ce fichier (index technique) |

---

## CHANGELOG COMPLET

### V2.1 (Decembre 2025) — CURRENT

**Origine:** Audit externe V3 (Hardware + Breakout)

**Corrections Circuit:**

| # | Bloc | Modification | Raison |
|---|------|--------------|--------|
| 1 | A.2 | TVS 1.5KE18CA → 1.5KE22CA | V_RWM=15.3V < V_batt=16.8V |
| 2 | A.3 | NOUVEAU: Crowbar SCR | Protection chargeur 19-24V |
| 3 | B.2 | Ajout R_pulldown 100k | Marge gate Q_SS |
| 4 | E.1 | L1 specifie: Wurth 74435588100 | I_sat=13A, DCR=8m ohm |
| 5 | E.2 | C_filt specifie: Panasonic FM | ESR=28m ohm, 105C |
| 6 | F.3 | Ajout R_fb 1M (hysteresis) | Anti-chattering 300mV |
| 7 | F.4 | Ajout R_serie_bobine 150 ohm | Protege bobine @ 16.8V |

**Corrections Breakout:**

| # | Modification | Raison |
|---|--------------|--------|
| 1 | R_sense 1k → 2.2k | Marge thermique 88% vs 44% |
| 2 | Ajout R_limit 100 ohm | Backup si R_sense ouverte |
| 3 | Ajout PolySwitch 100mA | Limite absolue court-circuit |
| 4 | Ajout TVS SMAJ18CA x7 | ESD 8kV + inversion |
| 5 | Ajout C_filt 100nF x7 | Filtrage HF -60dB |
| 6 | Borniers → JST-XH | Anti-vibration |
| 7 | Ajout LED temoin | Indication tension presente |
| 8 | Paires torsadees | Rejection mode commun |

### V2.0 (Decembre 2025)

**Origine:** Refonte architecture plug & play

**Ajouts majeurs:**
- Soft-start P-MOSFET (IRF9540N)
- Circuit anti-pop (TL431 + LM393 + relais)
- Filtre LC (L1 10uH + C_filt 4700uF)
- Snubber arc suppression (RC)
- Protection Zener gate

**Philosophie:**
- Zero configuration utilisateur
- ON/OFF/CHARGER = seules actions
- Protection complete automatique

### V1.10 (Novembre 2025)

**Origine:** Audit V2

**Corrections:**
- Cold crank 6V valide
- Reference TL431 stable
- Calculs thermiques complets
- Hysteresis comparateur

### V1.0-1.9 (Novembre 2025)

**Evolution initiale:**
- V1.0: Concept initial
- V1.5: Protection TVS
- V1.7: Optimisation BOM
- V1.9: Corrections mineures

---

## ARCHITECTURE V2.1

### Diagramme Bloc

```
BATTERIE 4S
    │
    ├─→ [D1 Anti-inversion] ─→ [TVS Surtension] ─→ [CROWBAR Chargeur]
    │                                                      │
    │                                              [Q_SS Soft-start]
    │                                                      │
    │                                              [SW1 ON/OFF]
    │                                                      │
    │                                              [F1 Fusible]
    │                                                      │
    │                                              [NTC Inrush]
    │                                                      │
    │                                              [L1+C Filtre]
    │                                                      │
    │   ┌──────────────────────────────────────────────────┤
    │   │                                                  │
    │   │  [TL431 Ref] ─→ [LM393 Comp] ─→ [K_HP Relais]   │
    │   │                                       │          │
    │   │                                      HP      MODULE
    │   │                                              ARYLIC
    │   └──────────────────────────────────────────────────┘
    │
BREAKOUT BOX (7 TP)
```

### Flux Signal

```
1. BATTERIE → D1 (anti-inversion)
2. D1 → TVS1 (protection transitoire)
3. TVS1 → CROWBAR (protection chargeur)
4. CROWBAR → Q_SS (soft-start 300ms)
5. Q_SS → SW1 (ON/OFF manuel)
6. SW1 → F1 (fusible 6.3A)
7. F1 → NTC1 (limite inrush)
8. NTC1 → L1+C_filt (filtre LC)
9. L1 → MODULE (alimentation)
10. MODULE → K_HP (via anti-pop) → HP
```

### Flux Protection

```
SCENARIO: Chargeur 24V branche par erreur

1. V_entree = 24V arrive sur circuit
2. D_zener 20V conduit (24V > 20V)
3. I_gate SCR = (24-20)/1k = 4mA
4. SCR s'amorce (I_gt = 0.2mA)
5. Court-circuit V_D1 → GND
6. I_cc ~ 48A (limite chargeur)
7. Fusible F1 fond en < 10ms
8. Circuit protege, fusible a remplacer
```

---

## SPECIFICATIONS DETAILLEES

### Tensions Nominales

| Point | Min | Typ | Max | Notes |
|-------|-----|-----|-----|-------|
| V_BATT | 12.0V | 14.8V | 16.8V | 4S Li-ion |
| V_D1 | 11.5V | 14.3V | 16.3V | Apres Schottky |
| V_SOFT | 0→V_D1 | - | - | Rampe 300ms |
| V_PROT | 11.5V | 14.3V | 16.3V | Apres fusible |
| V_FILT | 11.5V | 14.3V | 16.3V | Apres filtre |
| V_REF | 2.45V | 2.50V | 2.55V | TL431 |

### Courants

| Point | Typ | Max | Notes |
|-------|-----|-----|-------|
| I_repos | 10mA | 20mA | Module standby |
| I_moyen | 500mA | 1A | Volume moyen |
| I_max | 3A | 5A | Volume max |
| I_inrush | - | 6A | Limite NTC |
| I_cc | - | 12.6A | Fusion fusible |

### Temperatures

| Composant | Max continu | Critique |
|-----------|-------------|----------|
| D1 (SB560) | 80C | 100C |
| Q_SS (IRF9540N) | 60C | 80C |
| L1 | 50C | 70C |
| C_filt | 50C | 70C |
| K_HP bobine | 60C | 80C |

---

## CALCULS CRITIQUES

### Protection Crowbar

```
Seuil declenchement:
V_trigger = V_zener + V_gt = 20V + 0.8V = 20.8V

Courant gate @ 24V:
I_gate = (24V - 20V) / 1k = 4mA >> 0.2mA (I_gt) OK

Temps fusion fusible:
I_cc = V_chargeur / R_int = 24V / 0.5 = 48A
Fusible 6.3A: t_fusion < 10ms @ 48A

Marge securite:
V_normal_max = 16.8V < 20V (seuil) = 3.2V marge OK
```

### Hysteresis Comparateur

```
R_parallele = R_div1 // R_div2 = 100k // 27k = 21.3k
V_swing = V_PROT = 14V (open collector)

Hysteresis = V_swing x R_parallele / R_fb
Hysteresis = 14V x 21.3k / 1M = 298mV ~ 300mV

Seuil haut: 11.76V + 150mV = 11.91V
Seuil bas:  11.76V - 150mV = 11.61V
```

### Thermique Relais

```
Sans R_serie @ 16.8V:
I = 16.8V / 400 ohm = 42mA
P = 16.8V x 42mA = 706mW > 500mW nominal = SURCHAUFFE

Avec R_serie 150 ohm @ 16.8V:
I = 16.8V / 550 ohm = 30.5mA = nominal OK
P_bobine = 30.5mA x 30.5mA x 400 = 372mW OK
P_R_serie = 30.5mA x 30.5mA x 150 = 140mW < 500mW OK
```

### Triple Protection Breakout

```
Mode normal:
I = 16.8V / 2.2k = 7.6mA
P = 7.6mA x 7.6mA x 2.2k = 0.127W < 0.5W OK

R_sense ouverte:
I = 16.8V / 100 ohm = 168mA
PolySwitch 100mA declenche OK

Court-circuit TP:
I_max = 168mA (limite PolySwitch)
Pas de dommage circuit principal
```

---

## TESTS VALIDATION

### Tests Obligatoires V2.1

| # | Test | Critere GO | Critere NO-GO |
|---|------|------------|---------------|
| 1 | Crowbar | Fusible fond @ 20V | Pas de reaction @ 24V |
| 2 | Soft-start | Rampe 200-500ms | Instantane |
| 3 | Anti-pop | 0 pop sur 5 cycles | Pop audible |
| 4 | Thermique D1 | T < 80C @ 1h | T > 90C |
| 5 | Thermique relais | T < 60C @ 1h | T > 70C |
| 6 | Ripple audio | < 10mVpp | > 50mVpp |
| 7 | Hysteresis | Stable @ 11.7V | Chattering |

### Procedure Test Crowbar

```
ATTENTION: Ce test detruit le fusible!

1. Deconnecter batterie
2. Alimentation labo sur J_charge
3. Limite courant 1A
4. Monter tension:
   - 12V: Normal
   - 16V: Normal
   - 18V: Normal
   - 20V: SCR declenche, fusible fond

Si fusible ne fond pas @ 24V:
→ SCR ou Zener defaillant
→ Remplacer et retester
```

---

## DEPANNAGE

### Arbre Decision

```
PROBLEME: Circuit ne demarre pas

  TP1 = 0V?
  ├─ OUI → Batterie HS ou deconnectee
  └─ NON → TP1 = 12-17V
            │
            TP2 = 0V?
            ├─ OUI → D1 inverse ou HS
            └─ NON → TP2 = TP1 - 0.5V
                      │
                      TP4 = 0V (SW1=ON)?
                      ├─ OUI → F1 fondu ou SW1 HS
                      └─ NON → TP4 = TP2
                                │
                                Son OK?
                                ├─ NON → Verifier K_HP, LM393
                                └─ OUI → Circuit OK
```

### Codes Erreur (Breakout)

| LED | TP4 | TP6 | Signification |
|-----|-----|-----|---------------|
| OFF | 0V | - | Pas d'alimentation |
| ON | OK | 0V | Batterie trop basse |
| ON | OK | 14V | Relais commande OK |
| Clignote | - | - | BMS protection |

---

## REFERENCES

### Datasheets Composants Critiques

| Composant | Fabricant | Reference |
|-----------|-----------|-----------|
| SB560 | ON Semi | SB560-E3/54 |
| 1.5KE22CA | Littelfuse | 1.5KE22CA |
| IRF9540N | Infineon | IRF9540NPBF |
| LM393 | TI | LM393P |
| TL431 | TI | TL431ACLP |
| HF46F-12 | Hongfa | HF46F-12-HS1 |
| MCP41100 | Microchip | - |

### Protocole Premortem

Ce projet suit le protocole PREMORTEM V3.8+:
- Module 0: Detection composants critiques
- Module 4: Protections par type
- Module 4.2: Driver MOSFET + Zener
- Module 11: Anti-surinfection
- Module 12: Anti-troncature

---

## CONTACT

Questions techniques: Consulter documentation
Bugs: Signaler avec numero version + symptome

---

**FIN DOCUMENTATION TECHNIQUE V2.1**
