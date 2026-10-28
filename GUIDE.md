# Guide de mise en ligne : Firebase puis GitHub Pages

Durée : environ 30 minutes. Les noms des menus Firebase et GitHub évoluent parfois : si un libellé diffère légèrement, cherchez l'équivalent.

## Partie 1. Créer le projet Firebase

1. Allez sur https://console.firebase.google.com et connectez-vous avec un compte Google.
2. **Ajouter un projet**, nom : `pharmarevis`. Désactivez Google Analytics (inutile ici), puis **Créer le projet**.
3. **Authentication** : menu Build > Authentication > **Commencer** > onglet « Sign-in method » > **Google** > Activer. Choisissez un e-mail d'assistance, puis **Enregistrer**.
4. **Firestore** : menu Build > Firestore Database > **Créer une base de données**.
   - Emplacement : une région européenne (par exemple `europe-west9` Paris ou `eur3`). Ce choix est définitif.
   - Mode : **production**.
5. Onglet **Règles** de Firestore : remplacez tout le contenu par celui du fichier `firestore.rules`, puis **Publier**.
6. **Récupérer la configuration** : roue dentée > Paramètres du projet > « Vos applications » > icône web `</>` > nom `pharmarevis` > Enregistrer l'application (ne cochez pas Firebase Hosting). Copiez l'objet `firebaseConfig` affiché.
7. Ouvrez `firebase-config.js` et remplacez chaque valeur « VOTRE_… » par celles copiées.

La clé `apiKey` n'est pas un secret : elle identifie le projet. La protection des données repose sur les règles Firestore (étape 5) et sur les domaines autorisés (partie 3).

## Partie 2. Déposer le code sur GitHub

1. Créez un compte sur https://github.com si besoin.
2. **New repository** : nom `pharmarevis`, visibilité **Public** (GitHub Pages gratuit sur dépôt public), ne cochez aucune option d'initialisation.
3. Déposez les 5 fichiers à la **racine** du dépôt (pas dans un sous-dossier) : `index.html`, `firebase-config.js`, `firestore.rules`, `README.md`, `GUIDE.md`.
   - Méthode simple : sur la page du dépôt, **uploading an existing file**, glissez les fichiers, puis **Commit changes**.
   - Méthode en ligne de commande, depuis le dossier du projet :
     ```
     git init
     git add .
     git commit -m "PharmaRévis"
     git branch -M main
     git remote add origin https://github.com/VOTRE_NOM/pharmarevis.git
     git push -u origin main
     ```

## Partie 3. Activer GitHub Pages et autoriser le domaine

1. Dans le dépôt : **Settings > Pages**. Source : **Deploy from a branch**, branche `main`, dossier `/ (root)`, **Save**.
2. Après une à deux minutes, le site est disponible à l'adresse `https://VOTRE_NOM.github.io/pharmarevis/`.
3. Retournez dans Firebase : Authentication > **Settings** (Paramètres) > **Authorized domains** > **Add domain** > `VOTRE_NOM.github.io` (sans `https://` ni chemin). Sans cette étape, la connexion Google échoue.

## Partie 4. Tester

1. Ouvrez l'adresse du site et cliquez sur **Se connecter avec Google**.
2. Révisez une carte : le message « Synchronisé » doit s'afficher.
3. Dans Firebase > Firestore > collection `users` : un document à votre identifiant doit apparaître.
4. Ouvrez le site sur un autre appareil, connectez-vous avec le même compte : les cartes et la progression se chargent.

Test en local : l'ouverture directe du fichier (`file://`) ne charge pas la configuration Firebase. Lancez plutôt `python3 -m http.server` dans le dossier, puis ouvrez `http://localhost:8000`.

## Fonctionnement et limites

- Sans connexion, l'application reste utilisable : tout est enregistré dans le navigateur.
- Avec connexion, chaque modification est envoyée au cloud après environ 1,5 seconde. À la connexion, la version la plus récente (appareil ou cloud) l'emporte. Si deux appareils sont modifiés hors ligne puis reconnectés, la dernière modification écrase l'autre.
- Les données de l'utilisateur sont stockées dans un seul document Firestore (limite d'environ 1 Mo, soit plusieurs milliers de cartes).

## Pour aller plus loin (facultatif)

- Dans Google Cloud Console > API et services > Identifiants, restreignez la clé API aux référents HTTP `VOTRE_NOM.github.io/*`.
- Surveillez l'usage dans la console Firebase. Le plan gratuit suffit largement pour un usage personnel, mais vérifiez les quotas actuels.
- Si d'autres personnes utilisent l'application, ajoutez une mention de confidentialité (RGPD) : seules l'adresse e-mail du compte et les cartes sont stockées.
