# PharmaRévis

Application web de révision pour étudiante en pharmacie : HTML/CSS/JS, sans étape de compilation. Synchronisation facultative via Firebase.

## Fonctions
- **Réviser** : cartes à répétition espacée (algorithme inspiré de SM-2), filtre par thème.
- **QCM** : généré à partir des cartes (distracteurs pris dans le même thème).
- **Ordonnances** : 5 cas d'officine avec correction commentée.
- **Mes cartes** : ajout, suppression, import/export CSV (`question;réponse;thème`), packs par thème.
- **Calculs** : Cockcroft-Gault, dilution, débit de perfusion.
- **Synchronisation** (facultative) : connexion Google et sauvegarde Firestore. Sans configuration, l'application reste en mode local.

## Mise en route
Suivre `GUIDE.md` (Firebase, GitHub, GitHub Pages). Pour tester en local : `python3 -m http.server`, puis http://localhost:8000.

## Fichiers
`index.html` (application), `firebase-config.js` (à remplir), `firestore.rules` (règles de sécurité), `GUIDE.md`.

## Avertissement
Outil pédagogique. Vérifier toute information sur les sources officielles (ANSM, Thériaque, base de données publique des médicaments).
