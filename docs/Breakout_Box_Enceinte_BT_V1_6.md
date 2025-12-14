# BREAKOUT BOX ENCEINTE BT V1.6

**Version:** 1.6  
**Date:** 14 Decembre 2025  
**Compatibilite:** Circuit V1.10+

---

# ⚠️ AVERTISSEMENT SECURITE

| Version | Risque court-circuit | Statut |
|---------|---------------------|--------|
| V1.4 et avant | 200A → INCENDIE | ❌ DANGEREUSE |
| **V1.5+** | **17mA max** | **✅ SECURISEE** |

**Cette breakout V1.6 necessite le Circuit V1.10+ avec resistances R_sense 1kΩ integrees.**

---

# PRINCIPE

## Pourquoi une breakout box ?

| Probleme | Solution |
|----------|----------|
| Mesurer tensions = fils qui trainent | Boitier avec borniers propres |
| Fils sur points puissance = risque CC | Resistances 1kΩ limitent a 17mA |
| Branchements temporaires = accidents | Connexion permanente securisee |

## Schema de protection

```
CARTE PRINCIPALE                          BREAKOUT BOX
─────────────────                         ────────────

J1+ (BATT+) ─── R_s1 (1kΩ) ─── TP1 ═══════ Fil 0.25mm² ═══════ Bornier 1 (V_BATT)
                                                                      │
D1 cathode ──── R_s2 (1kΩ) ─── TP2 ═══════ Fil 0.25mm² ═══════ Bornier 2 (V_D1)
                                                                      │
Sortie F1 ───── R_s3 (1kΩ) ─── TP3 ═══════ Fil 0.25mm² ═══════ Bornier 3 (V_SW)
                                                                      │
J2+ (V_PROT) ── R_s4 (1kΩ) ─── TP4 ═══════ Fil 0.25mm² ═══════ Bornier 4 (V_PROT)
                                                                      │
J1- (GND) ───────────────────── TP_GND ═══ Fil 0.25mm² ═══════ Bornier 5 (GND)
                                                                      │
                                           (Bornier 6 libre)          │
                                                                      │
                                                            MULTIMETRE 10MΩ
```

## Calcul securite (preuve)

| Parametre | Valeur | Calcul |
|-----------|--------|--------|
| V_max (batterie chargee) | 16.8V | - |
| R_sense | 1kΩ | - |
| **I_court-circuit max** | **16.8mA** | 16.8V / 1kΩ |
| Capacite fil 0.25mm² | 3A | - |
| **Marge securite** | **178×** | 3A / 0.017A |
| P_resistor si CC | 0.28W | (16.8mA)² × 1kΩ |
| Rating R_sense | 0.5W | - |
| **Marge thermique** | **44%** | 0.28W / 0.5W |

**Conclusion : Court-circuit fils breakout = AUCUN risque incendie.**

---

# COMPARAISON V1.5 vs V1.6

| Parametre | V1.5 (10kΩ) | V1.6 (1kΩ) | Verdict |
|-----------|-------------|------------|---------|
| I_cc max | 1.7mA | 17mA | Les deux OK |
| Erreur multi 10MΩ | 0.1% | 0.01% | V1.6 mieux |
| Erreur multi 1MΩ | 1% | 0.1% | **V1.6 bien mieux** |
| Standard industrie | Non | **Oui** | V1.6 |
| Rating resistor | 0.25W OK | **0.5W requis** | V1.6 plus robuste |

**V1.6 avec 1kΩ est le standard industrie pour les sense lines.**

---

# MATERIEL NECESSAIRE

| Composant | Quantite | Recherche | Prix |
|-----------|----------|-----------|------|
| Bornier 6 positions 5mm | 1 | "bornier a vis 6 positions 5mm" | 2 EUR |
| Boitier ABS 60×40×20mm | 1 | "boitier plastique electronique petit" | 3 EUR |
| Fil 0.25mm² rouge | 50cm | "fil souple 0.25mm rouge" | 0.50 EUR |
| Fil 0.25mm² noir | 50cm | "fil souple 0.25mm noir" | 0.50 EUR |
| Fil 0.25mm² autres couleurs | 1.5m | "fil souple 0.25mm couleurs" | 1 EUR |
| Etiqueteuse ou marqueur | 1 | - | - |

**TOTAL : ~7 EUR**

---

# FABRICATION

## Etape 1 : Preparer les fils

| Fil | Couleur | Longueur | De (carte) | Vers (breakout) |
|-----|---------|----------|------------|-----------------|
| 1 | Rouge | 40cm | TP1 | Bornier 1 |
| 2 | Orange | 40cm | TP2 | Bornier 2 |
| 3 | Jaune | 40cm | TP3 | Bornier 3 |
| 4 | Vert | 40cm | TP4 | Bornier 4 |
| 5 | Noir | 40cm | TP_GND | Bornier 5 |

## Etape 2 : Percer le boitier

| Action | Detail |
|--------|--------|
| 1 | Marquer 5 trous alignes sur un cote (passage fils) |
| 2 | Percer a 3mm |
| 3 | Optionnel : passe-fil ou gaine thermoretractable |

## Etape 3 : Monter le bornier

| Action | Detail |
|--------|--------|
| 1 | Placer le bornier 6 positions dans le boitier |
| 2 | Coller a la colle chaude ou visser |
| 3 | Verifier acces aux vis par le dessus |

## Etape 4 : Cabler

| Action | Detail |
|--------|--------|
| 1 | Passer les 5 fils dans les trous |
| 2 | Denuder 5mm a chaque extremite |
| 3 | Visser chaque fil dans son bornier |
| 4 | Tirer doucement pour verifier serrage |

## Etape 5 : Etiqueter

| Bornier | Etiquette | Couleur fil |
|---------|-----------|-------------|
| 1 | V_BATT | Rouge |
| 2 | V_D1 | Orange |
| 3 | V_SW | Jaune |
| 4 | V_PROT | Vert |
| 5 | GND | Noir |
| 6 | (libre) | - |

## Etape 6 : Souder cote carte

| Action | Detail |
|--------|--------|
| 1 | Reperer TP1 a TP4 et TP_GND sur la carte V1.10 |
| 2 | Souder chaque fil sur son point TP |
| 3 | Verifier pas de court-circuit entre points |

---

# UTILISATION

## Branchement multimetre

| Mesure | Borne + multi | Borne - multi (COM) |
|--------|---------------|---------------------|
| V_BATT (tension batterie) | Bornier 1 | Bornier 5 (GND) |
| V_D1 (apres diode) | Bornier 2 | Bornier 5 (GND) |
| V_SW (apres inter+fusible) | Bornier 3 | Bornier 5 (GND) |
| V_PROT (sortie carte) | Bornier 4 | Bornier 5 (GND) |

## Valeurs attendues

| Point | SW1 OFF | SW1 ON | Anomalie si |
|-------|---------|--------|-------------|
| V_BATT | 12-16.8V | 12-16.8V | <12V (batterie vide) |
| V_D1 | V_BATT - 0.5V | V_BATT - 0.7V | >1V de chute (D1 HS) |
| V_SW | 0V | V_D1 | 0V avec SW1 ON (fusible grille) |
| V_PROT | 0V | V_SW - 0.2V | >0.5V chute (NTC HS) |

## Precision des mesures

| Impedance multimetre | Erreur due a R_sense 1kΩ |
|---------------------|--------------------------|
| 10MΩ (standard) | 0.01% (negligeable) |
| 1MΩ (entree gamme) | 0.1% (negligeable) |
| 100kΩ (tres bas) | 1% (acceptable) |

**Avec R_sense 1kΩ, compatible avec quasiment tous les multimetres.**

---

# ETIQUETTE BOITIER

Coller sur le boitier :

```
╔════════════════════════════════════════╗
║     BREAKOUT BOX ENCEINTE BT V1.6     ║
╠════════════════════════════════════════╣
║  ⚠️ MESURE TENSION UNIQUEMENT         ║
║  ⚠️ NE PAS BRANCHER CHARGE            ║
║  ⚠️ MULTIMETRE MODE VOLTS DC          ║
╠════════════════════════════════════════╣
║  1: V_BATT (rouge)   4: V_PROT (vert) ║
║  2: V_D1 (orange)    5: GND (noir)    ║
║  3: V_SW (jaune)     6: (libre)       ║
╚════════════════════════════════════════╝
```

---

# SECURITE

## Ce qui est INTERDIT

| Interdit | Pourquoi |
|----------|----------|
| ❌ Mode amperemetre | Shunt interne ≈ 0Ω → mesure fausse |
| ❌ Brancher une charge | Pas prevu pour delivrer du courant |
| ❌ Court-circuiter les borniers | Inutile (protege, mais pas le but) |
| ❌ Utiliser avec Circuit < V1.10 | Pas de R_sense = risque incendie |

## Ce qui est AUTORISE

| Autorise | Detail |
|----------|--------|
| ✅ Mesure tension DC | Mode V= du multimetre |
| ✅ Oscilloscope | Sonde 10:1 recommandee |
| ✅ Enregistreur de donnees | Si impedance > 100kΩ |
| ✅ Laisser branchee en permanence | Aucune consommation |

---

# DEPANNAGE

| Symptome | Cause | Solution |
|----------|-------|----------|
| Toutes tensions = 0V | Batterie debranchee | Verifier J1 |
| V_BATT OK, autres = 0V | D1 en court-circuit inverse | Verifier polarite D1 |
| V_D1 OK, V_SW = 0V | Fusible grille ou SW1 OFF | Verifier F1 et SW1 |
| V_SW OK, V_PROT = 0V | NTC ouverte | Verifier NTC |
| Valeurs instables | Mauvais contact bornier | Resserrer vis |
| Erreur > 5% | Multi en mode AC | Passer en mode DC |

---

# CHANGELOG

| Version | Date | Modifications |
|---------|------|---------------|
| V1.6 | 14 Dec 2025 | R_sense 1kΩ 0.5W (standard industrie) |
| V1.5 | 14 Dec 2025 | R_sense 10kΩ anti-incendie |
| V1.4 | 14 Dec 2025 | Fils directs (DANGEREUSE) |

---

**FIN BREAKOUT BOX V1.6**
