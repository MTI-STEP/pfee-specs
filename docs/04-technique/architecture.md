# Architecture

Décrivez l'architecture technique du projet, insérer votre schéma d'architecture technique également.

## Architecture (Electron + Vite + React)

### Vue d’ensemble

- **`apps/renderer`**: UI (Vite + React + TypeScript). Sert en dev sur `http://localhost:8080` et build en prod dans `dist/` à la racine.
- **`apps/main`**: process principal Electron (création de fenêtre, IPC, lancement backend BLE).
- **`apps/preload`**: preload Electron (API sécurisée exposée à `window.electronAPI`).
- **`electron/`**: backend BLE (`ble_client.py`) et son exécutable packagé `ble_backend/ble_client.exe` (suivi via Git LFS).
- **`android/`**: projet Capacitor pour le build mobile (généré via `npx cap sync`).

### Points d’entrée

- **Renderer**: `apps/renderer/index.html` → `apps/renderer/src/main.tsx`
- **Main**: `apps/main/src/main.js`
- **Preload**: `apps/preload/src/preload.cjs`