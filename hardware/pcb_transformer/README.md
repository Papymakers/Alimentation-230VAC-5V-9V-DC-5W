# PCB Transformateur 9VAC — Carte B

## Fichiers

| Fichier | Description |
|---|---|
| `acdc_transformer_gerber.zip` | Gerbers JLCPCB (à ajouter depuis EasyEDA) |
| `acdc_transformer_schematic.json` | Source EasyEDA schéma |
| `acdc_transformer_pcb.json` | Source EasyEDA PCB |
| `acdc_transformer_bom.csv` | Bill of Materials |

## Paramètres JLCPCB

| Paramètre | Valeur |
|---|---|
| Dimensions | 85.34 × 48.28 mm |
| Couches | 2 |
| Épaisseur | 1.6 mm FR4 |
| Couleur masque | Rouge (sérigraphie visible sur photo) |
| Sérigraphie | Blanche |
| Finition | HASL sans plomb |
| Quantité min. | 5 pièces |

## Spécificités PCB

- **Zone cuivre nu** sous le LM7805 (pas de vernis épargne) — dissipation thermique
- **Trou M3** pour visser le TO220 sur le PCB
- **Sérigraphie** : `AC/DC 5V 1A` + `D-Sys 02/25`

## BOM (Bill of Materials)

| Réf. | Désignation | Valeur | Empreinte | Qté |
|---|---|---|---|---|
| U1 | Régulateur TO220 | LM7805 | TO-220 | 1 |
| BR1 | Pont de diodes | 1A / 50V | DIL ou discret | 1 |
| C1 | Électrochimique | 1000µF / 25V | Ø10mm, pas 5mm | 1 |
| F1 | Fusible temporisé | 2A T | 5×20mm | 1 |
| J1 | Bornier sortie DC | 2 pos. | Pas 5.08mm | 1 |
| J2 | Bornier entrée AC | 2 pos. | Pas 5.08mm | 1 |

## Transformateur externe compatible

| Paramètre | Valeur |
|---|---|
| Tension secondaire | 9 VAC |
| Courant secondaire | ≥ 1.5 A (prévoir marge) |
| Type | Toroïdal ou EI — selon encombrement |

> Le transformateur est externe au PCB — prévoir le câblage
> entre le secondaire du transformateur et le bornier J2.
