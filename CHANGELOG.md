# Changelog — hilink-acdc-psu

Format : [Keep a Changelog](https://keepachangelog.com/fr/1.0.0/)

---

## [1.0.0] — 2026-06-14

### Ajouté
- PCB universel 85 × 48 mm compatible HLK-5M05 et HLK-9M05
- Protection EMI primaire : Common Mode Choke 250VAC / 1.1A / 10mH
- Protection surtension : Varistance MOV 275VAC
- Condensateur de sécurité Y : 0.1µF / 275VAC / 20% MPP
- Fusible 2A temporisé en série sur la Phase
- Emplacement régulateur TO220 optionnel (U2) avec diode 1N4001
  et condensateur 100nF — pontable si non utilisé
- Bornier entrée 230V (droite) et bornier sortie DC (gauche)
- Trois configurations documentées : 5V direct, 9V direct, 5V post-régulé
- Documentation sécurité 230V

### Compatibilité validée
- HLK-5M05 → ESP32-2432S028R (CYD), ESP32-C6
- HLK-9M05 → Préamplificateur audio, périphériques 9V

---

## [À venir — v2.0]

- Double sortie simultanée 9V + 5V
  (HLK-9M05 + LM7805 + deux borniers de sortie indépendants)
- LED témoin présence tension DC (optionnelle, sans résistance de puissance)
- Empreinte fusible ajoutée côté Neutre (option)

---

## [1.1.0] — 2026-06-14

### Ajouté
- **Carte B** — alimentation linéaire 9VAC → LM7805 → 5VDC / 1A
  - Pont de diodes double alternance
  - Condensateur de filtrage 1000µF / 25V
  - Zone cuivre nu exposé sous LM7805 pour dissipation thermique intégrée
  - Trou de fixation M3 pour TO220
  - Dimensions : 85.34 × 48.28 mm (compatibles boîtier Carte A)
  - Fusible 2A temporisé côté AC
- Restructuration `hardware/pcb/` → `hardware/pcb_hilink/` et `hardware/pcb_transformer/`
- README principal unifié présentant les deux cartes avec tableau comparatif
- Photo PCB Carte B ajoutée dans `docs/images/`
