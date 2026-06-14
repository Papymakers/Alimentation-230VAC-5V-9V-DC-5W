# Assemblage & Sécurité — Hi-Link AC/DC PSU

## ⚠️ Avertissement sécurité

Ce PCB comporte des tensions de **230 V CA** potentiellement mortelles.

- Assemblage et mise en service réservés aux personnes habilitées
- Norme applicable en France : **NF C 18-510**
- Toujours couper le secteur avant intervention
- Attendre ≥ 10 secondes après coupure (décharge condensateurs)
- Vérifier l'absence de tension avec un multimètre avant de toucher

---

## Ordre d'assemblage recommandé

Toujours commencer par les composants les plus bas, souder côté BT
avant les composants 230V.

### Étape 1 — Secondaire DC (côté BT)

1. **C1** — condensateur céramique 100nF (petite pastille, polarité indifférente)
2. **D1** — diode 1N4001 (repérer la bague = cathode = côté OUT de U2)
   *Omettre si config A ou B sans régulateur*
3. **U2** — régulateur TO220 (GND = broche centrale)
   *Omettre et ponter IN→OUT si config A ou B*

### Étape 2 — Module Hi-Link U1

4. **U1** — module Hi-Link HLK-5M05 ou HLK-9M05
   (respecter l'orientation — repère sérigraphié)

### Étape 3 — Composants primaire 230V

> À partir d'ici, les composants sont au potentiel secteur.
> Travailler avec soin, vérifier deux fois chaque soudure.

5. **Cy** — condensateur de sécurité 0.1µF/275VAC (polarité indifférente)
6. **RV1** — varistance MOV 275V (polarité indifférente)
7. **FL2** — Common Mode Choke 10mH/1.1A (respecter le sens du bobinage)
8. **F1** — fusible 2A T dans son porte-fusible, ou directement soudé

### Étape 4 — Borniers

9. **J2** (droite) — bornier 230V entrée : L (Phase) à gauche, N (Neutre) à droite
10. **J1** (gauche) — bornier DC sortie : +V en haut, GND en bas

---

## Vérifications avant mise sous tension

| Contrôle | Outil | Résultat attendu |
|---|---|---|
| Court-circuit +V → GND | Multimètre Ω | > 10 kΩ |
| Court-circuit L → N | Multimètre Ω | Résistance FL2 (~2 Ω) |
| Court-circuit L → GND secondaire | Multimètre Ω | > 1 MΩ (isolation HLK) |
| Continuité fusible F1 | Multimètre Ω | < 1 Ω |
| Tension sortie à vide | Multimètre V DC | 5.0 ± 0.2 V ou 9.0 ± 0.5 V |

---

## Mise en service

1. Brancher une charge légère de test (résistance 100Ω/2W en config 5V)
2. Alimenter via une prise avec disjoncteur différentiel 30mA
3. Mesurer la tension de sortie sous charge
4. Vérifier l'échauffement après 10 minutes (U1 et U2 si présent)

### Températures normales en fonctionnement

| Composant | Température typique | Limite |
|---|---|---|
| HLK U1 | 40–60 °C | 85 °C max |
| LM7805 U2 (config C, 300mA) | 50–70 °C | 125 °C jonction |
| FL2 CMC | 30–45 °C | 85 °C |

---

## Intégration dans un boîtier

### Distances minimales à respecter

- Carte → paroi conductrice (boîtier métal) : **≥ 10 mm** sur le côté primaire
- Carte → paroi plastique : **≥ 5 mm**
- Les borniers 230V doivent être inaccessibles sans outil

### Fixation

- 4 trous de fixation M3 aux coins (voir PCB)
- Utiliser des vis plastique ou des entretoises isolantes côté primaire
- Côté secondaire : entretoises métal acceptables

### Câblage 230V

- Section minimale câble Phase/Neutre : **0.75 mm²** (fusible 2A)
- Utiliser du câble souple H05VV-F ou équivalent
- Longueur maximale entre bornier et prise secteur : selon installation

---

## Dépannage

| Symptôme | Cause probable | Solution |
|---|---|---|
| Pas de tension sortie | Fusible F1 claqué | Remplacer F1, chercher court-circuit |
| Tension sortie basse | Surcharge | Réduire la charge, vérifier < Imax HLK |
| Oscillations sur sortie | C1 absent ou défectueux | Vérifier/remplacer C1 |
| Chaleur excessive U2 | Courant trop élevé en config C | Ajouter radiateur TO220 ou réduire charge |
| Disjoncteur différentiel déclenche | Fuite via Cy vers GND | Normal si Cy branché — vérifier ≤ 3.5mA |
