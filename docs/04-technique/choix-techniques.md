# Choix Techniques

## Frontend : React (+ Electron & Capacitor)
- **Justification :** Permet une grande réutilisabilité du code entre la plateforme SaaS (desktop via Electron) et l'application mobile (via React Native). L'écosystème React est idéal pour gérer les états complexes liés aux flux de données en temps réel.

## Script local : Python
- **Justification :** Utilisé pour la brique `ble_client.py` afin de gérer de manière stable et performante la connexion Bluetooth Low Energy (BLE) avec l'Arduino, ce qui est souvent plus complexe à gérer nativement en JavaScript depuis Electron.

## Backend : Spring Boot (Java)
- **Justification :** Framework robuste, fortement typé, sécurisé et idéal pour créer des API REST performantes. Il dispose d'un excellent écosystème pour la sécurité (Spring Security) et la gestion des données (Spring Data JPA).

## Base de données : PostgreSQL
- **Justification :** Base de données relationnelle (SQL) open-source très puissante. Parfaite pour garantir l'intégrité des données de santé (transactions ACID) et modéliser des relations complexes (Un praticien suit plusieurs patients, un patient génère des milliers de points de données).

## Infrastructure : Docker
- **Justification :** Conteneurisation de l'API et de la base de données pour garantir que les environnements de développement, de test et de production soient strictement identiques. Facilite grandement le déploiement.
