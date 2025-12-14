# ENCEINTE BLUETOOTH VINTAGE — README V2.1

**Projet:** Enceinte Bluetooth portable haut de gamme
**Version:** 2.1
**Date:** Decembre 2025
**Auteur:** Mehdi

---

## PRESENTATION

Transformation d'une enceinte vintage en systeme audio Bluetooth moderne:
- Batterie Li-ion 4S (14.8V nominal)
- Module Arylic Up2Stream Amp V4 (2x50W)
- Protection complete (surtension, inversion, court-circuit)
- Anti-pop au demarrage
- Diagnostic via Breakout Box

---

## PHILOSOPHIE V2.1

```
PLUG & PLAY TOTAL

L'utilisateur final:
- Appuie ON → musique
- Appuie OFF → arret propre
- Branche chargeur FOURNI → charge

C'est TOUT. Zero configuration. Zero risque.
```

---

## NOUVEAUTES V2.1

### Corrections Audit V3

| # | Probleme detecte | Solution V2.1 |
|---|------------------|---------------|
| 1 | TVS trop basse (18V vs 16.8V batt) | TVS 1.5KE22CA (V_RWM=18.8V) |
| 2 | Mauvais chargeur = destruction | Crowbar SCR coupe a 18V |
| 3 | Relais surchauffe @ 16.8V | R_serie 150 ohm |
| 4 | L1 saturation inconnue | Wurth 74435588100 (13A) |
| 5 | LM393 chattering | Hysteresis 300mV (R_fb 1M) |
| 6 | Breakout vulnerable | Triple protection + TVS |

### Protection Chargeur (Crowbar)

```
Chargeur correct (16.8V): Fonctionne normal
Chargeur laptop (19V):    Crowbar declenche → fusible fond → protege
Chargeur 24V:             Idem

L'utilisateur peut se tromper de chargeur.
Le circuit est TOUJOURS protege.
```

---

## FICHIERS DU PROJET

### Documentation Principale

| Fichier | Description | Lignes |
|---------|-------------|--------|
| Circuit_Enceinte_BT_Vintage_V2_1.md | Schema complet + BOM | 693 |
| Breakout_Box_Enceinte_BT_V3_1.md | Boitier diagnostic | 606 |
| README_V2.1.md | Ce fichier | - |

### Historique Versions

| Version | Date | Changements majeurs |
|---------|------|---------------------|
| V1.0-1.5 | Nov 2025 | Conception initiale |
| V1.6-1.10 | Nov 2025 | Corrections audit V1-V2 |
| V2.0 | Dec 2025 | Soft-start, anti-pop, filtre LC |
| **V2.1** | Dec 2025 | **Crowbar, TVS 22V, hysteresis** |

---

## SPECIFICATIONS TECHNIQUES

### Alimentation

| Parametre | Valeur |
|-----------|--------|
| Batterie | Li-ion 4S (14.8V nom, 16.8V charge) |
| Capacite recommandee | 6Ah minimum |
| BMS | 4S 30A avec equilibrage |
| Chargeur | 16.8V 2A (FOURNI) |
| Autonomie estimee | 8-12h @ volume moyen |

### Audio

| Parametre | Valeur |
|-----------|--------|
| Module | Arylic Up2Stream Amp V4 |
| Puissance | 2x50W (stereo) ou 1x100W (mono) |
| Impedance HP | 4-8 ohms |
| Bluetooth | 5.0 aptX HD |
| Connectivite | WiFi, AirPlay 2, Spotify Connect |

### Protections

| Protection | Composant | Seuil |
|------------|-----------|-------|
| Anti-inversion | D1 SB560 | Schottky 60V |
| Surtension transitoire | TVS1 1.5KE22CA | Clamp 35V |
| Mauvais chargeur | SCR crowbar | >18V → fusible |
| Surintensité | F1 6.3A | Temporise |
| Inrush | NTC1 2.5 ohm | Limite 6A |
| Anti-pop | K_HP relais | Delai 300ms |

---

## GUIDE MONTAGE RAPIDE

### Etape 1 — Preparer Composants

Verifier BOM complete dans Circuit_V2.1.md
Commander composants manquants
Preparer veroboard 10x15cm

### Etape 2 — Monter Bloc Alimentation

```
1. D1 (SB560) + radiateur
2. TVS1 (1.5KE22CA)
3. Crowbar (SCR + Zener 20V + R)
4. F1 (fusible 6.3A)
5. NTC1 (2.5 ohm)
```

### Etape 3 — Monter Soft-Start

```
1. Q_SS (IRF9540N)
2. R_pull (10k) + R_gate (47k) + R_pulldown (100k)
3. C_soft (33uF)
4. D_zener (12V)
```

### Etape 4 — Monter Filtre LC

```
1. L1 (10uH 13A)
2. C_filt (4700uF low-ESR)
3. C_hf (100uF ceramique)
```

### Etape 5 — Monter Anti-Pop

```
1. TL431 + R_ref (10k)
2. Diviseur R_div1/R_div2
3. LM393 + R_fb (1M) + R_pullup (10k)
4. Q1 (BC547) + R_base (4.7k) + R_serie (150 ohm)
5. K_HP (relais HF46F-12)
```

### Etape 6 — Connecter Module Arylic

```
1. Decouplage (100nF + 10uF)
2. Ferrite bead
3. Configurer jumpers selon HP (voir guide)
```

### Etape 7 — Tests

```
1. Verifier continuite GND
2. Verifier pas de court-circuit
3. Brancher batterie
4. Mesurer tensions (voir Breakout)
5. Test audio
```

---

## CONFIGURATION HP

### Mesurer Impedance

```
Multimetre mode Ohm sur HP:
- < 3.5 ohm = HP 4 ohm
- 3.5-5.5 ohm = HP 6 ohm  
- > 5.5 ohm = HP 8 ohm
```

### Choisir Mode

| HP | Mode | Jumpers Arylic |
|----|------|----------------|
| 4 ohm | STEREO (L seul) | HAUT + MILIEU |
| 6 ohm | STEREO (L seul) | HAUT + MILIEU |
| 8 ohm | MONO PBTL | MILIEU + BAS |

### Cabler

**STEREO (4-6 ohm):**
```
HP+ → L+
HP- → L-
```

**MONO (8 ohm):**
```
HP+ → R+
HP- → L+
```

---

## UTILISATION

### Allumer

```
1. Appuyer interrupteur SW1
2. LED verte s'allume
3. Attendre 2s (soft-start + anti-pop)
4. Musique!
```

### Eteindre

```
1. Appuyer interrupteur SW1
2. Arret propre sans pop
3. LED s'eteint
```

### Charger

```
1. Brancher chargeur FOURNI (16.8V)
2. BMS gere la charge
3. Peut ecouter pendant charge
4. Deconnecter quand plein
```

### ATTENTION

```
⚠️ UTILISER UNIQUEMENT LE CHARGEUR FOURNI
   (Protection crowbar si erreur, mais eviter)

⚠️ NE PAS OUVRIR PENDANT FONCTIONNEMENT
   (Tensions dangereuses)

⚠️ STOCKER BATTERIE CHARGEE 50-70%
   (Longevite optimale)
```

---

## DIAGNOSTIC

### Avec Breakout Box V3.1

```
7 points de test securises:
- TP1: V_BATT (batterie)
- TP2: V_D1 (apres diode)
- TP3: V_SOFT (soft-start)
- TP4: V_PROT (protege)
- TP5: V_FILT (filtre)
- TP6: COMP_OUT (comparateur)
- TP7: GATE_SS (gate MOSFET)
```

### Tableau Diagnostic Rapide

| Symptome | Verifier | Cause probable |
|----------|----------|----------------|
| Rien ne marche | TP1 | Batterie HS |
| Pas de son | TP4, TP6 | Seuil comparateur |
| Pop au demarrage | TP3 | C_soft ou timing |
| Ronflette 50Hz | TP5 | Masse ou filtre |
| Chauffe | D1, Q_SS | Surcharge |

---

## COUT ESTIMATIF

### Circuit Principal V2.1

| Categorie | Cout |
|-----------|------|
| Semiconducteurs | 5 EUR |
| Passifs | 10 EUR |
| Electromecanique | 7 EUR |
| Thermique | 2 EUR |
| **Sous-total circuit** | **~25 EUR** |

### Modules

| Module | Cout |
|--------|------|
| Arylic Up2Stream Amp V4 | 65 EUR |
| Batterie 4S 6Ah | 50 EUR |
| BMS 4S 30A | 8 EUR |
| Haut-parleur | 30 EUR |
| Chargeur 16.8V | 10 EUR |
| **Sous-total modules** | **~163 EUR** |

### Breakout Box V3.1

| Categorie | Cout |
|-----------|------|
| Composants | 11 EUR |
| Connecteurs | 4 EUR |
| Boitier | 3 EUR |
| **Sous-total breakout** | **~17 EUR** |

### TOTAL PROJET

```
Circuit V2.1:     25 EUR
Modules:         163 EUR
Breakout V3.1:    17 EUR
Divers (fils):    10 EUR
------------------------
TOTAL:          ~215 EUR
```

---

## SUPPORT

### Probleme?

1. Consulter Breakout_Box_V3.1.md (procedures diagnostic)
2. Verifier tensions aux points de test
3. Comparer avec valeurs attendues

### Ameliorations Futures (V3.0)

- USB-C Power Delivery (version premium)
- Indicateur niveau batterie (LED RGB)
- Telecommande IR
- Egaliseur integre

---

## LICENCE

Projet open-source pour usage personnel.
Documentation libre de droits.
Pas de garantie — utilisation a vos risques.

---

**BON MONTAGE!**

---

**FIN README V2.1**
