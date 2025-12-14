# BREAKOUT BOX - ENCEINTE BLUETOOTH VINTAGE V1.2

**Version:** 1.2  
**Date:** 14 Decembre 2025

---

# A QUOI CA SERT

La breakout box te permet de mesurer les tensions a 6 endroits du circuit sans rien demonter. Tu branches ton multimetre sur le bornier TP et tu lis.

---

# ORDRE DE FABRICATION

| Etape | Quoi | Temps |
|-------|------|-------|
| 1 | Percer le boitier | 10 min |
| 2 | Fixer les borniers | 5 min |
| 3 | Cabler l'interieur | 15 min |
| 4 | Marquer le boitier | 5 min |

---

# COMPOSANTS BREAKOUT BOX

| Ref | Quoi | Qte |
|-----|------|-----|
| TB1-A | Bornier 2 positions (entree batterie) | 1 |
| TB2-A | Bornier 2 positions (sortie batterie) | 1 |
| TB1-B | Bornier 2 positions (entree post-inter) | 1 |
| TB2-B | Bornier 2 positions (sortie post-inter) | 1 |
| TB1-C | Bornier 2 positions (entree post-protections) | 1 |
| TB2-C | Bornier 2 positions (sortie post-protections) | 1 |
| TP | Bornier 6 positions (points de test) | 1 |
| - | Boitier plastique 100x60x25mm | 1 |
| - | Fil 1.5mm2 rouge | 50cm |
| - | Fil 1.5mm2 noir | 30cm |
| - | Vis M3x10 + ecrous | 8 |

---

# ETAPE 1 : PERCER LE BOITIER

## Position des trous

| Zone | Quoi | Position |
|------|------|----------|
| Gauche haut | TB1-A (entree batterie) | 2 trous espaces de 5mm |
| Gauche milieu | TB1-B (entree post-inter) | 2 trous espaces de 5mm |
| Gauche bas | TB1-C (entree post-protections) | 2 trous espaces de 5mm |
| Droite haut | TB2-A (sortie batterie) | 2 trous espaces de 5mm |
| Droite milieu | TB2-B (sortie post-inter) | 2 trous espaces de 5mm |
| Droite bas | TB2-C (sortie post-protections) | 2 trous espaces de 5mm |
| Centre droite | TP (points de test) | 6 trous espaces de 5mm |

---

# ETAPE 2 : FIXER LES BORNIERS

## Tu commences par

Visser TB1-A (entree batterie) en haut a gauche.

## Ordre de fixation

| Ordre | Bornier | Position |
|-------|---------|----------|
| 1 | TB1-A (entree batterie) | Gauche haut |
| 2 | TB2-A (sortie batterie) | Droite haut |
| 3 | TB1-B (entree post-inter) | Gauche milieu |
| 4 | TB2-B (sortie post-inter) | Droite milieu |
| 5 | TB1-C (entree post-protections) | Gauche bas |
| 6 | TB2-C (sortie post-protections) | Droite bas |
| 7 | TP (points de test) | Centre droite |

---

# ETAPE 3 : CABLER L'INTERIEUR

## Tu commences par

Cabler le bloc batterie (TB1-A vers TB2-A et vers TP).

## Bloc BATTERIE - Fils a souder

| # | Fil | De | Vers |
|---|-----|-----|------|
| 1 | Rouge 5cm | TB1-A borne 1 (entree +) | TB2-A borne 1 (sortie +) |
| 2 | Rouge 3cm | TB1-A borne 1 (entree +) | TP borne 1 (test V_BATT) |
| 3 | Noir 5cm | TB1-A borne 2 (entree -) | TB2-A borne 2 (sortie -) |
| 4 | Noir 3cm | TB1-A borne 2 (entree -) | TP borne 6 (test GND) |

## Bloc POST-INTER - Fils a souder

| # | Fil | De | Vers |
|---|-----|-----|------|
| 5 | Rouge 5cm | TB1-B borne 1 (entree post-inter) | TB2-B borne 1 (sortie post-inter) |
| 6 | Rouge 3cm | TB1-B borne 1 (entree post-inter) | TP borne 2 (test V_SW) |

TB1-B borne 2 et TB2-B borne 2 : tu ne branches rien.

## Bloc POST-PROTECTIONS - Fils a souder

| # | Fil | De | Vers |
|---|-----|-----|------|
| 7 | Rouge 5cm | TB1-C borne 1 (entree post-prot) | TB2-C borne 1 (sortie post-prot) |
| 8 | Rouge 3cm | TB1-C borne 1 (entree post-prot) | TP borne 5 (test V_PROT) |

TB1-C borne 2 et TB2-C borne 2 : tu ne branches rien.

## Tu finis par

Verifier au multimetre (mode continuite) :

| Test | Doit sonner |
|------|-------------|
| TB1-A borne 1 | TB2-A borne 1 ET TP borne 1 |
| TB1-A borne 2 | TB2-A borne 2 ET TP borne 6 |
| TB1-B borne 1 | TB2-B borne 1 ET TP borne 2 |
| TB1-C borne 1 | TB2-C borne 1 ET TP borne 5 |

---

# ETAPE 4 : MARQUER LE BOITIER

## Texte a ecrire au marqueur

| Position | Texte |
|----------|-------|
| Au-dessus TB1-A | BATT IN |
| Au-dessus TB2-A | BATT OUT |
| Au-dessus TB1-B | SW OUT |
| Au-dessus TB2-B | FUSE IN |
| Au-dessus TB1-C | PROT OUT |
| Au-dessus TB2-C | AMP IN |
| A cote TP borne 1 | 1: BATT |
| A cote TP borne 2 | 2: SW |
| A cote TP borne 5 | 5: PROT |
| A cote TP borne 6 | 6: GND |

---

# BORNIER TP - CE QUE TU MESURES

| Borne TP | Nom | Tension attendue inter ON | Tension attendue inter OFF |
|----------|-----|---------------------------|----------------------------|
| 1 | V_BATT | 12 a 16.8V | 12 a 16.8V |
| 2 | V_SW | 12 a 16.8V | 0V |
| 3 | (reserve) | - | - |
| 4 | (reserve) | - | - |
| 5 | V_PROT | 11.8 a 16.5V | 0V |
| 6 | GND | 0V (reference) | 0V (reference) |

---

# CHANGELOG

| Version | Date | Modifications |
|---------|------|---------------|
| V1.2 | 14 Dec 2025 | Refs explicites entre parentheses, ordre clair |
| V1.1 | 14 Dec 2025 | Suppression schemas ASCII |
| V1.0 | 14 Dec 2025 | Version initiale |

---

**FIN BREAKOUT BOX V1.2**
