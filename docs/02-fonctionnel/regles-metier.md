# Règles Métier

Décrivez ici les règles métier du projet.
## Calcul des scores

C'est la partie la plus sensible. Les paramètres sont le poids, les références, fonctions
  (`clamp01`, `saturatingScore`, `intensityRate`, `pressureScoreFromNorms`).

### Principes :

1. **Une seule source de données** : `footCumulStore.ts` lit d'abord le store Electron,
   sinon `localStorage`. La liste patients et l'onglet analyse utilisent la **même**
   source → plus d'écart entre les écrans.
2. **Sous-scores renormalisés** : si l'adhérence ou le profil sont absents, on ne les
   compte pas (au lieu de les mettre à 0). On combine seulement les sous-scores disponibles.
3. **Données insuffisantes = N/A** : si un patient n'a ni pression, ni temps de port, ni
   profil, le statut est `INSUFFICIENT` et l'UI affiche **N/A** .
4. **Saturation maîtrisée** : `saturatingScore` permet d'atteindre réellement ~100 %
   quand l'intensité et la fréquence sont élevées.

Pour modifier un poids ou une référence, **éditez `riskConfig.ts`** (pas les composants).

## Suivi clinique — pression (kPa) & température (°C)

### Objectif


Ce module ajoute une couche **clinique** au-dessus du flux FSR existant :

- **Pression** : conversion FSR (unités brutes après baseline) → **kPa** via calibration.
- **Température** : canaux **°C** par zone (ou global), baseline patient + ΔT.
- **Alertes cliniques** : règles temps réel O(N) basées sur pression/température/COP.

Important : **outil d’aide** destiné à la surveillance et à l’exploration. **Ce n’est pas un diagnostic**.

### Références de seuils (à afficher / rappeler)


- **ΔT 2.2°C** (≈ 4°F) **contralatéral** sur **2 jours consécutifs** → indicateur de prévention (hotspot).
- **Objectif** de pic de pression in-shoe **< 200 kPa** sur zones à risque **si capteurs calibrés**.

### Niveaux de données (séparation)


Dans ce projet, on distingue :

- **raw** : valeurs capteurs telles que reçues (FSR brutes).
- **afterBaseline** : raw – baselineOffsets (clamp ≥ 0).
- **kPa (clinique)** : afterBaseline → kPa via calibration (clamp ≥ 0).

Les seuils “patient” (Tk) existants restent utilisés pour l’affichage et certains scores historiques. Les règles **cliniques** utilisent **kPa** (ou restent inactives si calibration absente).

### Calibration pression (FSR → kPa)


### Principe

Pour chaque **capteur** (sensor1..sensor13) et **pied** (left/right), on enregistre 2 ou 3 points :

- **P0** : 0 kPa (pied au repos / sans charge)
- **P1** : charge connue (kPa)
- option **P2** : seconde charge connue (kPa) → modèle piecewise

Ensuite, on ajuste :

- **linéaire** (2 points ou moindres carrés)
- **piecewise** (2 segments avec point de rupture sur P1)

### Où

UI : écran **Analyse** → “Calibration clinique — FSR → kPa”.

### Baseline température (°C)


### Principe

On capture une posture stable (immobile) et on calcule pour chaque zone :

- moyenne \( \mu \)
- écart-type \( \sigma \)

UI : écran **Analyse** → “Calibration clinique — Baseline température”.

### Alertes cliniques (résumé)


### Pression

- **PPP (Peak Plantar Pressure)** : événement par pas (max pendant STANCE). Alerte si **PPP > 200 kPa** (configurable) répétée ≥ N fois dans une fenêtre glissante.
- **PTI (Pressure-Time Integral)** : somme \( \sum p(t)\,dt \) par pas + agrégation fenêtre. Seuil par défaut **relatif** : > 2× la référence PTI (estimée au démarrage sur un nombre de pas).

### Température

- **Hotspot contralatéral** : ΔT ≥ 2.2°C (configurable) avec **persistance** (minutes) et règle **2 jours consécutifs** via résumé journalier.
- **Fallback baseline** : ΔT vs baseline ≥ 2.0°C (configurable) + persistance, avec filtre “surcharge mécanique probable” pour limiter les faux positifs.

### Proxy frottement / cisaillement (sans capteur shear)

Indicateur `friction_proxy` si :

- COP se déplace vite pendant STANCE (copSpeed > seuil)
- pression totale élevée
- corrélation avec hotspot thermique

### Exports CSV


Deux exports :

- **CSV (défaut)** : comportement historique (capteurs 1..13).
- **CSV clinique (CSV+)** : options `raw / afterBaseline / viz` + colonnes additionnelles (kPa, température, gaitState, COP, copSpeed) selon disponibilité des calibrations.

### Limitations & hypothèses


- Le mapping température “zone i ↔ capteur i” est un **fallback**. Si la semelle dispose d’un mapping clinique plus précis, il faut l’encoder explicitement.
- La baseline pression `baselineOffsets` est actuellement l’unique zéro utilisé (stocké localement). Une future évolution peut la rendre multi-pieds / par patient si nécessaire.
- Les alertes cliniques sont des heuristiques paramétrables. Les seuils peuvent nécessiter adaptation au protocole et aux capteurs.

### Disclaimer


Ce logiciel fournit des **indicateurs** et des **alertes** à but d’aide à la surveillance. Il ne remplace pas une évaluation clinique et ne doit pas être utilisé seul pour prendre des décisions médicales.

##  Glossaire

| Terme | Signification |
| --- | --- |
| **FSR** | Force Sensitive Resistor — capteur de pression de la semelle |
| **BLE** | Bluetooth Low Energy — liaison semelle ↔ app |
| **Cumul / footCumul** | Données agrégées par capteur et par patient (épisodes, intensité) |
| **Adhérence** | Régularité du port de la semelle sur 7 jours |
| **PTI** | Pressure-Time Integral — intégrale pression × temps |
| **Baseline** | Valeurs de référence d'un patient (température, marche) |
| **Renderer / Main / Preload** | Les 3 process Electron (UI / système / pont sécurisé) |