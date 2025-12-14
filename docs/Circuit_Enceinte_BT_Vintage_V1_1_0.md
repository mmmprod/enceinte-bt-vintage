# ENCEINTE BLUETOOTH VINTAGE V1.10

**Version:** 1.10  
**Date:** 14 Decembre 2025  
**Mode:** MONO (1 seul haut-parleur)

---

# ⚠️ AVERTISSEMENTS CRITIQUES

| # | Avertissement |
|---|---------------|
| 1 | **HP OBLIGATOIRE ≥ 8Ω** — Mesurer au multimetre : DCR doit etre ≥ 5.5Ω |
| 2 | **NE JAMAIS charger avec SW1 sur ON** — Bruit audio et coupures possibles |
| 3 | **Attendre 30 secondes entre OFF et ON** — NTC doit refroidir |
| 4 | **UNIQUEMENT chargeur 16.8V 2A** — Autre chargeur = destruction circuit |
| 5 | **Debrancher batterie si stockage > 2 semaines** — IND1 vide le pack |
| 6 | **Ventilation obligatoire** — Ne pas enfermer le module, T max 40°C |
| 7 | **Leger "plop" a l'extinction = normal** — Pas de dommage |

---

# CHANGELOG V1.10 (Audit Externe V2)

| Modif | Raison | Impact |
|-------|--------|--------|
| D1 → SB560 | 1N5822 = 3A, sous-dimensionnee pour 5A | Fiabilite |
| NTC → 7A | 5A au plafond, vieillissement | Duree vie |
| C3 bulk 1000µF | Brownout sur basses fortes | Audio propre |
| Puissance 60W → 30W | Spec fausse (24V vs 14.8V) | Doc correcte |
| R_sense → 1kΩ | Standard industrie, meilleure compatibilite | Precision |
| C_snub 100V film | "50V X2" incoherent | Fiabilite snubber |
| Warnings renforces | Usage reel ≠ usage ideal | Securite |

---

# SPECIFICATIONS TECHNIQUES V1.10 (CORRIGEES)

| Parametre | Valeur |
|-----------|--------|
| Tension entree | 12.0V - 16.8V (4S Li-Ion) |
| **Puissance max** | **30W typ, 40W crete @ 8Ω** |
| **Courant max** | **3A typ, 5A crete** |
| Protection inversion | D1 Schottky **SB560** (Vf=0.7V, 5A) |
| Protection surtension | TVS P6KE22CA (V_RWM=18.8V, V_clamp=30.6V) |
| Protection surintensité | F1 6.3A slow-blow |
| Protection inrush | NTC 2.5Ω **7A** (sureleve 10mm) |
| Protection arc DC | Snubber 47Ω + 100nF **film 100V** |
| Decouplage carte | 100nF ceramique + 100µF electro |
| **Bulk ampli** | **C3 1000µF 25V low-ESR** |
| Protection fils breakout | R_sense **1kΩ 0.5W** (x4) - I_cc max 17mA |
| Impedance HP mini | 8Ω (DCR ≥ 5.5Ω) |

---

# ORDRE DE REALISATION

| Etape | Quoi | Temps |
|-------|------|-------|
| 1 | Commander les composants | 5 min |
| 2 | Attendre livraison | 1-2 sem |
| 3 | Verifier impedance HP | 2 min |
| 4 | Configurer Up2Stream en MONO | 2 min |
| 5 | Souder la carte protection | 50 min |
| 6 | Fabriquer la breakout box (optionnel) | 20 min |
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

**⚠️ IMPORTANT : Utiliser UNIQUEMENT le chargeur 16.8V 2A. Un chargeur 24V detruit le circuit.**

## Composants carte protection

| Ref | Quoi | Recherche | Prix |
|-----|------|-----------|------|
| SW1 | Interrupteur a bascule 10A | "interrupteur bascule 10A" | 3 EUR |
| R_snub | Resistance snubber | "resistance 47 ohm 1W" | 0.50 EUR |
| C_snub | Condensateur snubber | "condensateur 100nF 100V MKT film" | 0.50 EUR |
| F1 | Porte-fusible + fusible 6.3A slow | "porte fusible 5x20 + fusible 6.3A slow blow" | 3 EUR |
| **D1** | **Diode Schottky 5A** | **"SB560 diode Schottky 5A 60V"** | 1.50 EUR |
| **NTC1** | **Thermistance inrush 7A** | **"NTC inrush limiter 2.5 ohm 7A"** | 3 EUR |
| TVS1 | Diode protection | "P6KE22CA" | 1 EUR |
| IND1 | Indicateur niveau batterie | "4S battery indicator LED" | 2 EUR |
| C1 | Condensateur decouplage | "100nF ceramique 50V" | 0.50 EUR |
| C2 | Condensateur reservoir carte | "100uF 25V electrolytique" | 0.50 EUR |
| **C3** | **Condensateur bulk ampli** | **"1000uF 25V electrolytique low-ESR"** | 2 EUR |
| R_s1-R_s4 | Resistances sense (x4) | **"resistance 1k ohm 0.5W" (x4)** | 0.40 EUR |

## Connecteur recommande (optionnel mais conseille)

| Quoi | Recherche | Prix |
|------|-----------|------|
| Connecteur XT60 male+femelle | "XT60 connector pair" | 2 EUR |

**Le connecteur XT60 empeche de brancher un mauvais chargeur (incompatible laptop).**

## Composants breakout box (optionnel)

| Quoi | Qte | Prix |
|------|-----|------|
| Bornier 6 positions 5mm | 1 | 2 EUR |
| Boitier plastique ABS 60x40x20mm | 1 | 3 EUR |
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

**TOTAL : ~175 EUR**

---

# ETAPE 3 : VERIFIER IMPEDANCE HP

**A faire AVANT tout branchement.**

## Ce que tu fais

| Action | Detail |
|--------|--------|
| 1 | Mettre multimetre en mode Ohms (Ω) |
| 2 | Toucher les deux bornes du HP avec les pointes |
| 3 | Lire la valeur DCR (resistance en continu) |

## Resultat attendu

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

## Schema bloc V1.10 (ordre du courant)

```
BATT+ ─┬─ IND1+ (indicateur TOUJOURS alimente - debrancher si stockage)
       │
       ├─ R_s1 (1kΩ) ─── TP1 (vers breakout V_BATT)
       │
       └─ J1+ → D1(SB560) ─┬─ R_s2 (1kΩ) ─── TP2 (V_D1)
                           │
                           └─ [SW1 // Snubber] → F1 ─┬─ R_s3 (1kΩ) ─── TP3 (V_SW)
                                    │                │
                               R(47Ω)+C(100nF)       └─ NTC1(7A) → J2+ ─┬─ R_s4 (1kΩ) ─── TP4 (V_PROT)
                               (film 100V)                              │
                                                                        └─ → C3(1000µF) → AMP

BATT- ─┬─ IND1-
       │
       └─ J1- ─── TP_GND ────────────────────────────────────────────── J2- → AMP
                                                                  TVS1 + C1 + C2
```

**NOUVEAUTES V1.10 :**
- D1 = SB560 (5A reel, pas 1N5822)
- NTC1 = 7A (pas 5A)
- R_s1-R_s4 = 1kΩ 0.5W (pas 10kΩ)
- C3 = 1000µF bulk pres de l'ampli

## Tu commences par

1. Couper le veroboard a 80x50mm
2. Souder J1 (bornier entree) a gauche
3. Souder J2 (bornier sortie) a droite

## Ensuite tu soudes dans cet ordre

| Ordre | Composant | Position sur carte | Notes |
|-------|-----------|-------------------|-------|
| 1 | J1 (bornier entree 2 positions) | Bord gauche | - |
| 2 | J2 (bornier sortie 2 positions) | Bord droit | - |
| 3 | **D1 (SB560 Schottky 5A)** | Apres J1+, bague cote SW1 | **BAGUE = CATHODE = SORTIE** |
| 4 | **NTC1 (thermistance 2.5Ω 7A)** | Centre, **SURELEVER 10mm** | Utiliser entretoises |
| 5 | TVS1 (diode P6KE22CA) | Parallele entre J2+ et J2- | Pas de sens |
| 6 | C1 (100nF ceramique) | Parallele J2, au plus pres | - |
| 7 | C2 (100µF electrolytique) | Parallele J2, + vers J2+ | RESPECTER POLARITE |
| 8 | R_snub (47Ω 1W) | A cote trous SW1 | En parallele de SW1 |
| 9 | C_snub (100nF **100V film**) | En serie avec R_snub | **PAS ceramique 50V** |
| 10 | **R_s1 (1kΩ 0.5W)** | Entre J1+ et TP1 | Protege fil breakout |
| 11 | **R_s2 (1kΩ 0.5W)** | Entre D1 cathode et TP2 | Protege fil breakout |
| 12 | **R_s3 (1kΩ 0.5W)** | Entre sortie F1 et TP3 | Protege fil breakout |
| 13 | **R_s4 (1kΩ 0.5W)** | Entre J2+ et TP4 | Protege fil breakout |

## Points de test TP

Les points TP1 a TP4 et TP_GND sont des trous ou tu peux :
- Soit souder les fils de la breakout box
- Soit utiliser des picots males pour mesure directe

| Point | Connecte a | Via | Mesure |
|-------|------------|-----|--------|
| TP1 | J1 borne 1 (BATT+) | R_s1 1kΩ | V_BATT |
| TP2 | D1 cathode | R_s2 1kΩ | V_D1 |
| TP3 | Sortie F1 | R_s3 1kΩ | V_SW |
| TP4 | J2 borne 1 | R_s4 1kΩ | V_PROT |
| TP_GND | J1 borne 2 | Direct | GND |

**SECURITE : Court-circuit fils breakout → I_max = 17mA → AUCUN risque incendie**

## Connexions a faire sur la carte

### Piste ou fil entre :

| De | Vers | Comment |
|----|------|---------|
| J1 borne 1 (entree +) | D1 anode (cote sans bague) | Piste cuivre |
| J1 borne 1 (entree +) | R_s1 patte 1 | Fil court |
| R_s1 patte 2 | TP1 | Trou pour fil breakout |
| D1 cathode (cote bague) | Trou pour fil SW1-A | Piste cuivre |
| D1 cathode | R_s2 patte 1 | Fil court |
| R_s2 patte 2 | TP2 | Trou pour fil breakout |
| Trou retour SW1-B | Trou pour fil F1 entree | Piste cuivre |
| Trou retour F1 | R_s3 patte 1 | Fil court |
| R_s3 patte 2 | TP3 | Trou pour fil breakout |
| Trou retour F1 | NTC1 patte 1 | Fil rouge court |
| NTC1 patte 2 | J2 borne 1 (sortie +) | Piste cuivre |
| J2 borne 1 | R_s4 patte 1 | Fil court |
| R_s4 patte 2 | TP4 | Trou pour fil breakout |
| J1 borne 2 (entree -) | J2 borne 2 (sortie -) | Piste cuivre continue |
| J1 borne 2 | TP_GND | Trou pour fil breakout |
| TVS1 patte 1 | J2 borne 1 (sortie +) | Piste cuivre |
| TVS1 patte 2 | J2 borne 2 (sortie -) | Piste cuivre |
| C1 patte 1 | J2 borne 1 (sortie +) | Piste cuivre |
| C1 patte 2 | J2 borne 2 (sortie -) | Piste cuivre |
| C2 patte + | J2 borne 1 (sortie +) | Piste cuivre |
| C2 patte - | J2 borne 2 (sortie -) | Piste cuivre |

### Snubber

| De | Vers | Comment |
|----|------|---------|
| Trou SW1-A | R_snub patte 1 | Piste cuivre |
| R_snub patte 2 | C_snub patte 1 | Fil court |
| C_snub patte 2 | Trou SW1-B | Piste cuivre |

### Fils pour composants deportes

| Fil | Section | Longueur | De (carte) | Vers (boitier) |
|-----|---------|----------|------------|----------------|
| A | 0.75mm2 rouge | 20cm | D1 cathode (trou SW1-A) | SW1 (inter) borne 1 |
| B | 0.75mm2 rouge | 20cm | Noeud apres SW1 (trou SW1-B) | SW1 (inter) borne 2 |
| C | 0.75mm2 rouge | 20cm | Noeud apres SW1 | F1 (fusible) entree |
| D | 0.75mm2 rouge | 20cm | Vers NTC1 patte 1 | F1 (fusible) sortie |
| E | 0.5mm2 rouge | 15cm | J1 borne 1 (AVANT D1) | IND1 fil + |
| F | 0.5mm2 noir | 15cm | J1 borne 2 (entree -) | IND1 fil - |

## Tu finis par

Verifier au multimetre :

| Test | Mode | Attendu |
|------|------|---------|
| J1+ vers D1 cathode | Diode | 0.5-0.8V (sens passant) |
| D1 cathode vers J1+ | Diode | OL (bloque) |
| J1- vers J2- | Continuite | Bip |
| C2 polarite | Visuel | + vers J2+ |
| SW1-A vers SW1-B (SW1 ouvert) | Ohms | ~47Ω (snubber) |
| SW1-A vers SW1-B (SW1 ferme) | Continuite | Bip |
| **TP1 vers J1+** | **Ohms** | **~1kΩ (R_s1)** |
| **TP4 vers J2+** | **Ohms** | **~1kΩ (R_s4)** |

---

# ETAPE 6 : FABRIQUER LA BREAKOUT BOX

Voir document separe **Breakout_Box_V1.6.md**

---

# ETAPE 7 : PREPARER LES FILS

## Liste complete des fils a couper et denuder

| # | Section | Couleur | Longueur | De | Vers |
|---|---------|---------|----------|-----|------|
| 1 | 1.5mm2 | Rouge | 15cm | Batterie fil + | J1 borne 1 (entree carte +) |
| 2 | 1.5mm2 | Noir | 15cm | Batterie fil - | J1 borne 2 (entree carte -) |
| 3 | 1.5mm2 | Rouge | 15cm | J2 borne 1 (sortie carte +) | **C3+ puis** Up2Stream borne V+ |
| 4 | 1.5mm2 | Noir | 15cm | J2 borne 2 (sortie carte -) | **C3- puis** Up2Stream borne GND |
| 5 | 1.0mm2 | Rouge | 30cm | Up2Stream borne 1 (R+) | HP borne + |
| 6 | 1.0mm2 | Noir | 30cm | Up2Stream borne 3 (L+) | HP borne - |

## Condensateur bulk C3 (NOUVEAU V1.10)

**C3 = 1000µF 25V electrolytique low-ESR**

| Action | Detail |
|--------|--------|
| 1 | Souder C3 AU PLUS PRES du bornier V+ de Up2Stream |
| 2 | Patte + vers fil rouge (V+) |
| 3 | Patte - vers fil noir (GND) |
| 4 | Peut etre fixe avec colle chaude sur le boitier |

**Pourquoi C3 ?** Absorbe les appels de courant sur les basses fortes. Evite brownout et distorsion.

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
| 5 | Brancher carte vers C3 vers Up2Stream | Fil 3 sur V+, fil 4 sur GND, C3 entre les deux |
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
| **A l'extinction** | **Leger "plop" possible = NORMAL** |

---

# RECHARGE

| Etape | Action |
|-------|--------|
| 1 | **ETEINDRE** l'enceinte avec SW1 (inter) — FORTEMENT RECOMMANDE |
| 2 | IND1 reste allume et montre niveau actuel |
| 3 | Brancher chargeur **16.8V 2A UNIQUEMENT** sur prise batterie |
| 4 | IND1 montre progression charge |
| 5 | Toutes LEDs IND1 allumees = termine (2-3h) |
| 6 | Debrancher chargeur |
| 7 | Rallumer avec SW1 si besoin |

## ⚠️ AVERTISSEMENTS CHARGE

| # | Avertissement |
|---|---------------|
| 1 | **UNIQUEMENT chargeur 16.8V 2A** — Un chargeur 24V DETRUIT le circuit |
| 2 | **Eteindre avant charger** — Sinon bruit audio et coupures possibles |
| 3 | **Charge + ecoute = pas de dommage** mais qualite audio degradee |

## Connecteur XT60 (recommande)

Si tu utilises un connecteur XT60 entre batterie et carte :
- Impossible de brancher un chargeur laptop par erreur
- Standard batterie RC, robuste, detrompeur

---

# STOCKAGE

| Duree stockage | Action |
|----------------|--------|
| < 2 semaines | Rien de special |
| 2-4 semaines | Eteindre avec SW1 |
| > 1 mois | **DEBRANCHER la batterie** (IND1 vide le pack sinon) |

**Pourquoi ?** IND1 consomme ~10mA en permanence. Pack vide en 25 jours.

---

# VENTILATION

| Regle | Detail |
|-------|--------|
| **T max module** | 40°C (spec Arylic) |
| **Ne pas enfermer** | Le module chauffe (~10W a fort volume) |
| **Ouvertures** | Prevoir trous ou grille dans le boitier |
| **Test** | 1h a 80% volume, verifier T module < 50°C au toucher |

---

# BILAN PROTECTIONS V1.10

| Defaut | Protection | Temps reaction |
|--------|------------|----------------|
| Inversion polarite | D1 SB560 bloque | Instantane |
| Surtension >22V | TVS P6KE22CA clampe | <1µs |
| Court-circuit | F1 6.3A fond | 10ms-2s |
| Inrush demarrage | NTC 2.5Ω 7A limite | 50ms |
| Arc extinction SW1 | Snubber absorbe | 5µs |
| HP court-circuit | OCP interne ampli | <1ms |
| Surchauffe ampli | OTP interne ampli | Continu |
| Court-circuit breakout | R_sense 1kΩ limite a 17mA | Instantane |
| **Brownout basses** | **C3 1000µF absorbe** | **Continu** |

---

# LIMITATIONS CONNUES

| Limitation | Cause | Mitigation |
|------------|-------|------------|
| Puissance 30W (pas 60W) | Alimentation 14.8V vs 24V requis | Suffisant pour usage domestique |
| IND1 vide le pack | Branche avant SW1 | Debrancher si stockage long |
| Plop a l'extinction | Pas de mute software | Normal, pas de dommage |
| Charge + ecoute = bruit | Ground loop chargeur | Eteindre avant charger |
| Protection BMS inconnue | Depend du pack achete | Verifier pack a OCP |

---

# DEPANNAGE

| Symptome | Cause probable | Solution |
|----------|----------------|----------|
| Rien ne s'allume | Polarite inversee | Verifier + et - batterie |
| Rien ne s'allume | Fusible F1 grille | Remplacer fusible |
| IND1 allume mais pas ampli | SW1 OFF ou D1 HS | Verifier SW1, tester D1 |
| S'allume puis s'eteint | Batterie vide (<12V) | Recharger |
| S'eteint au rallumage rapide | BMS coupe (NTC chaude) | Attendre 1min, ressayer |
| Son distordu fort volume | HP impedance trop basse | Verifier DCR ≥ 5.5Ω |
| Distorsion sur basses | C3 absent ou HS | Verifier C3 1000µF |
| Sifflement aigu | EMI antenne BT | Eloigner fils alim des antennes |
| Bruit pendant charge | Charge avec SW1 ON | Eteindre avant charger |
| Module chaud | Ventilation insuffisante | Aerer le boitier |
| Plop a l'extinction | Normal | Pas de solution simple, accepter |
| Pack vide apres stockage | IND1 a vide le pack | Debrancher si > 2 semaines |

---

# CHANGELOG COMPLET

| Version | Date | Modifications |
|---------|------|---------------|
| V1.10 | 14 Dec 2025 | Audit V2 : D1→SB560, NTC→7A, C3 bulk, puissance corrigee, warnings |
| V1.9 | 14 Dec 2025 | C_snub 100V film, R_sense 10kΩ anti-incendie breakout |
| V1.8 | 14 Dec 2025 | Audit certifie : PTC retiree, snubber SW1, IND1 avant SW1, NTC 10mm |
| V1.7 | 14 Dec 2025 | Audit : D1 anti-inversion, TVS 22CA, decouplage, ferrite |
| V1.6 | 14 Dec 2025 | Refs explicites, ordre clair |

---

**FIN CIRCUIT V1.10**
