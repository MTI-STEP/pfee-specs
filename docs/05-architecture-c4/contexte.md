# Contexte (C4 - Niveau 1)

## Vue d'ensemble

Le diagramme de contexte montre le système logiciel Digi'Feet dans son environnement global. L'objectif est de visualiser qui utilise le système et avec quels éléments matériels ou externes le système interagit.

## Acteurs (Personas)

- **Patient (Diabétique / Amputé) :** Utilisateur final qui porte le dispositif matériel. Il interagit avec le système principalement via l'application mobile pour consulter son état (alertes de surpression, scores de santé) de manière simplifiée.
- **Praticien (Professionnel de santé) :** Utilisateur clinique qui interagit avec le système via la plateforme SaaS (Desktop/Web). Il utilise le système lors des consultations ou à distance pour configurer les paramètres de suivi (seuils de pression/température), lire les historiques de données et suivre l'évolution clinique.

## Systèmes externes

- **Dispositif Hardware (Semelle / Prothèse) :** Matériel embarqué (incluant des capteurs FSR et thermiques connectés à une carte Arduino MKR WiFi 1010). Il n'a pas d'interface utilisateur mais transmet en continu des données brutes en temps réel au système logiciel.

## Le Système

- **Système Logiciel Digi'Feet :** La plateforme centrale (SaaS + Mobile + Backend) qui reçoit les flux de capteurs, calcule les indicateurs (PPP, PTI, Température de base), génère le score IA, déclenche les alertes et stocke l'historique médical pour le suivi.
