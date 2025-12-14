# 🔊 ENCEINTE BLUETOOTH VINTAGE V2.0

**Version:** 2.0 RELEASE
**Date:** Decembre 2024
**Statut:** PLUG & PLAY - Zero contrainte utilisateur

---

## 🎯 CONCEPT

Transformer une enceinte vintage (annees 60-80) en systeme audio Bluetooth/WiFi moderne avec batterie integree.

**Philosophie V2.0:** L'utilisateur final n'a RIEN a faire sauf allumer et eteindre.

---

## ✨ CARACTERISTIQUES V2.0

| Fonctionnalite | Specification |
|----------------|---------------|
| Connectivite | Bluetooth 5.0 + WiFi (AirPlay, Spotify Connect) |
| Puissance | 25W @ 4ohm / 35W @ 8ohm |
| Autonomie | 8-12h selon volume |
| Charge | USB-C ou adaptateur 16.8V |
| **Charge + ecoute** | ✅ OUI (sans bruit) |
| **Stockage** | ✅ Illimite (zero drain) |
| **Redemarrage rapide** | ✅ Immediat |
| **Pop ON/OFF** | ✅ Aucun |

---

## 📦 CONTENU DU PROJET

```
/
├── Circuit_Enceinte_BT_Vintage_V2_0.md    ← Schema principal
├── Breakout_Box_Enceinte_BT_V2_0.md       ← Outil diagnostic
├── README.md                               ← Ce fichier
└── docs/
    └── README.md                           ← Documentation technique
```

---

## 🔧 SPECIFICATIONS TECHNIQUES

### Alimentation

| Parametre | Valeur |
|-----------|--------|
| Batterie | 4S LiFePO4 ou Li-ion (12.8-16.8V) |
| Capacite | 6000mAh recommande |
| Chargeur | 16.8V 2A (Li-ion) ou 14.6V (LiFePO4) |
| Protection | Fusible 6.3A + TVS 18V + NTC 10A |

### Audio

| Parametre | Valeur |
|-----------|--------|
| Module | Up2Stream Amp V4 (Arylic) |
| Amplificateur | TPA3116D2 Class-D |
| Impedance HP | 4 ohm (STEREO) ou 8 ohm+ (MONO) |
| Reponse | 20Hz - 20kHz |

### Protections integrees

| Protection | Composant | Fonction |
|------------|-----------|----------|
| Anti-inversion | D1 SB560 | Polarite batterie |
| Surtension | TVS 1.5KE18CA | Pics >18V |
| Surintensité | F1 6.3A | Court-circuit |
| Inrush | NTC 2.5ohm 10A | Appel courant |
| Soft-start | Q_SS IRF9540 | Redemarrage rapide |
| Anti-pop | K_HP + LM393 | Zero pop ON/OFF |
| Filtre charge | L1 + C_filt | Bruit chargeur |

---

## 🎮 UTILISATION (UTILISATEUR FINAL)

```
ALLUMER:  Appuyer sur l'interrupteur → musique en 2 secondes
ETEINDRE: Appuyer sur l'interrupteur → arret propre sans pop
CHARGER:  Brancher le chargeur (peut ecouter en meme temps)
STOCKER:  Eteindre et oublier (pas besoin de debrancher)

C'est TOUT. Pas d'autres instructions.
```

---

## 🔨 CONSTRUCTION (POUR LE FABRICANT)

### Prerequis

- Fer a souder + etain
- Multimetre
- Oscilloscope (recommande pour tests)
- Perceuse (grilles ventilation)

### Etapes

1. **Commander les composants** (voir BOM dans Circuit_V2.0.md)
2. **Assembler le circuit** sur veroboard
3. **Configurer les jumpers HP** selon impedance
4. **Installer la thermique** (pad + plaque alu + grilles)
5. **Tester avec breakout box**
6. **Integrer dans l'enceinte**

### Configuration HP (importante)

```
┌─────────────────────────────────────────────────┐
│ Mesurer DCR du haut-parleur avec multimetre     │
├─────────────────────────────────────────────────┤
│ DCR < 4 ohm  → Mode STEREO                      │
│               Jumpers: HAUT + MILIEU            │
│               Cablage: HP sur L+ et L-          │
│               Puissance: ~25W                   │
├─────────────────────────────────────────────────┤
│ DCR >= 5.5 ohm → Mode MONO PBTL                 │
│                  Jumpers: MILIEU + BAS          │
│                  Cablage: HP+ sur R+, HP- sur L+│
│                  Puissance: ~35W                │
└─────────────────────────────────────────────────┘
```

---

## 💰 BUDGET

| Poste | Prix |
|-------|------|
| Module Up2Stream Amp V4 | 65 EUR |
| Pack batterie 4S 6Ah | 60 EUR |
| Chargeur 16.8V 2A | 15 EUR |
| Haut-parleur | 25 EUR |
| Composants electroniques | 30 EUR |
| Divers (cables, boitier, etc.) | 9 EUR |
| **TOTAL** | **~204 EUR** |

---

## 📊 SCHEMA BLOC SIMPLIFIE

```
                    FILTRE LC
CHARGEUR ──── L1 ────┬──── C_filt ──── GND
                     │
BATTERIE ────────────┴──── D1 ──── Q_SS ──── SW1 ──── F1 ──── NTC ──── V_PROT
                                   (soft)                              │
                                                                  ┌────┴────┐
                                                                  │         │
                                                               MODULE    K_HP
                                                               ARYLIC   (anti-pop)
                                                                  │         │
                                                                  └────┬────┘
                                                                       │
                                                                      HP
```

---

## 📜 HISTORIQUE VERSIONS

| Version | Date | Changements majeurs |
|---------|------|---------------------|
| V1.0 | Oct 2024 | Conception initiale |
| V1.5 | Nov 2024 | Ajout protections TVS, NTC |
| V1.9 | Dec 2024 | Securite incendie breakout |
| V1.10 | Dec 2024 | Corrections audit V2 |
| **V2.0** | Dec 2024 | **Refonte complete - Plug & Play** |

### Nouveautes V2.0

- ✅ Soft-start P-MOSFET (redemarrage immediat)
- ✅ Relais anti-pop (zero pop ON/OFF)
- ✅ Filtre LC charge (ecoute pendant charge)
- ✅ IND1 apres SW1 (stockage illimite)
- ✅ NTC 10A (marge inrush)
- ✅ Dissipateur integre (pas de surchauffe)

---

## ⚠️ AVERTISSEMENTS (FABRICANT)

1. **Chargeur:** Utiliser UNIQUEMENT chargeur compatible (16.8V Li-ion ou 14.6V LiFePO4)
2. **HP:** Configurer jumpers AVANT mise sous tension
3. **Thermique:** Installer dissipateur + grilles OBLIGATOIRE
4. **Breakout:** V2.0 uniquement compatible avec Circuit V2.0+

---

## 📄 LICENCE

Projet open-source pour usage personnel.
Documentation et schemas libres de droits.

---

## 🔗 FICHIERS

- [Circuit V2.0](./Circuit_Enceinte_BT_Vintage_V2_0.md)
- [Breakout V2.0](./Breakout_Box_Enceinte_BT_V2_0.md)
- [Documentation technique](./docs/README.md)
