# Caisse Bar

Caisse de vente de boissons pour tablette ou smartphone Android. Elle fonctionne hors ligne une fois installée.

## Mise en ligne sur GitHub Pages (une seule fois)

1. Connectez-vous sur https://github.com.
2. Cliquez sur **New** (nouveau dépôt) :
   - Repository name : `bar`
   - Cochez **Public**
   - Cliquez sur **Create repository**
3. Sur la page du dépôt, cliquez sur **uploading an existing file** (ou **Add file → Upload files**).
4. Dézippez `caisse-bar-github.zip` sur votre PC, puis glissez **tout le contenu** dans la page :
   `index.html`, `manifest.webmanifest`, `sw.js`, `catalogue.json`, `README.md` et le dossier `icons`.
5. Cliquez sur **Commit changes**.
6. Allez dans **Settings → Pages** :
   - Source : **Deploy from a branch**
   - Branch : **main**, dossier **/ (root)**
   - Cliquez sur **Save**
7. Attendez 1 à 2 minutes. L'adresse s'affiche en haut de la page Pages :
   `https://scraper147.github.io/bar/`

## Installation sur une tablette ou un smartphone

1. Connectez la tablette à internet (wifi ou partage de connexion).
2. Ouvrez l'adresse dans **Chrome**.
3. Menu **⋮ → Installer l'application** (ou **Ajouter à l'écran d'accueil**).
4. Lancez l'app depuis l'icône Caisse Bar.
5. Le catalogue se charge tout seul. Dans **Paramètres de la tablette**, choisissez le **point de vente** de la tablette, puis **Enregistrer**.

À partir de là, l'app fonctionne sans internet.

## Tablette ou smartphone

L'app choisit seule sa présentation au démarrage, selon la taille de l'écran :
- **Tablette** : panier sur le côté, affichage en paysage.
- **Smartphone** (plus petit côté de l'écran < 600 px) : affichage en portrait, produits sur deux colonnes, panier ouvert par la barre « Voir le panier » en bas.

Les ventes, l'export et le catalogue fonctionnent de la même façon sur les deux.

## Mettre à jour l'app

Remplacez les fichiers sur GitHub (**Add file → Upload files**, puis **Commit**).
Les tablettes prennent la nouvelle version la prochaine fois qu'elles ouvrent l'app avec du réseau.

## Mettre à jour les prix ou les produits

Le catalogue est le fichier `catalogue.json` du dépôt.

1. Modifiez `catalogue.json` (ou remplacez-le par celui exporté de l'app admin).
2. **Augmentez le numéro `version`** (par exemple de 2 à 3), sinon les tablettes ne verront pas le changement.
3. Déposez-le sur GitHub (**Add file → Upload files**, puis **Commit**).

À la prochaine ouverture avec du réseau, chaque tablette affiche « Nouveau catalogue disponible » et propose de l'installer.
Le bouton **Paramètres de la tablette → Vérifier les mises à jour** force la vérification.

## Bonnes pratiques

- Exportez les ventes au moins **deux fois par jour** (midi et soir) : menu **⋮ → Exporter / partager les ventes du jour**.
- Pour retélécharger le fichier d'un jour précédent : menu **⋮ → Ventes des jours précédents → Télécharger**.
- N'effacez jamais les données de Chrome sur les tablettes de caisse.
- **Mémoire de l'appareil** (environ 5 Mo, partagés avec les autres caisses du même compte GitHub) : la jauge est dans **⋮ → Ventes des jours précédents**. Au-delà de 80 %, un bandeau orange s'affiche : effacez alors les anciens jours. Un jour ne peut être effacé qu'après avoir été téléchargé, et jamais le jour en cours.
- Si l'enregistrement échoue (mémoire pleine), une alerte rouge s'affiche : **exportez immédiatement** les ventes du jour, sans fermer l'app.
- Une tablette = un point de vente.

## Important si la caisse sapins est sur le même compte GitHub

Les caisses du compte partagent l'adresse `scraper147.github.io` (caisse sapins dans `/sapin/`, Caisse Bar dans `/bar/`). Pour qu'elles cohabitent :
- clés de stockage propres : `bar-caisse`, `bar-caisse-catalogue` ;
- cache hors ligne propre, préfixé `caisse-bar-` (actuellement `caisse-bar-v9`) : une mise à jour de la Caisse Bar ne supprime que ses anciens caches, jamais ceux de la caisse sapins ;
- icône « Caisse Bar », `start_url` et `scope` limités à `./` (le dossier `/bar/`).

Pour une mise à jour, augmentez uniquement le numéro dans `sw.js` (`var CACHE = PREFIX + 'v10';`), sans changer le préfixe.
