# BREAKOUT BOX DIAGNOSTIC V3.1

**Version:** 3.1
**Date:** Decembre 2025
**Compatibilite:** Circuit Enceinte BT Vintage V2.0+
**Auteur:** Mehdi

---

## CHANGELOG V3.1

| Version | Date | Modifications |
|---------|------|---------------|
| V3.1 | Dec 2025 | Audit V3: Triple protection, TVS, filtrage HF, JST-XH |
| V2.0 | Dec 2025 | R_sense integrees au circuit principal |
| V1.0 | Nov 2025 | Version initiale externe |

### Corrections V3.1 vs V2.0

| # | Probleme V2.0 | Correction V3.1 | Cout |
|---|---------------|-----------------|------|
| 1 | R_sense 1k defaillante = 200A | Triple protection (R_sense + R_limit + PolySwitch) | +0.60 |
| 2 | Inversion polarite = dommage batterie | TVS SMAJ18CA bidirectionnelle par TP | +3.50 |
| 3 | Marge thermique 44% | R_sense 2.2k (P=0.058W, marge 88%) | 0 |
| 4 | Fils = antennes HF | Paires torsadees + C_filt 100nF | +0.70 |
| 5 | Pas indication tension | LED temoin V_PROT | +0.20 |
| 6 | Borniers vibration | Connecteur JST-XH verrouille | +1.00 |
| 7 | Corrosion possible | Conformal coating recommande | +2.00 |
| **TOTAL delta** | | | **~8 EUR** |

---

## SPECIFICATIONS BREAKOUT V3.1

| Parametre | Valeur |
|-----------|--------|
| Points de test | 7 (TP1-TP7) |
| Tension max | 25V |
| Courant max mesure | 7.6mA (nominal) |
| Courant court-circuit max | 200mA (PolySwitch) |
| Protection ESD | 8kV (IEC 61000-4-2) |
| Filtrage HF | -60dB @ 500kHz |
| Temperature operation | -10C a +60C |
| Precision mesure | ±0.5% (avec multi 10M ohm) |

---

## SCHEMA BLOC V3.1

```
CIRCUIT PRINCIPAL                    BREAKOUT BOX V3.1
================                     =================

                    TRIPLE PROTECTION PAR TP
                    ┌─────────────────────────────────────┐
                    │                                     │
V_BATT ──── R_sense ──── R_limit ──── PolySwitch ───┬─── TP1
            2.2k         100 ohm      100mA         │
                                                    TVS (SMAJ18CA)
                                                    │
                                                C_filt (100nF)
                                                    │
                                                   GND
```

---

## TOPOLOGIE DETAILLEE PAR POINT DE TEST

### TP1 — Tension Batterie (V_BATT)

**Topologie:**
BATT+ (circuit) → R_sense1 (2.2k 0.5W) → node1
node1 → R_limit1 (100 ohm 0.5W) → node2
node2 → PolySwitch1 (MF-R010 100mA) → TP1
TP1 → TVS1 (SMAJ18CA) cathode
TVS1 anode → GND_BB
TP1 → C_filt1 (100nF X7R) → GND_BB

**Calculs:**
V_nominal = 14.8V (typ), 16.8V (max)
I_nominal = 16.8V / 2300 ohm = 7.3mA
P_R_sense = (7.3mA)^2 x 2200 = 0.117W < 0.5W OK (marge 77%)
P_R_limit = (7.3mA)^2 x 100 = 0.005W negligeable

**Protection triple:**
1. R_sense 2.2k: Limite courant normal
2. R_limit 100 ohm: Backup si R_sense defaillante
3. PolySwitch: Limite absolue 200mA

**Mode defaillance:**
- R_sense OK: I = 7.3mA (nominal)
- R_sense ouverte: I = 16.8V / 100 = 168mA → PolySwitch declenche
- R_sense + R_limit ouvertes: Fil deconnecte (safe)
- Court-circuit TP: I = 168mA → PolySwitch declenche

### TP2 — Tension apres D1 (V_D1)

**Topologie:**
V_D1 (circuit) → R_sense2 (2.2k 0.5W) → node1
node1 → R_limit2 (100 ohm 0.5W) → node2
node2 → PolySwitch2 (MF-R010 100mA) → TP2
TP2 → TVS2 (SMAJ18CA) → GND_BB
TP2 → C_filt2 (100nF X7R) → GND_BB

### TP3 — Tension Soft-Start (V_SOFT)

**Topologie:**
V_SOFT (circuit) → R_sense3 (2.2k 0.5W) → node1
node1 → R_limit3 (100 ohm 0.5W) → node2
node2 → PolySwitch3 (MF-R010 100mA) → TP3
TP3 → TVS3 (SMAJ18CA) → GND_BB
TP3 → C_filt3 (100nF X7R) → GND_BB

### TP4 — Tension Protegee (V_PROT)

**Topologie:**
V_PROT (circuit) → R_sense4 (2.2k 0.5W) → node1
node1 → R_limit4 (100 ohm 0.5W) → node2
node2 → PolySwitch4 (MF-R010 100mA) → TP4
TP4 → TVS4 (SMAJ18CA) → GND_BB
TP4 → C_filt4 (100nF X7R) → GND_BB

**LED temoin (NOUVEAU V3.1):**
TP4 → R_led (10k) → LED_G anode
LED_G cathode → GND_BB

Calcul:
I_led = (12V - 2V) / 10k = 1mA (faible mais visible)
P = 1mA x 12V = 12mW negligeable

Fonction:
- LED ON = circuit sous tension = NE PAS mesurer resistance
- LED OFF = tension absente/faible = mesure resistance possible

### TP5 — Tension Filtree (V_FILT)

**Topologie:**
V_FILT (circuit) → R_sense5 (2.2k 0.5W) → node1
node1 → R_limit5 (100 ohm 0.5W) → node2
node2 → PolySwitch5 (MF-R010 100mA) → TP5
TP5 → TVS5 (SMAJ18CA) → GND_BB
TP5 → C_filt5 (100nF X7R) → GND_BB

### TP6 — Sortie Comparateur (COMP_OUT)

**Topologie:**
COMP_OUT (circuit) → R_sense6 (2.2k 0.5W) → node1
node1 → R_limit6 (100 ohm 0.5W) → node2
node2 → PolySwitch6 (MF-R010 100mA) → TP6
TP6 → TVS6 (SMAJ18CA) → GND_BB
TP6 → C_filt6 (100nF X7R) → GND_BB

**Note:** Signal logique 0V/14V, mesure ON/OFF relais

### TP7 — Gate Soft-Start (GATE_SS)

**Topologie:**
GATE_SS (circuit) → R_sense7 (2.2k 0.5W) → node1
node1 → R_limit7 (100 ohm 0.5W) → node2
node2 → PolySwitch7 (MF-R010 100mA) → TP7
TP7 → TVS7 (SMAJ18CA) → GND_BB
TP7 → C_filt7 (100nF X7R) → GND_BB

**Note:** Mesure rampe RC soft-start

### GND — Masse Reference

**Topologie:**
GND (circuit) → GND_BB (breakout)
GND_BB = reference commune tous TP

**Important:** GND unique, pas de GND separes par TP

---

## CONNECTEUR NAPPE JST-XH (NOUVEAU V3.1)

### Remplacement Borniers

**Avant (V2.0):** Borniers a vis 5mm (risque devissage vibration)
**Apres (V3.1):** Connecteur JST-XH 10 positions (verrouillage mecanique)

### Brochage Connecteur J1 (JST-XH 10 pins)

| Pin | Signal | Couleur fil |
|-----|--------|-------------|
| 1 | TP1 (V_BATT) | Rouge |
| 2 | TP2 (V_D1) | Orange |
| 3 | TP3 (V_SOFT) | Jaune |
| 4 | TP4 (V_PROT) | Vert |
| 5 | TP5 (V_FILT) | Bleu |
| 6 | TP6 (COMP_OUT) | Violet |
| 7 | TP7 (GATE_SS) | Gris |
| 8 | GND | Noir |
| 9 | GND | Noir |
| 10 | NC | - |

### Avantages JST-XH

- Verrouillage positif (click)
- Impossible devissage par vibration
- Detrompeur (impossible inverser)
- Contact fiable -40C a +85C
- Vibration-proof (utilise en automobile)

---

## CABLAGE NAPPE

### Paires Torsadees (NOUVEAU V3.1)

**Chaque signal + son GND dedie torsades ensemble:**

| Paire | Fils | Torsade |
|-------|------|---------|
| Paire 1 | TP1 + GND | 10 tours / 10cm |
| Paire 2 | TP2 + GND | 10 tours / 10cm |
| Paire 3 | TP3 + GND | 10 tours / 10cm |
| Paire 4 | TP4 + GND | 10 tours / 10cm |
| Paire 5 | TP5 + GND | 10 tours / 10cm |
| Paire 6 | TP6 + GND | 10 tours / 10cm |
| Paire 7 | TP7 + GND | 10 tours / 10cm |

**Effet:**
- Rejection mode commun: 20-40dB
- Bruit HF 100mV → 1-10mV

### Specifications Fils

- Section: 0.25mm² (AWG24)
- Type: Silicone ou PVC souple
- Longueur max: 50cm
- Blindage: Non requis (paires torsadees suffisent)

---

## BOM BREAKOUT V3.1

### Resistances

| Ref | Valeur | Tolerance | Puissance | Qte | Prix unit | Total |
|-----|--------|-----------|-----------|-----|-----------|-------|
| R_sense1-7 | 2.2k | 1% | 0.5W | 7 | 0.05 | 0.35 |
| R_limit1-7 | 100 | 5% | 0.5W | 7 | 0.03 | 0.21 |
| R_led | 10k | 5% | 0.25W | 1 | 0.02 | 0.02 |
| **Total R** | | | | | | **0.58** |

### Semiconducteurs

| Ref | Composant | Specs | Qte | Prix unit | Total |
|-----|-----------|-------|-----|-----------|-------|
| TVS1-7 | SMAJ18CA | 18V 400W bidir | 7 | 0.50 | 3.50 |
| LED_G | LED verte | 3mm 20mA | 1 | 0.10 | 0.10 |
| **Total semi** | | | | | | **3.60** |

### Fusibles Rearmables

| Ref | Composant | Specs | Qte | Prix unit | Total |
|-----|-----------|-------|-----|-----------|-------|
| PS1-7 | MF-R010 | 100mA hold, 200mA trip | 7 | 0.30 | 2.10 |
| **Total PTC** | | | | | | **2.10** |

### Condensateurs

| Ref | Valeur | Tension | Type | Qte | Prix unit | Total |
|-----|--------|---------|------|-----|-----------|-------|
| C_filt1-7 | 100nF | 50V | X7R | 7 | 0.05 | 0.35 |
| **Total C** | | | | | | **0.35** |

### Connecteurs

| Ref | Composant | Specs | Qte | Prix unit | Total |
|-----|-----------|-------|-----|-----------|-------|
| J1 | JST-XH | 10 positions male | 1 | 0.50 | 0.50 |
| J1_cable | JST-XH | 10 positions femelle + fils | 1 | 1.50 | 1.50 |
| Bananes | Douilles 4mm | Rouge/Noir | 8 | 0.30 | 2.40 |
| **Total conn** | | | | | | **4.40** |

### Divers

| Ref | Composant | Specs | Qte | Prix unit | Total |
|-----|-----------|-------|-----|-----------|-------|
| PCB | Veroboard | 5x7cm | 1 | 1.00 | 1.00 |
| Boitier | Plastique | 10x6x3cm | 1 | 3.00 | 3.00 |
| Conformal | Spray | Electrolube HPA | 1 | 8.00 | 2.00 |
| **Total divers** | | | | | | **6.00** |

### TOTAL BREAKOUT V3.1

| Categorie | Total |
|-----------|-------|
| Resistances | 0.58 |
| Semiconducteurs | 3.60 |
| PTC | 2.10 |
| Condensateurs | 0.35 |
| Connecteurs | 4.40 |
| Divers | 6.00 |
| **TOTAL** | **~17 EUR** |

---

## PROCEDURES DIAGNOSTIC

### Procedure 1 — Verification Alimentation

**Equipement:** Multimetre (impedance >= 1M ohm)

**Etapes:**

1. **SW1 = OFF, chargeur debranche**
   - TP1 (V_BATT): 12.0-16.8V selon SoC
   - TP2 (V_D1): 0V (D1 bloquee, pas de courant)
   - TP4 (V_PROT): 0V
   - LED temoin: OFF

2. **SW1 = ON**
   - TP1: Inchange
   - TP2: V_BATT - 0.5V (chute D1)
   - TP3 (V_SOFT): Monte progressivement 0 → V_D1 en 300-500ms
   - TP4: = TP3 apres stabilisation
   - LED temoin: ON

3. **Chargeur branche (SW1 = ON ou OFF)**
   - TP1: 16.8V (tension chargeur via BMS)
   - Si LED clignote: BMS en protection, verifier cellules

### Procedure 2 — Verification Soft-Start

**Equipement:** Oscilloscope (ou multimetre mode MIN/MAX)

**Etapes:**

1. SW1 = OFF, attendre 10s (decharge C_soft)
2. Connecter sonde sur TP3 (V_SOFT)
3. Basculer SW1 = ON
4. Observer rampe:
   - Temps 10% → 90%: 300-500ms
   - Pas de depassement (overshoot)
   - Forme exponentielle (1 - e^(-t/tau))

**Critere GO:** Rampe visible, t_montee > 200ms
**Critere NO-GO:** Montee instantanee = C_soft HS ou court-circuit

### Procedure 3 — Verification Anti-Pop

**Equipement:** Oreille + optionnel oscilloscope sur HP

**Etapes:**

1. HP connecte, volume moyen
2. SW1 = OFF → ON: Aucun pop audible
3. SW1 = ON → OFF: Aucun pop audible
4. Repeter 5 fois

**Critere GO:** Zero pop sur 5 cycles
**Critere NO-GO:** Pop audible = verifier K_HP, seuil comparateur

### Procedure 4 — Verification Relais

**Equipement:** Multimetre

**Etapes:**

1. SW1 = ON, attendre 2s stabilisation
2. TP6 (COMP_OUT): ~14V = relais commande
3. Continuite HP+_MODULE → HP+_OUT: < 1 ohm
4. SW1 = OFF
5. TP6: ~0V = relais decommande
6. Continuite HP+_MODULE → HP+_OUT: > 1M ohm (ouvert)

### Procedure 5 — Verification Thermique

**Equipement:** Thermometre IR ou doigt prudent

**Etapes:**

1. Fonctionnement 30min @ volume moyen
2. Mesurer temperature:
   - D1 (diode): < 80C
   - Q_SS (MOSFET): < 60C
   - L1 (inductance): < 50C
   - C_filt: < 50C

**Critere GO:** Toutes T < limites
**Critere NO-GO:** Composant brulant = probleme

### Procedure 6 — Test Protection Crowbar

**ATTENTION: Ce test detruit le fusible F1**

**Equipement:** Alimentation labo variable + fusible spare

**Etapes:**

1. SW1 = ON, deconnecter batterie
2. Connecter alimentation labo sur J_charge (centre +)
3. Limiter courant alim a 1A
4. Monter tension progressivement:
   - 12V: Circuit fonctionne normal
   - 16V: Circuit fonctionne normal
   - 18V: Circuit fonctionne normal
   - 20V: SCR s'amorce, courant monte, fusible fond

**Critere GO:** Fusible fond entre 19V et 22V
**Critere NO-GO:** Fusible ne fond pas a 24V = SCR ou Zener HS

---

## TABLEAU DIAGNOSTIC RAPIDE

| Symptome | TP a verifier | Cause probable | Action |
|----------|---------------|----------------|--------|
| Rien ne marche | TP1 | Batterie HS ou inversee | Verifier polarite, tension |
| LED temoin OFF mais batterie OK | TP4 | F1 fondu ou SW1 HS | Verifier fusible |
| Pas de son | TP4, TP6 | Relais ou comparateur | Verifier seuil 11.7V |
| Pop au demarrage | TP3, TP6 | Soft-start ou timing relais | Verifier C_soft, R_fb |
| Ronflette 50Hz | TP5 | Filtre LC ou boucle masse | Verifier L1, GND |
| Sifflement HF | TP5 | Decouplage module | Verifier C_dec |
| Chauffe excessive | TP2, TP4 | Surcharge ou ventilation | Verifier courant, aeration |
| Coupures aleatoires | TP4 | BMS protection | Verifier equilibrage cellules |

---

## SPECIFICATIONS MULTIMETRE

### Impedance Minimum Requise

| Impedance multi | Erreur mesure | Verdict |
|-----------------|---------------|---------|
| 10M ohm | 0.02% | IDEAL |
| 1M ohm | 0.22% | ACCEPTABLE |
| 100k ohm | 2.2% | DECONSEILLE |

**Calcul:**
Erreur = R_sense / (R_sense + R_multi) x 100%
Avec R_sense = 2.2k:
- 10M: 2.2k / 10M = 0.022%
- 1M: 2.2k / 1M = 0.22%
- 100k: 2.2k / 100k = 2.2%

### Test Impedance Multimetre

Si impedance inconnue:
1. Mesurer pile 1.5V neuve
2. Si affiche < 1.45V = impedance trop basse
3. Utiliser autre multimetre

### Precision Globale

| Source erreur | Valeur |
|---------------|--------|
| Tolerance R_sense 1% | ±1% |
| Impedance multi 10M | ±0.02% |
| Temperature -10C/+60C | ±0.4% |
| **Total (RSS)** | **±1.1%** |

---

## PROTECTION ESD

### Specifications TVS SMAJ18CA

| Parametre | Valeur |
|-----------|--------|
| V_RWM (standoff) | 18V |
| V_BR (breakdown) | 20-22V |
| V_C (clamp) | 29V @ 100A |
| I_PP (peak pulse) | 100A @ 8/20us |
| ESD rating | 8kV contact, 15kV air |

### Fonctionnement Protection

**Normal (V < 18V):**
- TVS haute impedance
- I_leakage < 1uA
- Aucun impact mesure

**ESD (4kV pulse):**
- TVS clampe en < 1ns
- Energie absorbee: ~1mJ
- Circuit protege

**Inversion polarite:**
- TVS clampe a -20V
- Courant limite par R_sense
- I_max = 20V / 2.2k = 9mA (safe)

---

## FILTRAGE HF

### Specifications Filtre RC

Avec R_sense 2.2k + C_filt 100nF:
- f_c = 1 / (2 x pi x R x C) = 723Hz
- Attenuation @ 100kHz: -43dB
- Attenuation @ 500kHz: -57dB
- Attenuation @ 1MHz: -63dB

### Sources Bruit Filtrees

| Source | Frequence | Attenuation | V_residuel |
|--------|-----------|-------------|------------|
| DC/DC chargeur | 100kHz | -43dB | 7uV |
| Bluetooth | 2.4GHz | >-80dB | <1uV |
| Classe D ampli | 400kHz | -55dB | 2uV |

### Impact sur Mesure DC

- Temps reponse: 5 x tau = 5 x 220us = 1.1ms
- Invisible pour multimetre (rafraichit @ 2-4Hz)

---

## MAINTENANCE

### Nettoyage

- Deconnecter avant nettoyage
- Alcool isopropylique 99%
- Brosse douce antistatique
- Secher completement avant utilisation

### Conformal Coating (Recommande)

**Application:**
1. Nettoyer PCB (alcool IPA)
2. Secher 80C / 2h (elimine humidite)
3. Masquer connecteurs JST avec ruban
4. Appliquer 2 couches spray (Electrolube HPA)
5. Secher 24h

**Benefices:**
- Protection humidite
- Protection corrosion
- Isolation supplementaire
- Duree vie x5 en environnement humide

### Stockage

- Boitier ferme
- Eviter humidite > 80%
- Temperature -20C a +70C
- A l'abri UV

---

## AVERTISSEMENTS SECURITE

```
⚠️ LED VERTE ALLUMEE = CIRCUIT SOUS TENSION
   Ne PAS mesurer resistance ou continuite

⚠️ UN SEUL MULTIMETRE A LA FOIS
   Deux multimetres secteur = boucle de masse = ronflette 50Hz

⚠️ UTILISER MULTIMETRE SUR BATTERIE si mesures simultanees requises

⚠️ VERIFIER POLARITE avant branchement
   Protection existe mais eviter de la solliciter

⚠️ NE JAMAIS court-circuiter les TP volontairement
   PolySwitch protege mais s'use a chaque declenchement
```

---

## SCHEMA IMPLANTATION VEROBOARD

```
     1   2   3   4   5   6   7   8   9  10  11  12  13  14  15
   +---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
 A | o | o | o | o | o | o | o | o | o | o | o | o | o | o | o |  ← GND rail
   +---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
 B |R_s|   |R_l|   |PTC|   |TVS|   |C_f|   |   |   |   |   |   |  ← TP1
   +---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
 C |R_s|   |R_l|   |PTC|   |TVS|   |C_f|   |   |   |   |   |   |  ← TP2
   +---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
 D |R_s|   |R_l|   |PTC|   |TVS|   |C_f|   |   |   |   |   |   |  ← TP3
   +---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
 E |R_s|   |R_l|   |PTC|   |TVS|   |C_f|   |LED|R_L|   |   |   |  ← TP4 + LED
   +---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
 F |R_s|   |R_l|   |PTC|   |TVS|   |C_f|   |   |   |   |   |   |  ← TP5
   +---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
 G |R_s|   |R_l|   |PTC|   |TVS|   |C_f|   |   |   |   |   |   |  ← TP6
   +---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
 H |R_s|   |R_l|   |PTC|   |TVS|   |C_f|   |   |   |   |   |   |  ← TP7
   +---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
 I | o | o | o | o | o | o | o | o | o | o |JST|JST|JST|JST|JST|  ← Connecteur
   +---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+

Legende:
R_s = R_sense 2.2k
R_l = R_limit 100 ohm  
PTC = PolySwitch MF-R010
TVS = SMAJ18CA
C_f = 100nF X7R
LED = LED verte 3mm
R_L = R_led 10k
JST = Connecteur JST-XH 10 pins
```

---

**FIN BREAKOUT BOX V3.1**
