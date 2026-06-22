# Ma Boulangerie — créer le fichier APK (guide)

## Pourquoi PWABuilder affichait 7/45
Le fichier `boulangerie.html` seul est parfait pour un usage direct, mais il **ne peut pas** être transformé en `.apk` tel quel. PWABuilder vérifie qu'une vraie application web (PWA) est en ligne, et il attend trois choses qui manquaient :

1. un **manifeste** servi comme fichier (`manifest.webmanifest`), pas intégré dans la page ;
2. un **service worker** (`sw.js`) qui gère le mode hors-ligne ;
3. de vraies **icônes PNG** (192 px, 512 px + une version « maskable »).

Un fichier unique ouvert localement ne remplit aucun de ces critères → score très bas.

Le dossier fourni ici (`boulangerie-pwa.zip`) corrige les trois points. Une fois **mis en ligne**, le score sera élevé et l'APK pourra être généré.

## Étape 1 — Décompresser
Dézippez `boulangerie-pwa.zip`. Vous obtenez :
`index.html`, `manifest.webmanifest`, `sw.js`, `icon-192.png`, `icon-512.png`, `icon-512-maskable.png`, `favicon.png`.

## Étape 2 — Mettre en ligne (HTTPS obligatoire)
PWABuilder a besoin d'une adresse web en `https://`. Deux options gratuites :

**Option A — Netlify Drop (le plus rapide, sans coder)**
1. Allez sur `https://app.netlify.com/drop`.
2. Glissez-déposez **le dossier décompressé** dans la zone.
3. Netlify vous donne une adresse du type `https://nom-aleatoire.netlify.app`.

**Option B — GitHub Pages**
1. Créez un dépôt, téléversez les fichiers (à la racine).
2. Settings → Pages → activez le déploiement depuis la branche `main`.
3. Vous obtenez `https://votre-compte.github.io/votre-depot/`.

Ouvrez d'abord cette adresse dans Chrome pour vérifier que l'app s'affiche.

## Étape 3 — Générer l'APK avec PWABuilder
1. Allez sur `https://www.pwabuilder.com`.
2. Collez votre adresse `https://…` et lancez l'analyse. Le score doit maintenant être élevé.
3. Cliquez sur **Package For Stores** → **Android**.
4. Téléchargez le paquet. Il contient un **APK signé** (clé de test) pour l'installation directe, et un **AAB** si vous visez le Play Store, ainsi qu'un fichier `assetlinks.json` et les explications de signature.

## Étape 4 — Installer l'APK sur Android
1. Copiez le `.apk` sur le téléphone.
2. Ouvrez-le ; autorisez « Installer des applications inconnues » si demandé.
3. L'application s'installe comme une app normale.

> Astuce : pour masquer la petite barre d'adresse en haut (mode plein écran « TWA »), déposez le fichier `assetlinks.json` fourni par PWABuilder à la racine de votre site, comme indiqué dans ses instructions. Sans cela, l'app fonctionne quand même.

## Bon à savoir
- Les données (ventes, stock, clients, caissiers…) restent **sur l'appareil**. Pensez à exporter une sauvegarde depuis Paramètres → Exporter.
- Pour mettre l'app à jour plus tard : remplacez les fichiers en ligne, puis régénérez l'APK.
- Le `index.html` du dossier est exactement la même application que `boulangerie.html` (mêmes fonctions : rôle administrateur, reçus, clients à crédit, export PDF du rapport, etc.).
