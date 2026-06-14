# PCB — Hi-Link AC/DC PSU

## Fichiers

| Fichier | Description |
|---|---|
| `hilink_acdc_psu_gerber.zip` | Gerbers JLCPCB (à ajouter depuis EasyEDA) |
| `hilink_acdc_psu_schematic.json` | Source EasyEDA schéma |
| `hilink_acdc_psu_pcb.json` | Source EasyEDA PCB |
| `hilink_acdc_psu_bom.csv` | Bill of Materials |

## Paramètres JLCPCB

| Paramètre | Valeur |
|---|---|
| Dimensions | 85 × 48 mm |
| Couches | 2 |
| Épaisseur | 1.6 mm FR4 |
| Couleur masque | Bleu ou Noir |
| Sérigraphie | Blanche |
| Finition | HASL sans plomb |
| Quantité min. | 5 pièces |

## Export Gerbers depuis EasyEDA

1. `Fabrication → Gerber → JLCPCB`
2. Vérifier avec [Gerber Viewer JLCPCB](https://gerber-viewer.jlcpcb.com)
3. Déposer le ZIP dans ce dossier

## BOM (Bill of Materials)

| Réf. | Désignation | Valeur | Empreinte | Qté |
|---|---|---|---|---|
| U1 | Module Hi-Link | HLK-5M05 ou HLK-9M05 | HLK-xM0x | 1 |
| U2 | Régulateur (optionnel) | LM7805 TO220 | TO-220 | 0–1 |
| F1 | Fusible temporisé | 2A T | 5×20mm | 1 |
| FL2 | Common Mode Choke | 10mH / 1.1A / 250VAC | TH pas 5mm | 1 |
| RV1 | Varistance MOV | 275VAC / 7mm | Ø7mm pas 5mm | 1 |
| Cy | Condensateur sécu. Y | 0.1µF / 275VAC MPP | Pas 10mm | 1 |
| D1 | Diode (optionnelle) | 1N4001 | DO-41 | 0–1 |
| C1 | Condensateur céramique | 100nF | Pas 2.54mm | 1 |
| J1 | Bornier DC sortie | 2 pos. | Pas 5.08mm | 1 |
| J2 | Bornier AC entrée | 2 pos. | Pas 5.08mm | 1 |
