# Architecture - Niveau Conteneurs (C4 - Niveau 2)

## Vue d'ensemble
Le système Digi'Feet est composé d'un ensemble de capteurs hardware communicant avec des applications clientes (SaaS et Mobile), qui s'appuient sur une API centralisée pour le stockage et la logique métier.

## Conteneurs

### 1. Hardware (Dispositif Patient)
- **Technologie :** Arduino MKR WiFi 1010 (BLE)
- **Responsabilité :** Captation des pressions plantaires et températures, transmission des données en temps réel au client SaaS via Bluetooth (BLE).

### 2. Clients (Frontend)
- **SaaS (Interface Praticien)**
  - **Technologie :** React, Electron, Python (script client BLE)
  - **Responsabilité :** Tableau de bord pour le praticien, réception en temps réel des données capteurs, gestion des paramètres cliniques.
- **Native App (Interface Patient)**
  - **Technologie :** React (Capacitor / React Native)
  - **Responsabilité :** Interface mobile simplifiée pour le patient, réception des alertes de surpression et suivi quotidien.

### 3. Serveur A (API Backend)
- **Technologie :** Java + Spring Boot, Docker
- **Responsabilité :** Fournir une API RESTful (HTTP/JSON). Gérer la logique métier, l'authentification, le calcul des historiques et l'interface avec la base de données.

### 4. Serveur B (Base de données)
- **Technologie :** PostgreSQL, Docker
- **Responsabilité :** Stockage persistant et relationnel des profils (patients/praticiens), des historiques de données médicales, des configurations des seuils et des alertes.

## Diagramme
(insérer diagramme ici)
