# 📚 DOCUMENTATION TECHNIQUE V2.0

**Projet:** Enceinte Bluetooth Vintage
**Version:** 2.0
**Date:** Decembre 2024

---

## 📋 TABLE DES MATIERES

1. [Architecture V2.0](#architecture-v20)
2. [Chaine de protection](#chaine-de-protection)
3. [Soft-start P-MOSFET](#soft-start-p-mosfet)
4. [Circuit anti-pop](#circuit-anti-pop)
5. [Filtre LC charge](#filtre-lc-charge)
6. [Gestion thermique](#gestion-thermique)
7. [Configuration HP](#configuration-hp)
8. [Historique versions](#historique-versions)
9. [Audits et corrections](#audits-et-corrections)

---

## 1. ARCHITECTURE V2.0

### Schema bloc complet

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                           CIRCUIT V2.0                                       │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  CHARGER+ ─── L1 ───┬─── C_filt ─── GND                                     │
│               10uH  │    4700uF                                              │
│                     │                                                        │
│  BATT+ ─────────────┴─── D1 ─── Q_SS ─── SW1 ─── F1 ─── NTC ─── V_PROT     │
│                        SB560  IRF9540         6.3A   2.5R/10A    │          │
│                                                                   │          │
│                                                              ┌────┴────┐     │
│                                                              │         │     │
│                                                           [ARYLIC]  [K_HP]   │
│                                                           [MODULE]  [RELAY]  │
│                                                              │         │     │
│                                                              └────┬────┘     │
│                                                                   │          │
│                                                                  HP          │
│                                                                              │
│  BATT- ══════════════════════════════════════════════════════════ GND       │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Flux de puissance

```
1. CHARGER ou BATTERIE
       ↓
2. FILTRE LC (si chargeur)
       ↓
3. D1 SB560 (anti-inversion)
       ↓
4. Q_SS IRF9540 (soft-start)
       ↓
5. SW1 (interrupteur principal)
       ↓
6. F1 6.3A (fusible)
       ↓
7. NTC 2.5R/10A (inrush limiter)
       ↓
8. V_PROT → TVS + Condensateurs + IND1
       ↓
9. MODULE ARYLIC
       ↓
10. K_HP RELAIS (anti-pop)
       ↓
11. HAUT-PARLEUR
```

---

## 2. CHAINE DE PROTECTION

### Tableau des protections

| Ordre | Composant | Protection | Reaction |
|-------|-----------|------------|----------|
| 1 | D1 SB560 | Inversion polarite | Bloque courant inverse |
| 2 | TVS 1.5KE18CA | Surtension >18V | Clampe a 25V |
| 3 | F1 6.3A | Court-circuit | Fond en <1s @ 15A |
| 4 | NTC 2.5R/10A | Inrush | Limite a 6A froid |
| 5 | Q_SS soft-start | Redemarrage rapide | Montee 500ms |
| 6 | K_HP relais | Pop audio | Coupe HP en 30ms |
| 7 | BMS pack | OCP/OVP/UVP | Coupe batterie |

### Scenarios de defaut

| Scenario | Protection active | Resultat |
|----------|-------------------|----------|
| Batterie inversee | D1 bloque | Rien ne se passe |
| Chargeur 24V | TVS clampe + F1 fond | Circuit protege |
| Court-circuit HP | F1 fond | Circuit protege |
| Redemarrage rapide | Q_SS soft-start | Demarrage OK |
| Extinction | K_HP coupe | Pas de pop |
| Stockage long | IND1 OFF | Zero drain |

---

## 3. SOFT-START P-MOSFET

### Probleme resolu

Sans soft-start, un redemarrage rapide (OFF/ON en <30s) avec NTC chaude cause:
- NTC chaude = R ≈ 0.3 ohm
- I_inrush = 14V / 0.3 = 47A
- BMS coupe (OCP 30A)
- Utilisateur confus

### Solution

P-MOSFET IRF9540 controle par RC:
- Montee progressive du courant sur 500ms
- Meme si NTC chaude, pas de pic brutal
- BMS ne coupe jamais

### Schema

```
V_D1 ─── S ──┬── D ─── V_SOFT
             │
         Q_SS (IRF9540)
             │
             G
             │
    ┌────────┼────────┐
    │        │        │
 R_pull   R_gate   C_gate
 (10k)    (47k)    (33uF)
    │        │        │
    │        └───┬────┘
    │            │
   V_D1      D_disch ─── SW1
```

### Calculs

```
tau = R_gate × C_gate = 47k × 33uF = 1.55s
Temps pour Vgs = -4V (seuil): t ≈ 0.3 × tau ≈ 500ms
Courant monte progressivement sur 500ms
```

---

## 4. CIRCUIT ANTI-POP

### Probleme resolu

A l'extinction, les condensateurs de l'ampli se dechargent via le HP, causant un "pop" audible.

### Solution

Relais K_HP coupe le HP AVANT que l'ampli fasse pop:
- Detection chute V_PROT par comparateur
- Seuil: 11.7V
- Temps de reaction: <30ms
- Pop arrive vers 50-100ms
- HP deconnecte AVANT pop

### Schema

```
V_PROT ─── R1 (100k) ───┬─── LM393 IN+
                        │
                    R2 (27k)
                        │
                       GND

TL431 (2.5V) ─── LM393 IN-

LM393 OUT ─── R3 (1k) ─── BC547 ─── Bobine K_HP
                                        │
                                    D_flyback
                                        │
                                       GND
```

### Calculs

```
Seuil = V_ref × (R1+R2)/R2 = 2.5V × 127k/27k = 11.7V

Temps de reaction:
- dV/dt ≈ 80 V/s (decharge condensateurs)
- Temps 14V → 11.7V = 2.3V / 80 = 29ms
- K_HP ouvre en 5ms supplementaires
- HP deconnecte a t = 34ms < 50ms (pop)
```

---

## 5. FILTRE LC CHARGE

### Probleme resolu

Charger pendant l'ecoute injecte du bruit 50Hz du chargeur.

### Solution

Filtre LC second ordre:
- L1 = 10uH
- C_filt = 4700uF
- f_coupure = 734Hz
- Attenuation @ 100Hz = 35dB

### Schema

```
CHARGER+ ─── L1 (10uH) ───┬─── C_filt (4700uF) ─── GND
                          │
BATT+ ────────────────────┘
```

### Calculs

```
f_c = 1 / (2π × sqrt(L × C))
f_c = 1 / (2π × sqrt(10uH × 4700uF))
f_c = 734 Hz

Attenuation @ 100Hz = 20 × log10((f_c/f)²)
= 20 × log10(53.9) = 34.6 dB

Ripple chargeur: 200mVpp
Apres filtre: 200mV / 54 = 3.7mVpp → INAUDIBLE
```

---

## 6. GESTION THERMIQUE

### Sources de chaleur

| Composant | P_diss | Notes |
|-----------|--------|-------|
| D1 SB560 | 3.5W @ 5A | Radiateur obligatoire |
| Q_SS IRF9540 | 1W | TO-220 nu suffit |
| Module Arylic | 5W | Pad + plaque alu |

### Solution thermique

```
1. D1: Petit radiateur TO-220 (10 degC/W)
2. Module: Pad thermique + plaque alu 100×100×3mm
3. Enceinte: Grilles aeration ≥ 50cm²
```

### Calculs

```
Module sans dissipateur:
Rth_enceinte ≈ 10 degC/W
Delta_T = 5W × 10 = 50 degC
T_interne @ 25C = 75 degC > 40C spec → SURCHAUFFE

Module avec dissipateur + grilles:
Rth_total ≈ 7 degC/W
Delta_T = 5W × 7 = 35 degC
T_interne @ 25C = 60 degC → OK (limite)
```

---

## 7. CONFIGURATION HP

### Pour le constructeur uniquement

L'utilisateur final n'a pas a toucher aux jumpers. C'est configure a la fabrication.

### Tableau de decision

| DCR mesure | Z nominale | Mode | Jumpers | Cablage |
|------------|------------|------|---------|---------|
| < 3.5 ohm | 4 ohm | STEREO | HAUT+MILIEU | L+ / L- |
| 3.5-5.5 ohm | 6 ohm | STEREO | HAUT+MILIEU | L+ / L- |
| > 5.5 ohm | 8 ohm+ | MONO PBTL | MILIEU+BAS | R+ / L+ |

### Pourquoi cette distinction?

```
Mode MONO PBTL:
- Les 2 canaux sont pontes en parallele
- Z vue par ampli = Z_HP / 2
- HP 4 ohm → Z vue = 2 ohm → TROP BAS
- HP 8 ohm → Z vue = 4 ohm → OK

Mode STEREO (1 canal):
- Un seul canal utilise
- Z vue = Z_HP
- HP 4 ohm → Z vue = 4 ohm → OK
```

---

## 8. HISTORIQUE VERSIONS

### V1.0 - V1.4 (Oct 2024)

- Conception initiale
- Ajout protections basiques

### V1.5 - V1.9 (Nov-Dec 2024)

- TVS 1.5KE18CA
- NTC 2.5R 7A
- Snubber SW1
- Securite incendie breakout

### V1.10 (Dec 2024)

- Corrections audit externe V2
- D1 → SB560 (5A reel)
- NTC → 7A
- Ajout C3 1000uF

### V2.0 (Dec 2024) - ACTUEL

- Refonte complete
- Soft-start P-MOSFET
- Relais anti-pop
- Filtre LC charge
- IND1 apres SW1
- NTC 10A
- Dissipateur integre

---

## 9. AUDITS ET CORRECTIONS

### Audit V1 (Nov 2024)

| Point | Severite | Correction |
|-------|----------|------------|
| D1 sous-dim | Critique | 1N5822 → SB560 |
| NTC limite | Majeur | 5A → 7A |
| Snubber absent | Majeur | Ajout RC 47R+100nF |

### Audit V2 (Dec 2024)

| Point | Severite | Correction V1.10 | Correction V2.0 |
|-------|----------|------------------|-----------------|
| Thermique 40C | Critique | Warning | Dissipateur |
| Mauvais chargeur | Critique | Warning XT60 | Connecteur detrompe |
| Charge+ecoute | Critique | Warning | Filtre LC |
| Redemarrage | Majeur | Warning 30s | Soft-start |
| Pop extinction | Majeur | "Normal" | Relais K_HP |
| IND1 drain | Majeur | Warning deconnexion | IND1 apres SW1 |
| HP 4 ohm | Majeur | Interdit | Mode STEREO |

### Philosophie V2.0

```
V1.x: "Warning-driven design"
      → L'utilisateur doit suivre des regles
      → Risque d'erreur humaine

V2.0: "Solution-driven design"
      → Le circuit gere tout
      → Zero contrainte utilisateur
```

---

## 📁 FICHIERS DU PROJET

| Fichier | Description |
|---------|-------------|
| Circuit_Enceinte_BT_Vintage_V2_0.md | Schema complet + BOM |
| Breakout_Box_Enceinte_BT_V2_0.md | Outil diagnostic |
| README.md | Presentation projet |
| docs/README.md | Ce fichier |

---

## ⚠️ NOTES IMPORTANTES

1. **Toujours utiliser la derniere version** du circuit
2. **Ne pas melanger** composants de versions differentes
3. **Breakout V2.0** incompatible avec Circuit V1.x
4. **Tester systematiquement** avant livraison client

---

**FIN DOCUMENTATION TECHNIQUE V2.0**
