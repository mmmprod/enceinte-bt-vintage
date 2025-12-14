# CIRCUIT ENCEINTE BLUETOOTH VINTAGE V2.1

**Version:** 2.1
**Date:** Decembre 2025
**Auteur:** Mehdi
**Statut:** RELEASE CANDIDATE

---

## CHANGELOG V2.1

| Version | Date | Modifications |
|---------|------|---------------|
| V2.1 | Dec 2025 | Corrections audit V3: TVS 22V, crowbar SCR, hysteresis LM393, specs L1/C_filt |
| V2.0 | Dec 2025 | Soft-start P-MOS, relais anti-pop, filtre LC, plug & play |
| V1.10 | Dec 2025 | Corrections audit V2 partielles |

### Corrections V2.1 vs V2.0

| # | Probleme V2.0 | Correction V2.1 |
|---|---------------|-----------------|
| 1 | TVS 1.5KE18CA V_RWM=15.3V < V_batt=16.8V | TVS 1.5KE22CA V_RWM=18.8V |
| 2 | Relais 12V avec V_batt=16.8V surchauffe | R_serie 150 ohm protege bobine |
| 3 | L1 I_sat non specifie | Wurth 74435588100 I_sat=13A |
| 4 | C_filt ESR inconnu | Panasonic FM ESR=28m ohm |
| 5 | LM393 sans hysteresis = chattering | R_fb 1M ohm = hysteresis 256mV |
| 6 | Mauvais chargeur 19-24V = destruction | Crowbar SCR coupe a 18V |
| 7 | Q_SS gate marge faible | R_pulldown 100k ajoute |

---

## SCHEMA BLOC V2.1

```
BATT 4S ─→ D1 ─→ TVS ─→ CROWBAR ─→ Q_SS ─→ SW1 ─→ F1 ─→ NTC ─→ FILTRE LC ─→ MODULE
 14.8V    SB560  22V     SCR       Soft    ON/    6.3A   10A    L1+C      Arylic
                                   Start   OFF                           Up2Stream
                                     │
                              ┌──────┴──────┐
                              │   ANTI-POP  │
                              │  LM393+K_HP │
                              └──────┬──────┘
                                     │
                                    HP
```

---

## BLOC A — PROTECTION ENTREE ET ANTI-INVERSION

### A.1 Diode Anti-Inversion

**Topologie:**
BATT+ → D1 anode (SB560)
D1 cathode → V_D1

**Composant:**
D1: SB560 Schottky 60V 5A TO-220
- Vf = 0.45V @ 5A (typ)
- Vf = 0.55V @ 5A (max, chaud)
- Tj_max = 150C
- Rth_jc = 2.5C/W
- Rth_ja = 50C/W (sans radiateur)

**Calcul thermique:**
P_diss = Vf x I = 0.55V x 5A = 2.75W (pire cas)
Sans radiateur: dT = 2.75W x 50C/W = 137.5C
Tj = 40C + 137.5C = 177.5C > 150C = SURCHAUFFE

**Solution thermique OBLIGATOIRE:**
Radiateur TO-220 Rth_sa = 10C/W
Rth_total = 2.5 + 0.5 + 10 = 13C/W
dT = 2.75W x 13C/W = 35.75C
Tj = 40C + 35.75C = 75.75C < 150C OK

**Composant radiateur:**
Radiateur: Aavid 577102B00000G ou equivalent TO-220

### A.2 Protection TVS

**Topologie:**
V_D1 → TVS1 anode (1.5KE22CA)
TVS1 cathode → GND

**Composant:**
TVS1: 1.5KE22CA bidirectionnelle
- V_RWM = 18.8V (standoff, zero courant)
- V_BR = 21.2V - 23.5V (breakdown)
- V_C = 35.6V @ 76A (clamp max)
- P_pp = 1500W @ 1ms

**Verification marge:**
V_batt_max = 16.8V (4S charge)
V_RWM = 18.8V
Marge = 18.8V - 16.8V = 2.0V OK
TVS ne conduit JAMAIS en fonctionnement normal

**Protection transitoire:**
Chargeur defectueux 24V:
V_entree = 24V > V_BR = 22V
TVS clampe, courant eleve
Si maintenu > 1s → crowbar prend le relais

### A.3 Protection Crowbar SCR (NOUVEAU V2.1)

**Topologie:**
V_D1 → R_crowbar1 (1k) → node_trigger
node_trigger → D_zener cathode (18V)
D_zener anode → GND
node_trigger → SCR1 gate (MCR100-6)
V_D1 → SCR1 anode
SCR1 cathode → GND
SCR1 gate → R_crowbar2 (100 ohm) → GND

**Composants:**
SCR1: MCR100-6 0.8A 400V TO-92
D_zener: 1N4747A 20V 1W (seuil 18V + marge)
R_crowbar1: 1k ohm 0.25W
R_crowbar2: 100 ohm 0.25W (pull-down gate)

**Fonctionnement:**
V_entree < 18V:
- D_zener bloquee (V < V_z)
- Gate SCR = 0V (via R_crowbar2)
- SCR OFF
- Courant passe normalement

V_entree > 20V (zener 20V + Vf):
- D_zener conduit
- I_gate = (V - 20V) / 1k
- @ 24V: I_gate = 4mA > I_gt (0.2mA typ)
- SCR s'amorce
- Court-circuit V_D1 → GND
- F1 (6.3A) fond en < 100ms
- Circuit protege

**Calcul temps fusion:**
I_court_circuit = V_chargeur / R_interne_chargeur
Chargeur 24V 2A: R_int ~ 0.5 ohm
I_cc ~ 48A (limite par chargeur)
Fusible 6.3A: fond en < 10ms @ 48A

---

## BLOC B — SOFT-START P-MOSFET

### B.1 MOSFET Principal

**Topologie:**
V_D1 → Q_SS source (IRF9540N)
Q_SS drain → V_SOFT
Q_SS gate → GATE_SS

**Composant:**
Q_SS: IRF9540N P-MOSFET
- Vds_max = -100V
- Id_max = -23A
- Rds_on = 0.117 ohm @ Vgs=-10V
- Vgs_th = -2V a -4V
- Qg = 71nC

### B.2 Circuit RC Soft-Start

**Topologie:**
V_D1 → R_pull (10k) → GATE_SS
GATE_SS → C_soft (33uF) → GND_SW1
GATE_SS → R_pulldown (100k) → GND (NOUVEAU V2.1)
GATE_SS → R_gate (47k) → SW1_IN

**Composants:**
R_pull: 10k ohm 0.25W
C_soft: 33uF 25V electrolytique
R_gate: 47k ohm 0.25W
R_pulldown: 100k ohm 0.25W (NOUVEAU V2.1)

**Calcul constante temps:**
R_eq = R_gate // R_pulldown = 47k // 100k = 32k ohm
tau = R_eq x C_soft = 32k x 33uF = 1.06s
t_montee (10%-90%) = 2.2 x tau = 2.3s
t_seuil (Vgs=-4V) ~ 350ms

**Verification R_pulldown:**
SW1 OFF:
- R_pull tire gate vers V_D1
- R_pulldown tire vers GND
- V_gate = V_D1 x 100k / (10k + 100k) = V_D1 x 0.91
- Vgs = 0.91 x V_D1 - V_D1 = -0.09 x V_D1 = -1.3V
- Vgs = -1.3V > Vgs_th = -2V → Q_SS OFF OK
- Marge de securite supplementaire vs V2.0

### B.3 Protection Zener Gate

**Topologie:**
GATE_SS → D_zener cathode (12V)
D_zener anode → V_D1

**Composant:**
D_zener: 1N4742A 12V 1W
- Limite Vgs a 12V max
- Protege gate (Vgs_max = +/-20V)

---

## BLOC C — INTERRUPTEUR PRINCIPAL ET SNUBBER

### C.1 Interrupteur

**Topologie:**
V_SOFT → SW1 pole commun
SW1 NO → F1_IN
SW1 NC → non connecte

**Composant:**
SW1: Interrupteur bipolaire 10A 250VAC
- Contact NO utilise
- Rating DC: 10A @ 30VDC minimum

### C.2 Snubber Arc Suppression

**Topologie:**
SW1 pole commun → R_snub (47 ohm) → C_snub (100nF) → F1_IN

**Composants:**
R_snub: 47 ohm 0.5W
C_snub: 100nF 250V film polypropylene (WIMA MKP ou KEMET R60)

**Note V2.1:** Film PP au lieu de MKT pour meilleure tenue aux impulsions

---

## BLOC D — FUSIBLE ET NTC

### D.1 Fusible Principal

**Topologie:**
F1_IN → F1 (6.3A) → F1_OUT

**Composant:**
F1: Fusible verre 5x20mm 6.3A temporise
- I_nominal = 6.3A
- I_fusion = 12.6A (2x nominal, < 10s)
- Pouvoir coupure: 35A @ 32VDC minimum

### D.2 NTC Inrush Limiter

**Topologie:**
F1_OUT → NTC1 → V_PROT

**Composant:**
NTC1: Epcos B57364S0259M 2.5 ohm 10A
- R @ 25C = 2.5 ohm
- I_max = 10A continu
- R @ regime (chaud) = 0.1 ohm

**Calcul inrush:**
Sans NTC: I_inrush = V_batt / ESR_capa = 14.8V / 0.03 = 493A
Avec NTC froide: I_inrush = 14.8V / 2.5 = 5.9A < BMS limit 15A OK

---

## BLOC E — FILTRE LC CHARGE

### E.1 Inductance Filtre

**Topologie:**
V_PROT → L1 → V_FILT

**Composant (SPECIFIE V2.1):**
L1: Wurth 74435588100
- L = 10uH +/-20%
- I_sat (30% drop) = 13A
- I_rms = 10.5A
- DCR = 8m ohm
- Package: 12x12x8mm

**Alternative:**
Bourns SRR1210-100M (10uH, 10A, 12m ohm)

### E.2 Condensateur Principal Filtre

**Topologie:**
V_FILT → C_filt+ (4700uF)
C_filt- → GND

**Composant (SPECIFIE V2.1):**
C_filt: Panasonic EEU-FM1E472
- C = 4700uF
- V = 25V
- ESR = 28m ohm @ 100kHz
- Ripple = 3.15A @ 105C
- Temp = 105C rated

**Calcul attenuation:**
f_c = 1 / (2 x pi x sqrt(L x C))
f_c = 1 / (2 x 3.14159 x sqrt(10uH x 4700uF))
f_c = 734 Hz

Attenuation @ 100Hz = 20 x log10(100/734) = -17dB (1er ordre)
Attenuation @ 50Hz = 20 x log10(50/734) = -23dB
Filtre LC 2eme ordre: doubler → -34dB @ 100Hz, -46dB @ 50Hz

### E.3 Decouplage HF

**Topologie:**
V_FILT → C_hf (100uF X7R) → GND

**Composant:**
C_hf: 100uF 25V X7R ceramique (ou 10x 10uF)
- Absorbe HF > 100kHz
- ESR ~ 5m ohm
- Complement electrolytiqueE

---

## BLOC F — CIRCUIT ANTI-POP (MODIFIE V2.1)

### F.1 Reference Tension

**Topologie:**
V_PROT → R_ref1 (10k) → V_REF_TL431
V_REF_TL431 → TL431 cathode
TL431 anode → GND
TL431 ref → V_REF_TL431
V_REF_TL431 → C_ref (100nF) → GND

**Composant:**
U_ref: TL431ACLP 2.5V reference
R_ref1: 10k ohm 0.25W
C_ref: 100nF X7R

**Calcul:**
I_TL431 = (V_PROT - 2.5V) / 10k = (14V - 2.5V) / 10k = 1.15mA
P_TL431 = 2.5V x 1.15mA = 2.9mW OK

### F.2 Diviseur Tension Mesure

**Topologie:**
V_PROT → R_div1 (100k) → V_DIV
V_DIV → R_div2 (27k) → GND

**Composants:**
R_div1: 100k ohm 1% 0.25W
R_div2: 27k ohm 1% 0.25W

**Calcul seuil:**
V_seuil_HP = V_REF x (R_div1 + R_div2) / R_div2
V_seuil_HP = 2.5V x (100k + 27k) / 27k = 11.76V

### F.3 Comparateur avec Hysteresis (MODIFIE V2.1)

**Topologie:**
V_DIV → LM393 pin3 (IN+)
V_REF_TL431 → LM393 pin2 (IN-)
LM393 pin1 (OUT) → COMP_OUT
COMP_OUT → R_fb (1M) → LM393 pin3 (IN+) (NOUVEAU V2.1)
V_PROT → R_pullup_comp (10k) → COMP_OUT

**Composants:**
U_comp: LM393P comparateur dual
R_pullup_comp: 10k ohm 0.25W
R_fb: 1M ohm 0.25W (NOUVEAU V2.1 - hysteresis)

**Calcul hysteresis V2.1:**
R_parallel_entree = R_div1 // R_div2 = 100k // 27k = 21.3k ohm
V_swing_sortie = V_PROT = 14V (open collector avec pullup)

Hysteresis = V_swing x R_parallel / R_fb
Hysteresis = 14V x 21.3k / 1M = 298mV ~ 300mV

Seuils reels:
V_haut = 11.76V + 150mV = 11.91V
V_bas = 11.76V - 150mV = 11.61V

Batterie doit descendre de 11.91V a 11.61V pour chattering
= 300mV de marge anti-rebond OK

### F.4 Driver Relais

**Topologie:**
COMP_OUT → R_base (4.7k) → Q1 base
Q1 emetteur → GND
Q1 collecteur → R_serie_bobine (150 ohm) (NOUVEAU V2.1)
R_serie_bobine → K_HP bobine-
K_HP bobine+ → V_PROT
K_HP bobine → D_flyback cathode (1N4148)
D_flyback anode → GND

**Composants:**
Q1: BC547B NPN
R_base: 4.7k ohm 0.25W
R_serie_bobine: 150 ohm 0.5W (NOUVEAU V2.1)
D_flyback: 1N4148

**Calcul R_serie V2.1:**
Bobine relais HF46F-12: R_bobine = 400 ohm (typ)
I_nominal = 12V / 400 = 30mA
P_nominal = 360mW

Sans R_serie @ 16.8V:
I = 16.8V / 400 = 42mA (+40%)
P = 706mW → surchauffe

Avec R_serie 150 ohm @ 16.8V:
R_total = 400 + 150 = 550 ohm
I = 16.8V / 550 = 30.5mA = nominal OK
P_bobine = (30.5mA)^2 x 400 = 372mW OK
P_R_serie = (30.5mA)^2 x 150 = 140mW < 500mW OK

@ V_batt_min = 12V:
I = 12V / 550 = 21.8mA
Force maintien = 21.8/30 = 73% nominal → OK (relais deja enclenche)

### F.5 Relais HP

**Topologie:**
K_HP COM → HP+_MODULE
K_HP NO → HP+_OUT
K_HP NC → non connecte

**Composant:**
K_HP: HF46F-12-HS1 ou equivalent
- Bobine 12V nominal
- Contact 5A @ 30VDC
- Temps reponse: 10ms (ON), 5ms (OFF)

---

## BLOC G — INDICATEUR LED

### G.1 LED Power

**Topologie:**
V_PROT → R_led (1k) → LED1 anode
LED1 cathode → GND

**Composants:**
LED1: LED verte 3mm 20mA
R_led: 1k ohm 0.25W

**Calcul:**
I_led = (14V - 2V) / 1k = 12mA OK

---

## BLOC H — CONNEXION MODULE ARYLIC

### H.1 Alimentation Module

**Topologie:**
V_FILT → VCC module Arylic
GND → GND module Arylic

**Decouplage (< 1cm du module):**
VCC → C_dec1 (100nF X7R) → GND
VCC → C_dec2 (10uF X5R) → GND
VCC → FB1 (ferrite 600 ohm @ 100MHz) → VCC_module

**Composants:**
C_dec1: 100nF 25V X7R ceramique
C_dec2: 10uF 25V X5R ceramique
FB1: Ferrite bead 600 ohm @ 100MHz (BLM18PG601SN1)

### H.2 Sortie HP

**Topologie:**
HP+_OUT → HP+ haut-parleur
HP-_OUT → HP- haut-parleur

**Filtrage EMI (optionnel):**
HP+ → Ferrite clip → HP+ haut-parleur
HP- → Ferrite clip → HP- haut-parleur
HP+ → C_y1 (100nF Y2) → Chassis GND
HP- → C_y2 (100nF Y2) → Chassis GND

---

## BLOC J — CONNECTEURS

### J.1 Entree Batterie

**Topologie:**
BATT+ → Connecteur XT60 male pin+
BATT- → Connecteur XT60 male pin-

**Composant:**
J_batt: XT60 male chassis

### J.2 Entree Chargeur

**Topologie:**
CHARGER+ → J_charge pin+ → D1 anode (via batterie/BMS)
CHARGER- → J_charge pin-

**Composant:**
J_charge: Barrel jack 5.5x2.1mm femelle chassis

**Chargeur fourni:**
Chargeur 16.8V 2A barrel jack 5.5x2.1mm centre positif
Marquage enceinte: "UNIQUEMENT chargeur 16.8V fourni"

### J.3 Sortie HP

**Topologie:**
HP+_OUT → Bornier a vis 2 positions
HP-_OUT → Bornier a vis 2 positions

---

## BOM COMPLETE V2.1

### Semiconducteurs

| Ref | Composant | Valeur | Package | Qte | Prix unit | Total |
|-----|-----------|--------|---------|-----|-----------|-------|
| D1 | SB560 | Schottky 60V 5A | TO-220 | 1 | 0.80 | 0.80 |
| TVS1 | 1.5KE22CA | TVS 22V 1500W | DO-201 | 1 | 1.20 | 1.20 |
| D_zener1 | 1N4747A | Zener 20V 1W | DO-41 | 1 | 0.15 | 0.15 |
| D_zener2 | 1N4742A | Zener 12V 1W | DO-41 | 1 | 0.15 | 0.15 |
| SCR1 | MCR100-6 | SCR 0.8A 400V | TO-92 | 1 | 0.30 | 0.30 |
| Q_SS | IRF9540N | P-MOS 100V 23A | TO-220 | 1 | 1.50 | 1.50 |
| Q1 | BC547B | NPN | TO-92 | 1 | 0.10 | 0.10 |
| U_ref | TL431ACLP | Ref 2.5V | TO-92 | 1 | 0.30 | 0.30 |
| U_comp | LM393P | Comparateur | DIP-8 | 1 | 0.40 | 0.40 |
| LED1 | LED verte | 3mm 20mA | 3mm | 1 | 0.10 | 0.10 |
| D_flyback | 1N4148 | Diode signal | DO-35 | 1 | 0.05 | 0.05 |
| **Total semiconducteurs** | | | | | | **5.05** |

### Passifs - Resistances

| Ref | Valeur | Tolerance | Puissance | Qte | Prix unit | Total |
|-----|--------|-----------|-----------|-----|-----------|-------|
| R_pull | 10k | 5% | 0.25W | 1 | 0.02 | 0.02 |
| R_gate | 47k | 5% | 0.25W | 1 | 0.02 | 0.02 |
| R_pulldown | 100k | 5% | 0.25W | 1 | 0.02 | 0.02 |
| R_snub | 47 | 5% | 0.5W | 1 | 0.05 | 0.05 |
| R_crowbar1 | 1k | 5% | 0.25W | 1 | 0.02 | 0.02 |
| R_crowbar2 | 100 | 5% | 0.25W | 1 | 0.02 | 0.02 |
| R_ref1 | 10k | 5% | 0.25W | 1 | 0.02 | 0.02 |
| R_div1 | 100k | 1% | 0.25W | 1 | 0.05 | 0.05 |
| R_div2 | 27k | 1% | 0.25W | 1 | 0.05 | 0.05 |
| R_pullup_comp | 10k | 5% | 0.25W | 1 | 0.02 | 0.02 |
| R_fb | 1M | 5% | 0.25W | 1 | 0.02 | 0.02 |
| R_base | 4.7k | 5% | 0.25W | 1 | 0.02 | 0.02 |
| R_serie_bobine | 150 | 5% | 0.5W | 1 | 0.05 | 0.05 |
| R_led | 1k | 5% | 0.25W | 1 | 0.02 | 0.02 |
| **Total resistances** | | | | | | **0.40** |

### Passifs - Condensateurs

| Ref | Valeur | Tension | Type | Qte | Prix unit | Total |
|-----|--------|---------|------|-----|-----------|-------|
| C_soft | 33uF | 25V | Electro | 1 | 0.20 | 0.20 |
| C_snub | 100nF | 250V | Film PP | 1 | 0.50 | 0.50 |
| C_filt | 4700uF | 25V | Electro Low-ESR | 1 | 3.00 | 3.00 |
| C_hf | 100uF | 25V | X7R ou 10x10uF | 1 | 2.00 | 2.00 |
| C_ref | 100nF | 25V | X7R | 1 | 0.05 | 0.05 |
| C_dec1 | 100nF | 25V | X7R | 1 | 0.05 | 0.05 |
| C_dec2 | 10uF | 25V | X5R | 1 | 0.20 | 0.20 |
| **Total condensateurs** | | | | | | **6.00** |

### Passifs - Inductances et Ferrites

| Ref | Valeur | Specs | Qte | Prix unit | Total |
|-----|--------|-------|-----|-----------|-------|
| L1 | 10uH | 13A Isat, 8m ohm | 1 | 2.00 | 2.00 |
| NTC1 | 2.5 ohm | 10A Epcos | 1 | 1.50 | 1.50 |
| FB1 | 600 ohm | @ 100MHz | 1 | 0.30 | 0.30 |
| **Total inductances** | | | | | | **3.80** |

### Electromecanique

| Ref | Composant | Specs | Qte | Prix unit | Total |
|-----|-----------|-------|-----|-----------|-------|
| SW1 | Interrupteur | 10A bipolaire | 1 | 2.00 | 2.00 |
| F1 | Fusible | 6.3A 5x20 tempo | 2 | 0.30 | 0.60 |
| K_HP | Relais | HF46F-12 5A | 1 | 2.50 | 2.50 |
| J_batt | XT60 | Male chassis | 1 | 1.00 | 1.00 |
| J_charge | Barrel jack | 5.5x2.1mm | 1 | 0.50 | 0.50 |
| Bornier HP | Bornier vis | 2 positions | 1 | 0.50 | 0.50 |
| **Total electromeca** | | | | | | **7.10** |

### Thermique

| Ref | Composant | Specs | Qte | Prix unit | Total |
|-----|-----------|-------|-----|-----------|-------|
| Radiateur D1 | TO-220 | 10C/W | 1 | 1.50 | 1.50 |
| Pad thermique | Silicone | TO-220 | 2 | 0.20 | 0.40 |
| **Total thermique** | | | | | | **1.90** |

### Modules et Gros Composants

| Ref | Composant | Specs | Qte | Prix unit | Total |
|-----|-----------|-------|-----|-----------|-------|
| Module | Arylic Up2Stream Amp V4 | 2x50W | 1 | 65.00 | 65.00 |
| Batterie | Pack 4S LiFePO4/Li-ion | 6Ah min | 1 | 50.00 | 50.00 |
| BMS | BMS 4S 30A | Avec balance | 1 | 8.00 | 8.00 |
| HP | Haut-parleur | 4-8 ohm | 1 | 30.00 | 30.00 |
| Chargeur | 16.8V 2A | Barrel 5.5mm | 1 | 10.00 | 10.00 |
| **Total modules** | | | | | | **163.00** |

### TOTAL GENERAL

| Categorie | Total |
|-----------|-------|
| Semiconducteurs | 5.05 |
| Resistances | 0.40 |
| Condensateurs | 6.00 |
| Inductances/Ferrites | 3.80 |
| Electromecanique | 7.10 |
| Thermique | 1.90 |
| Modules | 163.00 |
| **TOTAL V2.1** | **~188 EUR** |

---

## GUIDE CONFIGURATION HP (CONSTRUCTEUR)

### Mesure DCR

1. Multimetre en mode Ohm
2. Mesurer resistance HP
3. Noter valeur DCR

### Decision Mode

| DCR mesure | Type HP | Mode | Jumpers Arylic |
|------------|---------|------|----------------|
| < 3.5 ohm | HP 4 ohm | STEREO (L seul) | HAUT + MILIEU |
| 3.5-5.5 ohm | HP 6 ohm | STEREO (L seul) | HAUT + MILIEU |
| > 5.5 ohm | HP 8+ ohm | MONO PBTL | MILIEU + BAS |

### Cablage

**Mode STEREO (HP 4 ohm):**
HP+ → L+ module
HP- → L- module
R+, R- → non connectes

**Mode MONO PBTL (HP 8 ohm):**
HP+ → R+ module
HP- → L+ module
L-, R- → non connectes

---

## UTILISATION FINALE

```
ALLUMER:  Appuyer SW1 → LED verte → musique en 2s
ETEINDRE: Appuyer SW1 → arret propre sans pop
CHARGER:  Brancher chargeur FOURNI (peut ecouter)
STOCKER:  Eteindre et oublier (drain < 10uA)

NE JAMAIS:
- Utiliser autre chargeur que celui fourni
- Brancher batterie a l'envers (mais protege)
```

---

## TESTS VALIDATION CONSTRUCTEUR

Voir protocole detaille: Protocole_Test_V2.1.md

Tests critiques GO/NO-GO:
1. Crowbar: Injecter 20V → fusible doit fondre < 1s
2. Soft-start: Mesurer rampe V_SOFT sur 300-500ms
3. Anti-pop: Aucun pop audible ON/OFF
4. Charge+ecoute: Ripple audio < 10mVpp
5. Thermique D1: T < 80C apres 1h @ 5A

---

## NOTES CONCEPTION

### Pourquoi pas USB-C PD

Decision V2.1: Transfo dedie + crowbar au lieu de USB-C PD

Raisons:
- Utilisateur pas forcement equipe PD
- Zero question, zero confusion
- Chargeur fourni = controle qualite
- Crowbar protege contre mauvais chargeur
- Cout similaire, complexite moindre

### Futur V3.0

Option USB-C PD pour version premium/tech-savvy

---

**FIN CIRCUIT V2.1**
