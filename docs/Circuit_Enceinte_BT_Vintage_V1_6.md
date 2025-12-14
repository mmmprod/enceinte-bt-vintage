# ENCEINTE BLUETOOTH VINTAGE V1.6

**Version:** 1.6  
**Date:** 14 Decembre 2025  
**Mode:** MONO (1 seul haut-parleur)

---

# ORDRE DE REALISATION

| Etape | Quoi | Temps |
|-------|------|-------|
| 1 | Commander les composants | 5 min |
| 2 | Attendre livraison | 1-2 sem |
| 3 | Configurer Up2Stream en MONO | 2 min |
| 4 | Souder la carte protection | 30 min |
| 5 | Fabriquer la breakout box | 20 min |
| 6 | Preparer les fils | 15 min |
| 7 | Brancher | 15 min |

---

# ETAPE 1 : COMMANDER

## A acheter tout fait

| Quoi | Recherche | Prix |
|------|-----------|------|
| Batterie 4S 6Ah avec BMS | "14.8V 6Ah 18650 battery pack BMS" sur AliExpress | 45 EUR |
| Chargeur 16.8V 2A | "16.8V 2A lithium battery charger" sur AliExpress | 12 EUR |
| Up2Stream Amp V4 | "Up2Stream Amp V4" sur arylic.com ou Amazon | 80 EUR |

## Composants carte protection

| Ref | Quoi | Recherche | Prix |
|-----|------|-----------|------|
| SW1 | Interrupteur a bascule | "interrupteur bascule 10A" | 3 EUR |
| F1 | Porte-fusible + fusible 5A | "porte fusible 5x20 + fusible 5A" | 3 EUR |
| NTC1 | Thermistance inrush | "NTC inrush limiter 2.5 ohm" | 2 EUR |
| PTC1 | Fusible resetable | "PTC resettable fuse 3A" | 1 EUR |
| TVS1 | Diode protection | "P6KE20CA" | 1 EUR |
| IND1 | Indicateur niveau batterie | "4S battery indicator LED" | 2 EUR |

## Composants breakout box

| Quoi | Qte | Prix |
|------|-----|------|
| Bornier 2 positions 5mm | 6 | 3 EUR |
| Bornier 6 positions 5mm | 1 | 2 EUR |
| Boitier plastique 100x60x25mm | 1 | 3 EUR |

## Divers

| Quoi | Prix |
|------|------|
| Veroboard 60x40mm | 2 EUR |
| Borniers 2 positions pour carte (x2) | 1 EUR |
| Fil 1.5mm2 rouge 1m | 2 EUR |
| Fil 1.5mm2 noir 1m | 2 EUR |
| Fil 1.0mm2 rouge 1m | 1 EUR |
| Fil 1.0mm2 noir 1m | 1 EUR |
| Fil 0.75mm2 rouge 1m | 1 EUR |

**TOTAL : ~167 EUR**

---

# ETAPE 3 : CONFIGURER UP2STREAM EN MONO

**A faire AVANT de brancher quoi que ce soit.**

## Ou sont les jumpers

Sur la carte Up2Stream, pres du bornier haut-parleur, il y a 4 petits cavaliers noirs sur 3 rangees de picots.

## Ce que tu fais

| Action | Detail |
|--------|--------|
| 1 | Prendre une pince fine |
| 2 | Retirer les 4 cavaliers de leur position actuelle (HAUT + MILIEU) |
| 3 | Les remettre sur MILIEU + BAS |
| 4 | Verifier qu'ils sont bien enfonces |

## Resultat

| Position | Mode |
|----------|------|
| HAUT + MILIEU | Stereo (usine) |
| MILIEU + BAS | MONO (ce qu'on veut) |

---

# ETAPE 4 : SOUDER LA CARTE PROTECTION

## Tu commences par

1. Couper le veroboard a 60x40mm
2. Souder J1 (bornier entree) a gauche
3. Souder J2 (bornier sortie) a droite

## Ensuite tu soudes dans cet ordre

| Ordre | Composant | Position sur carte |
|-------|-----------|-------------------|
| 1 | J1 (bornier entree 2 positions) | Bord gauche |
| 2 | J2 (bornier sortie 2 positions) | Bord droit |
| 3 | NTC1 (thermistance 2.5 ohms) | Centre, laisser 3mm autour car chauffe |
| 4 | PTC1 (fusible resetable 3A) | Entre NTC1 et J2 |
| 5 | TVS1 (diode P6KE20CA) | Parallele entre J2+ et J2-, pas de sens |

## Connexions a faire sur la carte

### Piste ou fil entre :

| De | Vers | Comment |
|----|------|---------|
| J1 borne 1 (entree +) | Trou pour fil SW1 | Piste cuivre |
| Trou retour SW1 | Trou pour fil F1 entree | Piste cuivre |
| Trou retour F1 | NTC1 patte 1 | Fil rouge court ou piste |
| NTC1 patte 2 | PTC1 patte 1 | Fil rouge court ou piste |
| PTC1 patte 2 | J2 borne 1 (sortie +) | Piste cuivre |
| J1 borne 2 (entree -) | J2 borne 2 (sortie -) | Piste cuivre continue |
| TVS1 patte 1 | J2 borne 1 (sortie +) | Piste cuivre |
| TVS1 patte 2 | J2 borne 2 (sortie -) | Piste cuivre |

### Fils pour composants deportes

| Fil | Section | Longueur | De (carte) | Vers (boitier) |
|-----|---------|----------|------------|----------------|
| A | 0.75mm2 rouge | 20cm | J1 borne 1 (entree +) | SW1 (inter) borne 1 |
| B | 0.75mm2 rouge | 20cm | Noeud apres SW1 | SW1 (inter) borne 2 |
| C | 0.75mm2 rouge | 20cm | Noeud apres SW1 | F1 (fusible) entree |
| D | 0.75mm2 rouge | 20cm | Vers NTC1 patte 1 | F1 (fusible) sortie |
| E | 0.5mm2 rouge | 15cm | Noeud apres SW1 | IND1 (LED niveau) fil + |
| F | 0.5mm2 noir | 15cm | J1 borne 2 (entree -) | IND1 (LED niveau) fil - |

## Tu finis par

Verifier au multimetre (mode continuite) :
- J1 borne 1 sonne avec le trou SW1 borne 1
- J1 borne 2 sonne avec J2 borne 2

---

# ETAPE 5 : FABRIQUER LA BREAKOUT BOX

Voir document separe Breakout_Box_V1.1.md

---

# ETAPE 6 : PREPARER LES FILS

## Liste complete des fils a couper et denuder

| # | Section | Couleur | Longueur | De | Vers |
|---|---------|---------|----------|-----|------|
| 1 | 1.5mm2 | Rouge | 15cm | Batterie fil + | J1 borne 1 (entree carte +) |
| 2 | 1.5mm2 | Noir | 15cm | Batterie fil - | J1 borne 2 (entree carte -) |
| 3 | 1.5mm2 | Rouge | 15cm | J2 borne 1 (sortie carte +) | Up2Stream borne V+ |
| 4 | 1.5mm2 | Noir | 15cm | J2 borne 2 (sortie carte -) | Up2Stream borne GND |
| 5 | 1.0mm2 | Rouge | 30cm | Up2Stream borne 1 (R+) | HP borne + |
| 6 | 1.0mm2 | Noir | 30cm | Up2Stream borne 3 (L+) | HP borne - |

---

# ETAPE 7 : BRANCHER

## Tu commences par (ordre obligatoire)

| Ordre | Action | Detail |
|-------|--------|--------|
| 1 | Visser antenne WiFi | Gros connecteur SMA sur Up2Stream |
| 2 | Visser antenne Bluetooth | Petit connecteur SMA sur Up2Stream |
| 3 | Brancher HP | Fil rouge sur borne 1 (R+), fil noir sur borne 3 (L+) |
| 4 | Brancher carte vers Up2Stream | Fil 3 sur V+, fil 4 sur GND |
| 5 | Verifier SW1 (inter) sur OFF | Position basse ou 0 |
| 6 | Brancher batterie vers carte | Fil 1 sur J1+, fil 2 sur J1- |

## Tu finis par

Mettre SW1 (inter) sur ON et verifier que :
- IND1 (LED niveau) s'allume
- Up2Stream LED bleue clignote

---

# UTILISATION BREAKOUT BOX (optionnel)

Si tu veux utiliser la breakout box pour mesurer, tu modifies le cablage :

## Insertion entre batterie et carte

| Sans breakout | Avec breakout |
|---------------|---------------|
| Batterie + vers J1 borne 1 | Batterie + vers TB1-A borne 1 (entree breakout) |
| - | TB2-A borne 1 (sortie breakout) vers J1 borne 1 |
| Batterie - vers J1 borne 2 | Batterie - vers TB1-A borne 2 (entree breakout) |
| - | TB2-A borne 2 (sortie breakout) vers J1 borne 2 |

## Insertion apres interrupteur

| Sans breakout | Avec breakout |
|---------------|---------------|
| SW1 (inter) borne 2 vers F1 (fusible) | SW1 borne 2 vers TB1-B borne 1 (entree breakout) |
| - | TB2-B borne 1 (sortie breakout) vers F1 (fusible) |

## Insertion apres protections

| Sans breakout | Avec breakout |
|---------------|---------------|
| J2 borne 1 vers Up2Stream V+ | J2 borne 1 vers TB1-C borne 1 (entree breakout) |
| - | TB2-C borne 1 (sortie breakout) vers Up2Stream V+ |

---

# RECHARGE

| Etape | Action |
|-------|--------|
| 1 | Eteindre enceinte avec SW1 (inter) |
| 2 | Brancher chargeur secteur sur prise batterie |
| 3 | LED rouge = en charge |
| 4 | LED verte = termine (2-3h) |
| 5 | Debrancher chargeur |

---

# CHANGELOG

| Version | Date | Modifications |
|---------|------|---------------|
| V1.6 | 14 Dec 2025 | Refs explicites entre parentheses, ordre clair |
| V1.5 | 14 Dec 2025 | Integration breakout box |
| V1.4 | 14 Dec 2025 | Format tableaux |

---

**FIN CIRCUIT V1.6**
