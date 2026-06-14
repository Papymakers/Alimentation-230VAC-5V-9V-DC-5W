# Hi-Link AC/DC PSU — 5V & 9V / 5W

**Carte d'alimentation universelle 230 VAC → 5 V ou 9 V DC**  
Projet open-source — [Papy Makers](https://github.com/papymakers)

---

## Présentation

PCB universel 85 × 48 mm conçu pour les modules **Hi-Link HLK-5M05** (5 V / 1 A)
et **HLK-9M05** (9 V / 0.6 A), avec protections EMI et surtensions conformes aux
recommandations Hi-Link.

Un emplacement optionnel **régulateur TO220** (U2) permet de post-réguler la tension
de sortie — par exemple LM7805 après un HLK-9M05 pour obtenir un 5 V très propre.

![PCB vue de dessus](docs/images/pcb_top_view.png)

---

## Configurations disponibles

| Config | Module HLK | U2 | Sortie | Usage typique |
|---|---|---|---|---|
| **A** | HLK-5M05 | Pont + C100nF | 5 V / 1 A | CYD, ESP32 |
| **B** | HLK-9M05 | Pont + C100nF | 9 V / 0.6 A | Préamplificateur, périphérique 9 V |
| **C** | HLK-9M05 | LM7805 + 1N4001 + C100nF | 5 V / ~0.5 A | 5 V très régulé depuis 9 V |

> **Config C** : le LM7805 dissipe environ (9−5) × 0.5 = 2 W — prévoir
> une petite surface de dissipation ou un radiateur TO220 si charge > 300 mA.

---

## Schéma fonctionnel

```
                         Primaire 230 V AC
                         ─────────────────
L (Phase) ──[F1 2A]──[FL2 CMC 10mH/1.1A]──┬──► AC-L (HLK U1)
                                            │
N (Neutre) ─────────────────────────────────┼──► AC-N (HLK U1)
                                            │
                           [RV1 275 V]      │
                           [Cy 0.1µF/275V]  │
                                │           │
                               GND         GND

                         Secondaire DC
                         ─────────────
HLK +V ──[1N4001]──[IN  U2 TO220  OUT]──► Bornier +5V ou +9V
                   [GND = broche 2    ]
                   [C 100nF vers GND  ]
                                        ──► Bornier GND

         Sans régulateur : pont IN─OUT sur U2, garder C100nF
```

---

## Composants

### Primaire (commun aux deux variantes)

| Réf. | Composant | Valeur | Remarque |
|---|---|---|---|
| F1 | Fusible | 2 A T (temporisé) | 5 × 20 mm — en série sur la Phase |
| FL2 | Common Mode Choke | 250 VAC / 1.1 A / 10 mH | Filtre EMI différentiel et commun |
| RV1 | Varistance (MOV) | 275 VAC / 7 mm | Protection surtension réseau |
| Cy | Condensateur de sécurité | 0.1 µF / 275 VAC / 20% MPP | Condensateur Y — entre N et GND |
| U1 | Module Hi-Link | HLK-5M05 **ou** HLK-9M05 | Convertisseur AC/DC isolé |

### Secondaire — Config A et B (sans régulateur)

| Réf. | Composant | Valeur | Remarque |
|---|---|---|---|
| — | Pont | Fil ou 0 Ω | Court-circuit IN→OUT de U2 |
| C1 | Condensateur céramique | 100 nF | Découplage sortie |

### Secondaire — Config C (avec régulateur)

| Réf. | Composant | Valeur | Remarque |
|---|---|---|---|
| D1 | Diode | 1N4001 | Protection inverse entre HLK et U2 |
| U2 | Régulateur TO220 | LM7805 | Broche GND au centre |
| C1 | Condensateur céramique | 100 nF | Découplage sortie U2 |

---

## Caractéristiques électriques

| Paramètre | Config A | Config B | Config C |
|---|---|---|---|
| Tension entrée | 85–265 VAC | 85–265 VAC | 85–265 VAC |
| Fréquence | 47–63 Hz | 47–63 Hz | 47–63 Hz |
| Tension sortie | 5 V DC | 9 V DC | 5 V DC |
| Courant max. sortie | 1 A | 0.6 A | ~0.5 A |
| Puissance sortie | 5 W | 5.4 W | ~2.5 W utile |
| Rendement typique | ~80 % | ~80 % | ~65 % |
| Isolation HT/BT | 3 kV | 3 kV | 3 kV |
| Ondulation sortie | < 100 mVpp | < 100 mVpp | < 10 mVpp |

---

## PCB

### Dimensions

| Paramètre | Valeur |
|---|---|
| Dimensions | 85 × 48 mm |
| Épaisseur | 1.6 mm FR4 |
| Couches | 2 |

### Borniers

| Bornier | Signal | Pas | Remarque |
|---|---|---|---|
| J1 (gauche) | +5V / +9V / GND | 5.08 mm | Sortie DC vers charge |
| J2 (droite) | L / N | 5.08 mm | Entrée 230 VAC |

### Distances de sécurité

| Paramètre | Valeur |
|---|---|
| Piste HT ↔ piste BT | ≥ 6 mm |
| Piste HT ↔ bord PCB | ≥ 4 mm |
| Largeur piste primaire | ≥ 1 mm (fusible 2 A) |

### Paramètres JLCPCB

| Paramètre | Valeur |
|---|---|
| Couleur masque | Bleu (standard) ou Noir |
| Sérigraphie | Blanche |
| Finition surface | HASL sans plomb |
| Quantité minimale | 5 pièces |

Fichiers Gerbers : [`hardware/pcb/`](hardware/pcb/)

---

## Compatibilité modules Hi-Link

| Module | Tension | Courant | Puissance | Compatible PCB |
|---|---|---|---|---|
| HLK-5M05 | 5 V | 1 A | 5 W | ✅ |
| HLK-9M05 | 9 V | 0.6 A | 5.4 W | ✅ |
| HLK-PM01 | 5 V | 0.6 A | 3 W | ✅ (empreinte identique) |
| HLK-PM09 | 9 V | 0.4 A | 3.6 W | ✅ (empreinte identique) |

---

## Applications testées

| Application | Config | Consommation typique |
|---|---|---|
| ESP32-2432S028R (CYD) | A | 200–350 mA |
| ESP32-C6 seul | A | 100–200 mA |
| ESP32-C6 + périphériques I2C | A | 200–300 mA |
| Préamplificateur audio | B | 50–150 mA |

---

## Sécurité

> ⚠️ **Ce PCB comporte des tensions de 230 V CA dangereuses.**  
> La conception, l'assemblage et la mise en service doivent être réalisés
> par des personnes formées et habilitées aux travaux sous tension
> (norme NF C 18-510 en France).
>
> **Avant toute intervention sur le circuit :**
> - Couper l'alimentation secteur
> - Attendre la décharge des condensateurs (≥ 10 s)
> - Vérifier l'absence de tension avec un multimètre

### Évolutions prévues (v2)

- Double sortie simultanée **9 V + 5 V** depuis un seul HLK-9M05
  (LM7805 en post-régulateur, deux borniers de sortie indépendants)
- LED témoin optionnelle sur sortie DC

---

## Projets utilisant cette carte

| Projet | Config utilisée |
|---|---|
| [esp32-cyd-home-monitor](https://github.com/papymakers/esp32-cyd-home-monitor) | A — 5 V / 1 A |
| [esp32-cyd-heating-remote](https://github.com/papymakers/esp32-cyd-heating-remote) | A — 5 V / 1 A |

---

## Licence

MIT — voir [`LICENSE`](LICENSE)

## Auteur

**Papy Makers** — Normandie, France  
[github.com/papymakers](https://github.com/papymakers)
