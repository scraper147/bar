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

## Ajouter un article depuis l'app

Menu **⋮ → Ajouter un article au catalogue** : choisir une catégorie (ou en créer une), saisir le libellé et le prix, puis **Créer l'article**.
- L'app affiche l'**ID** de l'article (et de la catégorie si elle est nouvelle). Pour avoir le même article sur un autre appareil, créez-le là-bas avec **exactement le même ID** (champ « ID de l'article »).
- Ces articles sont propres à l'appareil et sont **gardés** lors des mises à jour de `catalogue.json`. Si le catalogue officiel contient un jour le même ID, c'est la version officielle qui est utilisée.
- Pour corriger une erreur : supprimer l'article dans la même fenêtre, puis le recréer. Les ventes déjà faites ne changent pas.

## Exporter le catalogue de l'appareil

Menu **⋮ → Exporter le catalogue (catalogue.json)** : télécharge un `catalogue.json` au même format que celui du dépôt, qui reprend le catalogue installé **avec les modifications faites sur cet appareil** : articles ajoutés (même ID, dans leur catégorie ; une catégorie créée dans l'app est ajoutée à la fin), prix modifiés (deviennent les prix du catalogue) et articles désactivés (`"actif": false`, donc retirés de toutes les caisses). La version est augmentée d'un cran et la date mise à jour.

Pour l'appliquer à tous les appareils : déposer ce fichier à la place de `catalogue.json` dans le dépôt `bar`. Chaque caisse proposera ensuite « Nouveau catalogue disponible » → **Installer**. Un seul appareil à la fois doit faire ses modifications et l'export, sinon le dernier fichier déposé écrase les changements de l'autre.

## Annuler une vente

Onglet **Historique** : choisir le jour (aujourd'hui ou l'un des 6 jours précédents), puis **Annuler** sur la vente concernée, avec un motif facultatif.
- La vente n'est pas effacée : elle reste affichée barrée avec l'heure et le motif de l'annulation, et figure dans l'export avec un champ `annulation`. Elle n'est plus comptée dans les totaux (`totalJournee`, `totalCash`, `totalBancontact`, `nombreVentes` ; `nombreAnnulations` en plus).
- Si le jour avait déjà été exporté, il faut le télécharger à nouveau (l'app le signale).
- Une annulation ne peut pas être défaite. Le remboursement éventuel (cash ou terminal Bancontact) se fait à part.

## Activer / désactiver des articles, changer un prix

Menu **⋮ → Gérer le catalogue (activer / désactiver)** : liste de tous les articles par catégorie, avec un interrupteur par article et un « Tout activer / Tout désactiver » par catégorie.
- Un article désactivé n'apparaît plus dans la caisse ; une catégorie sans article actif est masquée.
- Le réglage est propre à chaque appareil et reste valable après les mises à jour de `catalogue.json`. Le catalogue lui-même n'est pas modifié.
- **Changer un prix** : toucher le prix de l'article, saisir le nouveau prix, **Enregistrer**. Le prix d'origine reste affiché (« catalogue : … ») et le bouton **Revenir au prix du catalogue** annule la modification. Le nouveau prix vaut pour les prochaines ventes de cet appareil ; les ventes déjà faites ne changent pas.

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
- cache hors ligne propre, préfixé `caisse-bar-` (actuellement `caisse-bar-v16`) : une mise à jour de la Caisse Bar ne supprime que ses anciens caches, jamais ceux de la caisse sapins ;
- icône « Caisse Bar », `start_url` et `scope` limités à `./` (le dossier `/bar/`).

Pour une mise à jour, augmentez uniquement le numéro dans `sw.js` (`var CACHE = PREFIX + 'v17';`), sans changer le préfixe.
