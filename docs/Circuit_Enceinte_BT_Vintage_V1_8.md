# ENCEINTE BLUETOOTH VINTAGE V1.8

**Version:** 1.8  
**Date:** 14 Decembre 2025  
**Mode:** MONO (1 seul haut-parleur)

---

# ⚠️ AVERTISSEMENTS CRITIQUES

| # | Avertissement |
|---|---------------|
| 1 | **HP OBLIGATOIRE ≥ 8Ω** — Mesurer au multimetre : DCR doit etre ≥ 5.5Ω |
| 2 | **NE JAMAIS charger avec SW1 sur ON** — Eteindre AVANT de brancher chargeur |
| 3 | **Attendre 30 secondes entre OFF et ON** — NTC doit refroidir |
| 4 | **Recharger si IND1 < 25%** — Comportement erratique sous 12V |
| 5 | **Verifier polarite AVANT de brancher batterie** — Rouge = +, Noir = - |
| 6 | **Volume app 4Stream max 90%** — Evite clipping en crete |

---

# CHANGELOG V1.8 (Audit Certifie)

| Modif | Raison | Impact |
|-------|--------|--------|
| PTC retiree | Compression audio, protections internes ampli suffisent | Audio propre |
| Snubber SW1 | Arc DC erode contacts, rating AC ≠ DC | Duree vie x50 |
| IND1 avant SW1 | Voir niveau batterie pendant charge | UX amelioree |
| NTC surelever 10mm | Evite surchauffe PCB | Fiabilite |
| Seuil HP 5.5Ω | Marge securite PBTL | Protection ampli |
| TVS P6KE22CA | Marge vs chargeur a vide | Pas de conduction parasite |

---

# ORDRE DE REALISATION

| Etape | Quoi | Temps |
|-------|------|-------|
| 1 | Commander les composants | 5 min |
| 2 | Attendre livraison | 1-2 sem |
| 3 | Verifier impedance HP | 2 min |
| 4 | Configurer Up2Stream en MONO | 2 min |
| 5 | Souder la carte protection | 45 min |
| 6 | Fabriquer la breakout box (optionnel) | 25 min |
| 7 | Preparer les fils | 15 min |
| 8 | Brancher | 15 min |

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
| SW1 | Interrupteur a bascule 10A | "interrupteur bascule 10A" | 3 EUR |
| R_snub | Resistance snubber | "resistance 47 ohm 1W" | 0.50 EUR |
| C_snub | Condensateur snubber | "condensateur 100nF 50V X2" | 0.50 EUR |
| F1 | Porte-fusible + fusible 6.3A slow | "porte fusible 5x20 + fusible 6.3A slow blow" | 3 EUR |
| D1 | Diode Schottky anti-inversion | "1N5822 diode Schottky 5A" | 1 EUR |
| NTC1 | Thermistance inrush | "NTC inrush limiter 2.5 ohm 5A" | 2 EUR |
| TVS1 | Diode protection | "P6KE22CA" | 1 EUR |
| IND1 | Indicateur niveau batterie | "4S battery indicator LED" | 2 EUR |
| C1 | Condensateur decouplage | "100nF ceramique 50V" | 0.50 EUR |
| C2 | Condensateur reservoir | "100uF 25V electrolytique" | 0.50 EUR |

## Composants breakout box (optionnel)

| Quoi | Qte | Prix |
|------|-----|------|
| Bornier 6 positions 5mm | 1 | 2 EUR |
| Boitier plastique ABS 100x60x25mm | 1 | 3 EUR |
| Fil 0.25mm2 couleurs | 2m | 1 EUR |

## Divers

| Quoi | Prix |
|------|------|
| Veroboard 80x50mm | 2 EUR |
| Borniers 2 positions pour carte (x2) | 1 EUR |
| Fil 1.5mm2 rouge 1m | 2 EUR |
| Fil 1.5mm2 noir 1m | 2 EUR |
| Fil 1.0mm2 rouge 1m | 1 EUR |
| Fil 1.0mm2 noir 1m | 1 EUR |
| Fil 0.75mm2 rouge 1m | 1 EUR |
| Ferrite clip-on 5mm | 1 EUR |
| Entretoises 10mm (x4) | 1 EUR |

**TOTAL : ~168 EUR**

---

# ETAPE 3 : VERIFIER IMPEDANCE HP

**A faire AVANT tout branchement.**

## Ce que tu fais

| Action | Detail |
|--------|--------|
| 1 | Mettre multimetre en mode Ohms (Ω) |
| 2 | Toucher les deux bornes du HP avec les pointes |
| 3 | Lire la valeur DCR (resistance en continu) |

## Resultat attendu (MISE A JOUR V1.8)

| Lecture DCR | Z nominale | Z vue PBTL | Verdict |
|-------------|------------|------------|---------|
| < 4Ω | 4Ω | 2Ω | ❌ INTERDIT mono - Utiliser STEREO |
| 4 - 5.5Ω | 6Ω | 3Ω | ⚠️ LIMITE - Volume max 70% |
| 5.5 - 8Ω | 8Ω | 4Ω | ✅ OK |
| > 8Ω | 16Ω | 8Ω | ✅ OK |
| OL / infini | - | - | ❌ HP coupe, NE PAS UTILISER |

**Si HP < 5.5Ω : Utiliser mode STEREO et brancher sur UN SEUL canal (L+ et L-).**

---

# ETAPE 4 : CONFIGURER UP2STREAM EN MONO

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

# ETAPE 5 : SOUDER LA CARTE PROTECTION

## Schema bloc V1.8 (ordre du courant)

```
BATT+ ─┬─ IND1+ (indicateur TOUJOURS alimente)
       │
       └─ J1+ → D1(anode→cathode) → [SW1 // Snubber] → F1 → NTC1 → J2+ → AMP
                                         │
                                    R_snub+C_snub
                                    (47Ω + 100nF)

BATT- ─┬─ IND1-
       │
       └─ J1- ──────────────────────────────────────────────────→ J2- → AMP
                                                          TVS1 (parallele J2)
                                                          C1+C2 (parallele J2)
```

**NOTA V1.8 : PTC RETIREE (protections internes ampli suffisent)**

## Tu commences par

1. Couper le veroboard a 80x50mm
2. Souder J1 (bornier entree) a gauche
3. Souder J2 (bornier sortie) a droite

## Ensuite tu soudes dans cet ordre

| Ordre | Composant | Position sur carte | Notes |
|-------|-----------|-------------------|-------|
| 1 | J1 (bornier entree 2 positions) | Bord gauche | - |
| 2 | J2 (bornier sortie 2 positions) | Bord droit | - |
| 3 | D1 (1N5822 Schottky) | Apres J1+, bague cote SW1 | BAGUE = CATHODE = SORTIE |
| 4 | NTC1 (thermistance 2.5Ω) | Centre, **SURELEVER 10mm** | Utiliser entretoises ou plier pattes |
| 5 | TVS1 (diode P6KE22CA) | Parallele entre J2+ et J2- | Pas de sens (bidirectionnel) |
| 6 | C1 (100nF ceramique) | Parallele J2, au plus pres | - |
| 7 | C2 (100µF electrolytique) | Parallele J2, + vers J2+ | RESPECTER POLARITE |
| 8 | R_snub (47Ω 1W) | A cote trous SW1 | Sera en parallele de SW1 |
| 9 | C_snub (100nF X2) | En serie avec R_snub | Classe X2 obligatoire (securite) |

## Connexions a faire sur la carte

### Piste ou fil entre :

| De | Vers | Comment |
|----|------|---------|
| J1 borne 1 (entree +) | D1 anode (cote sans bague) | Piste cuivre |
| D1 cathode (cote bague) | Trou pour fil SW1-A | Piste cuivre |
| Trou retour SW1-B | Trou pour fil F1 entree | Piste cuivre |
| Trou retour F1 | NTC1 patte 1 | Fil rouge court |
| NTC1 patte 2 | J2 borne 1 (sortie +) | Piste cuivre |
| J1 borne 2 (entree -) | J2 borne 2 (sortie -) | Piste cuivre continue |
| TVS1 patte 1 | J2 borne 1 (sortie +) | Piste cuivre |
| TVS1 patte 2 | J2 borne 2 (sortie -) | Piste cuivre |
| C1 patte 1 | J2 borne 1 (sortie +) | Piste cuivre |
| C1 patte 2 | J2 borne 2 (sortie -) | Piste cuivre |
| C2 patte + | J2 borne 1 (sortie +) | Piste cuivre |
| C2 patte - | J2 borne 2 (sortie -) | Piste cuivre |

### Snubber (NOUVEAU V1.8)

| De | Vers | Comment |
|----|------|---------|
| Trou SW1-A | R_snub patte 1 | Piste cuivre |
| R_snub patte 2 | C_snub patte 1 | Fil court |
| C_snub patte 2 | Trou SW1-B | Piste cuivre |

**Resultat : R_snub + C_snub en serie, le tout en parallele de SW1**

### Fils pour composants deportes

| Fil | Section | Longueur | De (carte) | Vers (boitier) |
|-----|---------|----------|------------|----------------|
| A | 0.75mm2 rouge | 20cm | D1 cathode (trou SW1-A) | SW1 (inter) borne 1 |
| B | 0.75mm2 rouge | 20cm | Noeud apres SW1 (trou SW1-B) | SW1 (inter) borne 2 |
| C | 0.75mm2 rouge | 20cm | Noeud apres SW1 | F1 (fusible) entree |
| D | 0.75mm2 rouge | 20cm | Vers NTC1 patte 1 | F1 (fusible) sortie |
| E | 0.5mm2 rouge | 15cm | **J1 borne 1 (AVANT D1)** | IND1 fil + |
| F | 0.5mm2 noir | 15cm | J1 borne 2 (entree -) | IND1 fil - |

**NOTA V1.8 : IND1 branche AVANT D1 et SW1 → affiche niveau batterie meme enceinte eteinte**

## Tu finis par

Verifier au multimetre :

| Test | Mode | Attendu |
|------|------|---------|
| J1+ vers D1 cathode | Diode | 0.3-0.5V (sens passant) |
| D1 cathode vers J1+ | Diode | OL (bloque) |
| J1- vers J2- | Continuite | Bip |
| C2 polarite | Visuel | + vers J2+ |
| SW1-A vers SW1-B (SW1 ouvert) | Ohms | ~47Ω (snubber) |
| SW1-A vers SW1-B (SW1 ferme) | Continuite | Bip |

---

# ETAPE 6 : FABRIQUER LA BREAKOUT BOX

Voir document separe **Breakout_Box_V1.4.md**

**NOTA V1.8 : Nouvelle version "observation parallele" sans insertion serie.**

---

# ETAPE 7 : PREPARER LES FILS

## Liste complete des fils a couper et denuder

| # | Section | Couleur | Longueur | De | Vers |
|---|---------|---------|----------|-----|------|
| 1 | 1.5mm2 | Rouge | 15cm | Batterie fil + | J1 borne 1 (entree carte +) |
| 2 | 1.5mm2 | Noir | 15cm | Batterie fil - | J1 borne 2 (entree carte -) |
| 3 | 1.5mm2 | Rouge | 15cm | J2 borne 1 (sortie carte +) | Up2Stream borne V+ |
| 4 | 1.5mm2 | Noir | 15cm | J2 borne 2 (sortie carte -) | Up2Stream borne GND |
| 5 | 1.0mm2 | Rouge | 30cm | Up2Stream borne 1 (R+) | HP borne + |
| 6 | 1.0mm2 | Noir | 30cm | Up2Stream borne 3 (L+) | HP borne - |

## Preparation fils HP

| Action | Detail |
|--------|--------|
| 1 | Couper fils 5 et 6 a 30cm chacun |
| 2 | Les TORSADER ensemble (1 tour par 2cm) |
| 3 | Resultat : paire torsadee rouge/noir |

---

# ETAPE 8 : BRANCHER

## Tu commences par (ordre obligatoire)

| Ordre | Action | Detail |
|-------|--------|--------|
| 1 | Visser antenne WiFi | Gros connecteur SMA sur Up2Stream |
| 2 | Visser antenne Bluetooth | Petit connecteur SMA sur Up2Stream |
| 3 | Clipser ferrite | Sur fils 3+4 groupes, pres de Up2Stream |
| 4 | Brancher HP | Fil rouge sur borne 1 (R+), fil noir sur borne 3 (L+) |
| 5 | Brancher carte vers Up2Stream | Fil 3 sur V+, fil 4 sur GND |
| 6 | Verifier SW1 (inter) sur OFF | Position basse ou 0 |
| 7 | VERIFIER POLARITE | Rouge batterie = + , Noir batterie = - |
| 8 | Brancher batterie vers carte | Fil 1 sur J1+, fil 2 sur J1- |

## Tu finis par

Mettre SW1 (inter) sur ON et verifier que :

| Quoi | Attendu |
|------|---------|
| IND1 (LED niveau) | Deja allume (branche avant SW1) |
| Up2Stream LED | Bleue clignote |
| HP | Pas de bruit fort (leger souffle OK) |

---

# RECHARGE (MISE A JOUR V1.8)

| Etape | Action |
|-------|--------|
| 1 | **ETEINDRE** l'enceinte avec SW1 (inter) — OBLIGATOIRE |
| 2 | IND1 reste allume et montre niveau actuel |
| 3 | Brancher chargeur secteur sur prise batterie |
| 4 | IND1 montre progression charge |
| 5 | Toutes LEDs IND1 allumees = termine (2-3h) |
| 6 | Debrancher chargeur |
| 7 | Rallumer avec SW1 si besoin |

**❌ NE JAMAIS charger avec SW1 sur ON — Risque bruit audio et oscillations chargeur**

---

# SPECIFICATIONS TECHNIQUES V1.8

| Parametre | Valeur |
|-----------|--------|
| Tension entree | 12.0V - 16.8V (4S Li-Ion) |
| Courant max | 5A continu, 7A crete |
| Puissance max | 60W mono @ 8Ω |
| Protection inversion | D1 Schottky 1N5822 (Vf=0.4V) |
| Protection surtension | TVS P6KE22CA (V_RWM=18.8V, V_clamp=30.6V) |
| Protection surintensité | F1 6.3A slow-blow |
| Protection inrush | NTC 2.5Ω (sureleve 10mm) |
| Protection arc DC | Snubber 47Ω + 100nF X2 |
| Decouplage | 100nF ceramique + 100µF electro |
| Impedance HP mini | 8Ω (DCR ≥ 5.5Ω) |

---

# BILAN PROTECTIONS V1.8

| Defaut | Protection | Temps reaction |
|--------|------------|----------------|
| Inversion polarite | D1 Schottky bloque | Instantane |
| Surtension >22V | TVS P6KE22CA clampe | <1µs |
| Court-circuit | F1 6.3A fond | 10ms-2s |
| Inrush demarrage | NTC 2.5Ω limite | 50ms |
| Arc extinction SW1 | Snubber absorbe | 5µs |
| HP court-circuit | OCP interne ampli | <1ms |
| Surchauffe ampli | OTP interne ampli | Continu |

---

# DEPANNAGE

| Symptome | Cause probable | Solution |
|----------|----------------|----------|
| Rien ne s'allume | Polarite inversee | Verifier + et - batterie |
| Rien ne s'allume | Fusible F1 grille | Remplacer fusible |
| IND1 allume mais pas ampli | SW1 OFF ou D1 HS | Verifier SW1, tester D1 |
| S'allume puis s'eteint | Batterie vide (<12V) | Recharger |
| Son distordu fort volume | HP impedance trop basse | Verifier DCR ≥ 5.5Ω |
| Sifflement aigu | EMI antenne BT | Eloigner fils alim des antennes |
| Bruit pendant charge | Charge avec SW1 ON | ETEINDRE avant charger |
| Contacts SW1 colles | Snubber absent/HS | Verifier R_snub et C_snub |
| Chauffe excessive NTC | NTC touche PCB | Surelever a 10mm |

---

# CHANGELOG COMPLET

| Version | Date | Modifications |
|---------|------|---------------|
| V1.8 | 14 Dec 2025 | Audit certifie : PTC retiree, snubber SW1, IND1 avant SW1, NTC 10mm, seuil HP 5.5Ω |
| V1.7 | 14 Dec 2025 | Audit : D1 anti-inversion, TVS 22CA, PTC 5A, F1 6.3A, decouplage, ferrite |
| V1.6 | 14 Dec 2025 | Refs explicites, ordre clair |

---

**FIN CIRCUIT V1.8**
