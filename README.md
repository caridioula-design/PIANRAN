# PIANRAN Budget

Application de suivi et de gestion de budget (salaire, autres revenus, dépenses par catégorie).
100 % hors-ligne : les données restent sur le téléphone, dans IndexedDB.

## Contenu

```
www/                 ← l'application (HTML/CSS/JS, IndexedDB, service worker)
  index.html
  manifest.json
  sw.js
  icons/
capacitor.config.json ← configuration pour l'APK Android
package.json
.github/workflows/build-apk.yml ← construction automatique de l'APK sur GitHub
```

## Fonctions

- **Accueil** : reste disponible, revenus, dépensé, budget prévu, marge prévue, catégories à surveiller, où va l'argent.
- **Budget** : vos catégories avec le montant prévu (pré-remplies avec votre tableau : 273 350 F prévus pour 285 000 F de salaire), barre de progression, bouton « Payer le reste » pour régler une charge fixe en un geste.
- **Mouvements** : toutes les dépenses et revenus du mois, filtrables, modifiables, suppression avec « Annuler ».
- **Réglages** : thème clair/sombre, sauvegarde/restauration JSON, export CSV du mois, effacement.
- Changement de mois avec les flèches en haut ; « Reprendre les revenus du mois dernier » quand un nouveau mois commence.

## Obtenir l'APK — 3 façons

### A. GitHub Actions (le plus simple, rien à installer)
1. Créez un dépôt GitHub et envoyez-y tout le dossier (`git push` sur la branche `main`).
2. Onglet **Actions** → « Construire l'APK » se lance tout seul (~5 min).
3. Ouvrez l'exécution terminée → section **Artifacts** → téléchargez `PIANRAN-Budget-apk` (zip contenant `app-debug.apk`).
4. Copiez l'APK sur le téléphone et installez-le (autorisez « sources inconnues »).

### B. Android Studio sur votre PC
```bash
npm install
npx cap add android
npx cap sync android
npx cap open android      # puis Build > Build APK(s)
```
L'APK se trouve dans `android/app/build/outputs/apk/debug/`.

### C. PWABuilder (sans code)
1. Hébergez le dossier `www/` en HTTPS (GitHub Pages, Netlify Drop…).
2. Allez sur pwabuilder.com, collez l'adresse, choisissez **Android** → téléchargez le paquet APK.

### Tester tout de suite sans APK
`npm run serve` puis ouvrez `http://localhost:8080` — ou ouvrez la version hébergée sur Chrome Android → menu ⋮ → **Installer l'application**.

## Données
- Base IndexedDB `pianran-budget` : magasins `categories`, `transactions` (index `month`), `meta`.
- Désinstaller l'app efface ses données : pensez à **Réglages → Sauvegarder** régulièrement.
