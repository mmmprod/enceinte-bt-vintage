# BREAKOUT BOX - ENCEINTE BLUETOOTH VINTAGE V1.4

**Version:** 1.4  
**Date:** 14 Decembre 2025

---

# CHANGEMENT MAJEUR V1.4

**AVANT (V1.3) : Insertion serie**
- Breakout box inseree dans le circuit
- Ajout resistances de contact
- Degrade qualite audio

**MAINTENANT (V1.4) : Observation parallele**
- Breakout box connectee EN PARALLELE
- Zero resistance ajoutee sur rail puissance
- Aucun impact sur qualite audio
- Peut rester branchee en permanence

---

# A QUOI CA SERT

La breakout box te permet de mesurer les tensions a 4 points cles du circuit SANS l'affecter. Tu branches ton multimetre sur le bornier TP et tu lis.

---

# PRINCIPE V1.4

```
CIRCUIT PRINCIPAL (inchange)
─────────────────────────────
BATT+ ─── J1+ ─── D1 ─── SW1 ─── F1 ─── NTC1 ─── J2+ ─── AMP
  │                │              │               │
  │                │              │               │
BREAKOUT BOX (observation)       │               │
──────────────────────────       │               │
  │                │              │               │
  └── fil 0.25mm² ─┴── fil ──────┴── fil ────────┴── vers TP
      (V_BATT)        (V_D1)        (V_SW)          (V_PROT)
```

Les fils fins 0.25mm² ne portent AUCUN courant (multimetre = 10MΩ).
Donc ZERO impact sur le circuit.

---

# COMPOSANTS BREAKOUT BOX V1.4

| Ref | Quoi | Qte |
|-----|------|-----|
| TP | Bornier 6 positions 5mm | 1 |
| - | Boitier plastique ABS 60x40x20mm | 1 |
| - | Fil 0.25mm2 rouge | 1m |
| - | Fil 0.25mm2 noir | 30cm |
| - | Fil 0.25mm2 jaune | 30cm |
| - | Fil 0.25mm2 orange | 30cm |
| - | Gaine thermo 2mm | 50cm |

**TOTAL : ~5 EUR**

---

# ETAPE 1 : PERCER LE BOITIER

| Zone | Quoi |
|------|------|
| Face avant | 6 trous pour bornier TP |
| Face arriere | 1 trou 5mm pour passage fils |

---

# ETAPE 2 : PREPARER LES FILS

| # | Couleur | Longueur | Point de mesure |
|---|---------|----------|-----------------|
| 1 | Rouge | 40cm | V_BATT (J1 borne 1) |
| 2 | Orange | 40cm | V_D1 (sortie D1, avant SW1) |
| 3 | Jaune | 40cm | V_SW (sortie SW1, apres F1) |
| 4 | Rouge | 40cm | V_PROT (J2 borne 1) |
| 5 | Noir | 40cm | GND (J1 borne 2) |

Denuder 5mm a chaque extremite.

---

# ETAPE 3 : CABLER LE BORNIER TP

## Assignation bornes

| Borne TP | Nom | Fil couleur |
|----------|-----|-------------|
| 1 | V_BATT | Rouge |
| 2 | V_D1 | Orange |
| 3 | V_SW | Jaune |
| 4 | V_PROT | Rouge |
| 5 | (reserve) | - |
| 6 | GND | Noir |

## Tu fais

| Etape | Action |
|-------|--------|
| 1 | Passer les 5 fils dans le trou arriere du boitier |
| 2 | Visser fil rouge (V_BATT) sur TP borne 1 |
| 3 | Visser fil orange (V_D1) sur TP borne 2 |
| 4 | Visser fil jaune (V_SW) sur TP borne 3 |
| 5 | Visser fil rouge (V_PROT) sur TP borne 4 |
| 6 | Visser fil noir (GND) sur TP borne 6 |
| 7 | Fixer bornier TP dans boitier |

---

# ETAPE 4 : CONNECTER A LA CARTE PROTECTION

**Ces fils sont SOUDES sur la carte, pas branches sur borniers.**

| Fil | Souder sur | Point exact |
|-----|------------|-------------|
| Rouge (V_BATT) | J1 borne 1 | Entree + batterie |
| Orange (V_D1) | Cathode D1 | Sortie diode, avant SW1 |
| Jaune (V_SW) | Sortie F1 | Apres fusible, avant NTC |
| Rouge (V_PROT) | J2 borne 1 | Sortie + vers ampli |
| Noir (GND) | J1 borne 2 | Masse commune |

## Methode de soudure

| Etape | Action |
|-------|--------|
| 1 | Denuder 3mm au bout du fil |
| 2 | Etamer le fil |
| 3 | Ajouter une goutte de soudure sur le point de la carte |
| 4 | Souder le fil sur le point |
| 5 | Mettre gaine thermo sur la soudure |
| 6 | Chauffer la gaine au briquet |

---

# ETAPE 5 : MARQUER LE BOITIER

| Position | Texte |
|----------|-------|
| A cote TP borne 1 | 1: BATT |
| A cote TP borne 2 | 2: D1 |
| A cote TP borne 3 | 3: SW |
| A cote TP borne 4 | 4: PROT |
| A cote TP borne 5 | 5: - |
| A cote TP borne 6 | 6: GND |

---

# UTILISATION

## Methode de mesure

| Etape | Action |
|-------|--------|
| 1 | Mettre multimetre en mode V DC (20V) |
| 2 | Pointe NOIRE sur TP borne 6 (GND) |
| 3 | Pointe ROUGE sur borne a mesurer (1, 2, 3 ou 4) |
| 4 | Lire la valeur |

## Tensions attendues (Circuit V1.8)

| Borne | Nom | SW1 ON | SW1 OFF | Si hors plage |
|-------|-----|--------|---------|---------------|
| 1 | V_BATT | 12.0 - 16.8V | 12.0 - 16.8V | Batterie HS |
| 2 | V_D1 | 11.5 - 16.3V | 11.5 - 16.3V | D1 defaillante |
| 3 | V_SW | 11.5 - 16.3V | 0V | SW1 ou F1 HS |
| 4 | V_PROT | 11.0 - 15.8V | 0V | NTC HS |
| 6 | GND | 0V (ref) | 0V (ref) | - |

## Chutes de tension normales

| Entre | Chute attendue | Si trop elevee |
|-------|----------------|----------------|
| BATT → D1 | 0.3 - 0.5V | D1 defaillante |
| D1 → SW | 0V (SW ferme) | SW1 mauvais contact |
| SW → PROT | 0.1 - 0.5V | NTC chaude normale |

---

# DIAGNOSTIC AVEC BREAKOUT BOX

| Symptome | Mesure a faire | Interpretation |
|----------|----------------|----------------|
| Rien ne marche | V_BATT | 0V = batterie debranchee |
| Rien ne marche | V_D1 vs V_BATT | Diff > 1V = D1 inversee |
| Rien apres allumage | V_SW | 0V = SW1 OFF ou F1 grille |
| Ampli demarre pas | V_PROT | < 11V = batterie vide |
| Son coupe par moments | V_PROT sous charge | Chute > 2V = NTC HS |

---

# AVANTAGES V1.4 vs V1.3

| Aspect | V1.3 (serie) | V1.4 (parallele) |
|--------|--------------|------------------|
| Impact audio | Degrade | **AUCUN** |
| Resistance ajoutee | 0.1 - 1Ω | **0Ω** |
| Peut rester branchee | Non | **Oui** |
| Points de mesure | 3 | **4** |
| Mesure V_D1 | Non | **Oui** |
| Complexite cablage | Moyenne | Facile |
| Prix | 10 EUR | **5 EUR** |

---

# ⚠️ PRECAUTIONS

| # | Precaution |
|---|------------|
| 1 | Ne pas court-circuiter les fils entre eux |
| 2 | Ne pas tirer sur les fils (soudures fragiles) |
| 3 | Verifier isolation gaines thermo |
| 4 | Si fil se dessoud : ETEINDRE avant ressouder |

---

# CHANGELOG

| Version | Date | Modifications |
|---------|------|---------------|
| V1.4 | 14 Dec 2025 | Refonte totale : mode observation parallele, zero impact audio |
| V1.3 | 14 Dec 2025 | GND relie sur tous blocs, tensions corrigees |
| V1.2 | 14 Dec 2025 | Refs explicites |
| V1.1 | 14 Dec 2025 | Suppression schemas ASCII |
| V1.0 | 14 Dec 2025 | Version initiale (insertion serie) |

---

**FIN BREAKOUT BOX V1.4**
