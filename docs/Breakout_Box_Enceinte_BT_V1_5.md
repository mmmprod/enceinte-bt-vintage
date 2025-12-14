# BREAKOUT BOX - ENCEINTE BLUETOOTH VINTAGE V1.5

**Version:** 1.5  
**Date:** 14 Decembre 2025

---

# ⚠️ SECURITE V1.5

**AVANT (V1.4) : RISQUE INCENDIE**
- Fils 0.25mm² connectes DIRECT aux points de puissance
- Court-circuit fil rouge/noir = 200A instantane
- Fil fond en 50ms, feu possible

**MAINTENANT (V1.5) : SECURISE**
- Resistances 10kΩ sur le PCB principal (Circuit V1.9)
- Court-circuit max = 14V / 10kΩ = 1.4mA
- IMPOSSIBLE de creer un incendie

---

# A QUOI CA SERT

La breakout box te permet de mesurer les tensions a 4 points cles du circuit SANS risque. Tu branches ton multimetre sur le bornier TP et tu lis.

---

# PREREQUIS

**Cette breakout box necessite le Circuit V1.9 ou superieur.**

Le Circuit V1.9 a des resistances R_s1 a R_s4 (10kΩ) et des points TP1-TP4 sur le PCB.
Ces resistances protegent les fils contre les courts-circuits.

---

# PRINCIPE V1.5

```
PCB PRINCIPAL (Circuit V1.9)
────────────────────────────
                    ┌── R_s1 (10kΩ) ── TP1 ──┐
BATT+ ──────────────┤                         │
                    └── vers D1...            │
                                              │
D1 cathode ─────────── R_s2 (10kΩ) ── TP2 ──┤
                                              ├── Fils 0.25mm² ── BREAKOUT BOX
Sortie F1 ─────────── R_s3 (10kΩ) ── TP3 ──┤
                                              │
J2+ ────────────────── R_s4 (10kΩ) ── TP4 ──┤
                                              │
J1- ────────────────── direct ────── TP_GND ─┘


SECURITE:
Si fil TP1 touche fil TP_GND :
I = 14V / 10kΩ = 1.4mA → AUCUN DANGER
```

---

# COMPOSANTS BREAKOUT BOX V1.5

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

**NOTE : Les resistances 10kΩ sont sur le PCB principal (Circuit V1.9), PAS dans la breakout box.**

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
| 1 | Rouge | 40cm | V_BATT (TP1 sur PCB) |
| 2 | Orange | 40cm | V_D1 (TP2 sur PCB) |
| 3 | Jaune | 40cm | V_SW (TP3 sur PCB) |
| 4 | Rouge | 40cm | V_PROT (TP4 sur PCB) |
| 5 | Noir | 40cm | GND (TP_GND sur PCB) |

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

# ETAPE 4 : CONNECTER AU PCB PRINCIPAL

**Ces fils sont SOUDES sur les points TP du PCB principal (Circuit V1.9).**

| Fil | Souder sur | Point exact | Protege par |
|-----|------------|-------------|-------------|
| Rouge (V_BATT) | TP1 | Apres R_s1 | R_s1 10kΩ |
| Orange (V_D1) | TP2 | Apres R_s2 | R_s2 10kΩ |
| Jaune (V_SW) | TP3 | Apres R_s3 | R_s3 10kΩ |
| Rouge (V_PROT) | TP4 | Apres R_s4 | R_s4 10kΩ |
| Noir (GND) | TP_GND | Direct J1- | - |

## Methode de soudure

| Etape | Action |
|-------|--------|
| 1 | Denuder 3mm au bout du fil |
| 2 | Etamer le fil |
| 3 | Ajouter une goutte de soudure sur le point TP |
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

## Tensions attendues (Circuit V1.9)

| Borne | Nom | SW1 ON | SW1 OFF | Si hors plage |
|-------|-----|--------|---------|---------------|
| 1 | V_BATT | 12.0 - 16.8V | 12.0 - 16.8V | Batterie HS |
| 2 | V_D1 | 11.5 - 16.3V | 11.5 - 16.3V | D1 defaillante |
| 3 | V_SW | 11.5 - 16.3V | 0V | SW1 ou F1 HS |
| 4 | V_PROT | 11.0 - 15.8V | 0V | NTC HS |
| 6 | GND | 0V (ref) | 0V (ref) | - |

## Precision des mesures

| Parametre | Valeur |
|-----------|--------|
| Resistance serie | 10kΩ (sur PCB) |
| Impedance multimetre | 10MΩ (typique) |
| Erreur diviseur | 10k / (10k + 10M) = 0.1% |
| Precision mesure | 99.9% |

**Les resistances 10kΩ n'affectent PAS la precision des mesures.**

---

# DIAGNOSTIC AVEC BREAKOUT BOX

| Symptome | Mesure a faire | Interpretation |
|----------|----------------|----------------|
| Rien ne marche | V_BATT | 0V = batterie debranchee |
| Rien ne marche | V_D1 vs V_BATT | Diff > 1V = D1 inversee |
| Rien apres allumage | V_SW | 0V = SW1 OFF ou F1 grille |
| Ampli demarre pas | V_PROT | < 11V = batterie vide |
| Son coupe par moments | V_PROT sous charge | Chute > 2V = probleme alim |

---

# COMPARAISON VERSIONS

| Aspect | V1.4 | V1.5 |
|--------|------|------|
| Protection court-circuit | ❌ AUCUNE | ✅ R_sense 10kΩ |
| I_max si CC fils | 200A | **1.4mA** |
| Risque incendie | ❌ ELEVE | ✅ ZERO |
| Precision mesure | 100% | 99.9% |
| Necessite Circuit | V1.8 | **V1.9** |
| Impact audio | Aucun | Aucun |

---

# ⚠️ PRECAUTIONS

| # | Precaution |
|---|------------|
| 1 | Verifier que le PCB est V1.9 (avec R_sense) |
| 2 | Ne pas tirer sur les fils (soudures fragiles) |
| 3 | Verifier isolation gaines thermo |
| 4 | Peut rester branchee en permanence (securisee) |

---

# SI TU AS UN CIRCUIT V1.8 OU ANTERIEUR

**Option 1 : Mettre a jour vers V1.9**
- Ajouter 4 resistances 10kΩ sur le PCB
- Creer les points TP

**Option 2 : Ajouter resistances dans la breakout box**
- Souder R 10kΩ en serie sur chaque fil DANS le boitier breakout
- Moins propre mais fonctionne

**Option 3 : Ne pas utiliser de breakout box**
- Mesurer directement sur le PCB avec pointes de touche
- Plus risque mais ponctuel OK

---

# CHANGELOG

| Version | Date | Modifications |
|---------|------|---------------|
| V1.5 | 14 Dec 2025 | Securisation : R_sense sur PCB, zero risque incendie |
| V1.4 | 14 Dec 2025 | Mode observation parallele (DANGEREUX - obsolete) |
| V1.3 | 14 Dec 2025 | GND relie sur tous blocs |
| V1.0 | 14 Dec 2025 | Version initiale |

---

**FIN BREAKOUT BOX V1.5**
