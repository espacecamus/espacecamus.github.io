# Projet Espace – Collège Albert Camus

Site web réalisé par Valentin et Mati, élèves du collège Albert Camus (La Norville) dans le cadre du projet Espace.

---

## Les modifications apportées

Après la première version réalisée par les élèves, plusieurs améliorations ont été apportées. Voici le détail de chaque commit, dans l'ordre chronologique (du plus ancien au plus récent).

---

### 1. `Correction des fautes d'orthographe`

**Fichier modifié :** `index.html`

#### Ce qui a été fait

Le fichier `index.html` contenait des fautes d'orthographe et de ponctuation dans les textes affichés sur le site : des mots mal écrits ("sugestions", "exeptionnelle", "occassion", "raté"), des virgules manquantes, et des majuscules oubliées après un point.

Ce commit les corrige toutes, sans toucher à la structure HTML ni au CSS.

#### Pourquoi c'est important

Un site web, c'est aussi un texte lu par des visiteurs réels. Des fautes d'orthographe donnent une mauvaise image du projet, comme si le travail avait été bâclé. Soigner l'écriture, c'est aussi soigner le code.

#### Notions HTML abordées

Ce commit ne modifie pas les balises mais rappelle un principe fondamental : **le contenu d'une balise** (ce qui est entre `<p>...</p>` par exemple) est du texte pur que le navigateur affiche tel quel. La qualité de ce texte est la responsabilité du développeur.

---

### 2. `Creation des plusieurs pages HTML pour un chargement plus rapide`

**Fichiers créés :** `album.html`, `astropi.html`, `description.html`, `evenement.html`, `maquette.html`, `projets.html`, `publications.html`, `remerciements.html`, `temoignages.html`

#### Ce qui a été fait

Dans la version originale, **tout le site tenait dans un seul fichier `index.html`**. La navigation fonctionnait avec des boutons JavaScript qui affichaient ou cachaient des `<section>` (des blocs) à l'intérieur de cette unique page. Le résultat : le navigateur devait tout charger d'un coup, même les parties que le visiteur ne regardait pas.

Ce commit remplace cette logique par une **vraie navigation multi-pages** : chaque thème devient un fichier HTML séparé. La navigation utilise maintenant des liens `<a href="album.html">`, `<a href="evenement.html">`, etc., qui chargent la page demandée à la demande.

Avant le commit, la navigation ressemblait à :
```html
<button onclick="showPage('album')">Album</button>
```

Après, elle ressemble à :
```html
<a href="album.html" class="active">Album</a>
```

#### Pourquoi c'est important

- **Vitesse** : le navigateur ne charge que la page demandée, pas les 10 sections en même temps.
- **Lisibilité du code** : un fichier de 50 lignes est beaucoup plus facile à comprendre et modifier qu'un fichier de 500 lignes.
- **Organisation** : chaque fichier a une responsabilité claire. C'est un principe fondamental en programmation.

#### Notions HTML abordées

| Balise / Attribut | Rôle |
|---|---|
| `<a href="page.html">` | Crée un lien vers un autre fichier HTML |
| `class="active"` | Marque le lien de la page courante (pour le mettre en surbrillance en CSS) |
| `<section>` | Regroupe un bloc de contenu thématique dans la page |
| `<nav>` | Balise sémantique pour la barre de navigation |

---

### 3. `Affichage plus rapide et plus stylé des photos`

**Fichiers modifiés :** `album.html`, `astropi.html`, `styles.css`

#### Ce qui a été fait

Les photos s'affichaient les unes en dessous des autres, chacune avec la balise `<img class="album-image">`. Ce commit les réorganise en **galerie en grille** : les images s'alignent en colonnes automatiquement, quelle que soit la taille de l'écran. Un effet de zoom s'active quand on passe la souris sur une photo.

Un **lightbox** a aussi été ajouté : quand on clique sur une photo, elle s'affiche en grand en plein écran.

Voici le CSS ajouté dans `styles.css` :
```css
.gallery {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
    gap: 14px;
}
.gallery-item img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform 0.3s ease;
}
.gallery-item:hover img {
    transform: scale(1.07);
}
```

#### Pourquoi c'est important

Avant ce commit, les images pouvaient déborder de l'écran ou s'afficher dans des tailles incohérentes. La grille CSS règle ce problème automatiquement et s'adapte aux écrans de toutes tailles (mobile, tablette, ordinateur).

#### Notions CSS abordées

| Propriété CSS | Ce qu'elle fait |
|---|---|
| `display: grid` | Active la mise en page en grille (colonnes et lignes) |
| `grid-template-columns: repeat(auto-fill, minmax(240px, 1fr))` | Crée autant de colonnes que possible, chacune d'au moins 240px |
| `gap` | Espace entre les éléments de la grille |
| `object-fit: cover` | Recadre l'image pour qu'elle remplisse bien son conteneur sans se déformer |
| `transition` | Anime progressivement un changement de style (ici, le zoom) |
| `:hover` | Pseudo-classe : applique un style quand la souris survole l'élément |
| `transform: scale(1.07)` | Agrandit légèrement l'élément (zoom de 7%) |
| `loading="lazy"` | Attribut HTML : charge les images seulement quand elles sont sur le point d'être visibles |

---

### 4. `Affichage d'une timeline en CSS pour les evenements`

**Fichiers modifiés :** `evenement.html`, `styles.css`

#### Ce qui a été fait

La liste des événements était affichée comme de simples paragraphes séparés par des lignes de tirets (`___...___`). Ce commit la transforme en une **frise chronologique visuelle** : chaque événement est une carte avec une date, un lieu, un titre, et un badge "Passé" ou "À venir".

Chaque événement est maintenant une `<div class="event-card">` :
```html
<div class="event-card past">
  <div class="event-meta">
    <span class="event-date">21 septembre 2025</span>
    <span class="event-location">Chartres</span>
    <span class="event-badge badge-past">Passé</span>
  </div>
  <h3>Meeting aérien de Chartres</h3>
  <p>...</p>
</div>
```

#### Pourquoi c'est important

Avant ce commit, le lecteur devait lire chaque paragraphe pour trouver la date. Maintenant, il repère les événements en un coup d'œil grâce à la structure visuelle. **La mise en page est une forme de communication** : bien organiser l'information aide le visiteur à la comprendre.

#### Notions HTML et CSS abordées

| Concept | Ce qu'il fait |
|---|---|
| `<div>` | Conteneur générique, utilisé ici pour chaque carte d'événement |
| `<span>` | Conteneur en ligne, utilisé pour afficher la date, le lieu et le badge côte à côte |
| `class="past"` / `class="upcoming"` | Permet d'appliquer un style différent aux événements passés et à venir |
| `border-left` | La ligne verticale de la frise est une simple bordure gauche épaisse |
| `border-radius` | Arrondit les coins des cartes et des badges |
| `box-shadow` | Ajoute une ombre portée sous les cartes pour un effet de relief |

---

### 5. `Modification de l'image Filme ton collège`

**Fichiers modifiés :** `projets.html`, remplacement de l'image

#### Ce qui a été fait

L'image utilisée pour illustrer la section "Filme ton collège" était un fichier PNG généré par ChatGPT et pesait **3,1 Mo**. Elle a été remplacée par une version JPEG du même visuel qui pèse à peine 3,1 Mo également, mais dans un format bien plus adapté aux photos.

#### Pourquoi c'est important

Le format d'une image a un impact direct sur la vitesse de chargement du site. Une image de 3 Mo, c'est 3 secondes de chargement supplémentaires sur une connexion mobile. Multiplié par toutes les images du site, cela peut rendre le site très lent.

#### Notions à retenir

| Format | Quand l'utiliser |
|---|---|
| **JPEG** | Photos et images avec beaucoup de couleurs. Compressé, donc léger. |
| **PNG** | Images avec transparence (fond transparent), logos, icônes. |
| **SVG** | Dessins vectoriels (logos, icônes). Pèse très peu et ne pixélise jamais. |
| **WebP** | Format moderne, encore plus léger que JPEG pour la même qualité. |

---

### 6. `Mise a jour de la page publications`

**Fichiers modifiés :** `publications.html`, `styles.css`, ajout de `pub1.png` à `pub8.png`

#### Ce qui a été fait

La page des publications affichait 4 captures d'écran brutes dont certaines pesaient **600 Ko à 1 Mo chacune**. Ce commit les remplace par 8 images `pub1.png` à `pub8.png` recadrées et optimisées (entre 70 et 500 Ko chacune), et les organise dans une grille CSS similaire à celle de l'album.

#### Pourquoi c'est important

Des captures d'écran non optimisées sont l'une des principales causes de lenteur sur les sites web. Avant de publier une image, il faut toujours la redimensionner et la compresser avec un outil comme [Squoosh](https://squoosh.app) ou [TinyPNG](https://tinypng.com).

#### Notions à retenir

Réutiliser les mêmes classes CSS (`.gallery`, `.gallery-item`) sur plusieurs pages différentes montre l'intérêt d'un fichier CSS partagé : on écrit le style une seule fois, et il s'applique partout.

---

### 7. `Mies a jour de l'albulm et des astropi`

**Fichiers modifiés :** `album.html`, `astropi.html`, `styles.css`

#### Ce qui a été fait

De nouvelles photos ont été ajoutées dans les pages album et AstroPi, et leur organisation a été améliorée avec des sous-titres (`<h3>`) pour regrouper les photos par thème.

#### Pourquoi c'est important

Un site web n'est jamais "fini" : il évolue au fur et à mesure que le projet avance. Chaque ajout de contenu est un nouveau commit dans l'historique — ce qui permet de retrouver exactement quand et pourquoi une photo a été ajoutée.

---

### 8. `Rajout du lien vers ARISS`

**Fichiers modifiés :** toutes les pages HTML (10 fichiers)

#### Ce qui a été fait

Un nouveau lien "ARISS" a été ajouté dans la barre `<nav>` de **toutes les pages** du site :
```html
<a href="https://padlet.com/padfse/ariss-qaf1ndtv7npwkudz" target="_blank">ARISS</a>
```

L'attribut `target="_blank"` a été utilisé pour que le Padlet s'ouvre dans un **nouvel onglet** plutôt que de remplacer la page du site.

#### Pourquoi c'est important

La barre de navigation doit être **identique sur toutes les pages**. Si un visiteur est sur la page "Album" et qu'il ne voit pas le lien ARISS, il ne pourra jamais y accéder depuis cette page. Il a donc fallu modifier les 10 fichiers HTML un par un.

C'est justement pour éviter cette répétition fastidieuse que les développeurs professionnels utilisent des systèmes de **composants** ou de **templates** (comme React, Vue.js ou Jekyll) : la navigation est écrite une seule fois et incluse automatiquement dans toutes les pages.

#### Notions HTML abordées

| Attribut | Ce qu'il fait |
|---|---|
| `href="https://..."` | Lien vers une URL externe (commence par `https://`) |
| `href="page.html"` | Lien vers un fichier local (chemin relatif) |
| `target="_blank"` | Ouvre le lien dans un nouvel onglet |

---

### 9. `Affichage du film sur le site`

**Fichier modifié :** `projets.html`

#### Ce qui a été fait

Le film réalisé par les élèves était hébergé sur Google Drive. Ce commit l'intègre **directement dans la page** : au lieu d'afficher juste un lien, une vignette de prévisualisation s'affiche, avec un bouton ▶ qui apparaît au survol. Quand on clique, la vidéo se lance dans un lecteur intégré (une `<iframe>` vers Google Drive).

```html
<div id="video-container">
  <img id="video-poster" src="filmeTonCollege.jpeg">
  <!-- overlay avec le bouton ▶ -->
  <div id="video-overlay">...</div>
  <!-- lecteur vidéo chargé au clic -->
  <div id="video-frame">
    <iframe id="video-iframe" allow="autoplay" allowfullscreen></iframe>
  </div>
</div>
```

#### Pourquoi c'est important

Au lieu de forcer le visiteur à quitter le site pour aller sur Google Drive, le film est maintenant visible sans partir. Cela améliore l'**expérience utilisateur** (UX). La vidéo n'est chargée qu'au moment du clic, ce qui évite de ralentir le chargement initial de la page.

#### Notions HTML et CSS abordées

| Concept | Ce qu'il fait |
|---|---|
| `<iframe>` | Balise qui intègre une autre page web (ici le lecteur Drive) dans la page |
| `allow="autoplay"` | Autorise la vidéo dans l'iframe à démarrer automatiquement |
| `allowfullscreen` | Autorise le mode plein écran |
| `position: relative` / `position: absolute` | Superpose l'overlay (bouton ▶) par-dessus l'image de prévisualisation |
| `padding-bottom: 56.25%` | Astuce CSS classique pour que la vidéo garde un ratio 16:9 sur tous les écrans |
| `opacity: 0` + `transition` | Rend l'overlay invisible par défaut, puis l'anime en fondu au survol |

---

### 10. `Feuille de style global du site`

**Fichiers modifiés :** `styles.css` (entièrement réécrit) et toutes les pages HTML

#### Ce qui a été fait

C'est le commit le plus important visuellement. Le fichier `styles.css` a été entièrement réécrit pour :

1. **Définir des variables CSS** (couleurs, rayons d'arrondi, etc.) en un seul endroit
2. **Uniformiser** tous les éléments du site (header, nav, sections, liens, boutons…)
3. **Adopter une police moderne** : "Inter" au lieu de "Oswald" + Arial
4. **Rendre le site responsive** (adapté aux mobiles)

Voici comment les variables CSS fonctionnent :
```css
:root {
  --bg-base:  #08101e;   /* couleur de fond de la page */
  --accent:   #6366f1;   /* couleur violette principale */
  --text:     #e2e8f0;   /* couleur du texte */
}

/* Ensuite, on utilise ces variables partout : */
body {
  background: var(--bg-base);
  color: var(--text);
}
```
Si on veut changer la couleur principale du site, on modifie **une seule ligne** dans `:root` et tout le site se met à jour.

#### Pourquoi c'est important

Avant ce commit, les couleurs et tailles étaient répétées directement dans chaque règle CSS. Pour changer une couleur, il fallait chercher et remplacer dans tout le fichier. Les variables CSS éliminent ce problème : c'est l'application directe du principe **DRY** (*Don't Repeat Yourself* — Ne vous répétez pas), qui est l'un des fondamentaux du développement.

#### Notions CSS abordées

| Concept | Ce qu'il fait |
|---|---|
| `:root { --nom: valeur; }` | Déclare une variable CSS utilisable partout |
| `var(--nom)` | Utilise la valeur d'une variable |
| `@import url(...)` | Charge une police depuis Google Fonts |
| `clamp(min, préféré, max)` | Taille adaptative : grandit avec l'écran, mais reste entre min et max |
| `@media (max-width: ...)` | Règle CSS qui s'applique seulement en dessous d'une certaine largeur d'écran |
| `box-sizing: border-box` | Fait que la taille d'un élément inclut son padding et sa bordure |

---

### 11. `Modification de la banniere du site`

**Fichiers modifiés :** `styles.css`, toutes les pages HTML, ajout de `galaxy-banner.jpg`, `galaxy-bg.svg`, `galaxy.png`

#### Ce qui a été fait

La bannière du site (le grand titre en haut de chaque page) a été redessinée. Elle affiche maintenant une photo de galaxie en fond, avec un titre en dégradé de couleurs animé et un effet de "respiration" (zoom lent de la photo).

Voici le CSS de l'animation :
```css
/* L'animation s'appelle "galaxy-breathe" */
@keyframes galaxy-breathe {
  0%   { opacity: .82; transform: scale(1)    translateX(0); }
  100% { opacity: 1;   transform: scale(1.04) translateX(-1%); }
}

/* On l'applique à l'arrière-plan du header */
header::before {
  background-image: url('galaxy-banner.jpg');
  animation: galaxy-breathe 9s ease-in-out infinite alternate;
}
```

Le titre lui-même est en **dégradé de couleurs** :
```css
.header-title {
  background: linear-gradient(130deg, #ffffff, #e0e7ff, #a5f3fc, #22d3ee);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
```
Cette technique consiste à appliquer un dégradé comme fond, puis à "découper" ce fond en forme de texte.

#### Pourquoi c'est important

Une bannière soignée donne une première impression professionnelle. Ces effets ne nécessitent aucune librairie externe : tout est fait en CSS pur.

#### Notions CSS abordées

| Concept | Ce qu'il fait |
|---|---|
| `@keyframes nom { 0% {...} 100% {...} }` | Définit les étapes d'une animation |
| `animation: nom durée timing-function infinite` | Applique l'animation à un élément |
| `alternate` | L'animation fait l'aller puis le retour (0%→100%→0%→...) |
| `ease-in-out` | L'animation commence et finit lentement, accélère au milieu |
| `linear-gradient(angle, couleur1, couleur2)` | Dégradé de couleurs |
| `::before` | Pseudo-élément : crée un élément enfant invisible avant le contenu réel, utilisé ici pour le fond |
| `background-clip: text` | Découpe le fond en forme du texte |
| `transform: scale(1.04)` | Agrandit très légèrement l'élément (effet zoom) |
| `filter: drop-shadow(...)` | Ombre portée qui suit le contour exact d'un élément (meilleur que `box-shadow` pour le texte) |

---

### 12. `Mise a jour du lien vers le drive pour les photos`

**Fichier modifié :** `album.html`

#### Ce qui a été fait

Le lien vers le Google Drive contenant les photos du projet avait changé d'URL. Ce commit met à jour ce lien dans `album.html` pour pointer vers la nouvelle adresse.

#### Pourquoi c'est important

Un lien cassé (qui ne mène nulle part) est une erreur grave sur un site web : le visiteur clique et obtient une page d'erreur. Il faut régulièrement **tester tous les liens** d'un site et les mettre à jour quand les ressources externes changent d'adresse.

---

### 13. `Ajout du CopyRight`

**Fichiers modifiés :** toutes les pages HTML, `styles.css`

#### Ce qui a été fait

Un **pied de page** a été ajouté en bas de chaque page :
```html
<footer>
  <p class="footer-title">© Projet Espace — Collège Albert Camus de La Norville</p>
  <p class="footer-made">🛸 Site réalisé avec passion par <strong>Valentin</strong> et <strong>Mati</strong> ✨</p>
</footer>
```

Le style correspondant a été ajouté dans `styles.css` :
```css
footer {
  text-align: center;
  padding: 28px 20px;
  border-top: 1px solid var(--border);
  color: var(--muted);
  font-size: .82rem;
}
```

#### Pourquoi c'est important

Le `<footer>` est une **balise sémantique** : elle indique au navigateur (et aux moteurs de recherche comme Google) que ce bloc est le pied de page. Utiliser les bonnes balises sémantiques (`<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`) aide au **référencement** (SEO) et à l'accessibilité du site.

#### Notions HTML et CSS abordées

| Concept | Ce qu'il fait |
|---|---|
| `<footer>` | Balise sémantique pour le pied de page |
| `<strong>` | Met le texte en **gras** et indique qu'il est important sémantiquement |
| `border-top` | Ligne de séparation au-dessus du footer |
| `text-align: center` | Centre le texte horizontalement |

---

### 14. `Mise a jour de la page d'accueil`

**Fichier modifié :** `index.html`

#### Ce qui a été fait

Quelques ajustements de contenu sur la page d'accueil : reformulation de certaines phrases, suppression d'éléments devenus obsolètes (comme le numéro de version "V1.7" affiché dans le texte), et ajustement des espacements.

#### Pourquoi c'est important

La page d'accueil est la **première page** que voit un visiteur. Elle doit donner envie d'explorer le site. Un contenu à jour, sans informations obsolètes, montre que le site est maintenu activement.

---

### 15. `Mise a jour du contenu`

**Fichiers modifiés :** `album.html`, `astropi.html`, `description.html`, `evenement.html`, `index.html`, `maquette.html`, `projets.html`, `remerciements.html` ; suppression de `publications.html` et `temoignages.html`

#### Ce qui a été fait

Ce commit met à jour le contenu textuel de plusieurs pages et **supprime deux pages** devenues inutiles :
- `temoignages.html` : section vide sans contenu
- `publications.html` : remplacée par une version améliorée intégrée différemment

#### Pourquoi c'est important

Supprimer du code inutile est aussi important qu'en écrire. Des pages vides ou abandonnées peuvent créer de la confusion pour les visiteurs et les développeurs. Un projet bien tenu se nettoie régulièrement.

---

### 16. `Petite coquille`

**Fichier modifié :** `evenement.html`

#### Ce qui a été fait

Une petite faute de frappe ("coquille") avait été introduite dans le texte de la page événements lors d'une modification précédente. Ce commit la corrige.

#### Pourquoi c'est important

Même les développeurs expérimentés font des erreurs. C'est la raison pour laquelle on **teste et relit toujours** son travail avant de publier. En HTML, une faute dans le texte ne fait pas "planter" le site — contrairement à une erreur dans le code — mais elle reste visible par tous les visiteurs.

---

### 17. `fichier .gitignore`

**Fichier créé :** `.gitignore`

#### Ce qui a été fait

Un fichier `.gitignore` a été créé à la racine du projet. Son contenu est une liste de fichiers et dossiers que Git doit **ignorer** (ne pas suivre, ne pas publier).

Dans ce cas, le fichier `.claude/settings.json` (fichier de configuration d'un outil de développement) se trouvait dans le dépôt par erreur. Il a été retiré du suivi Git et ajouté au `.gitignore` pour éviter que cela se reproduise.

#### Pourquoi c'est important

Git suit par défaut **tous** les fichiers d'un dossier. Certains fichiers ne devraient jamais être publiés :
- Fichiers de configuration personnelle de l'éditeur de code
- Fichiers contenant des mots de passe ou des clés secrètes (`.env`)
- Fichiers temporaires générés automatiquement (`node_modules/`, `__pycache__/`, etc.)

Le `.gitignore` permet de les exclure définitivement.

---

## Comment rejouer les commits un par un

Git conserve tout l'historique du projet. Il est possible de **voyager dans le temps** et de voir l'état du site à chaque étape, du premier jour jusqu'à aujourd'hui.

### Prérequis

- Avoir Git installé sur l'ordinateur
- Avoir cloné le dépôt (`git clone ...`)
- Ouvrir un terminal dans le dossier du projet

### Afficher la liste complète des commits

```bash
git log --oneline
```

Chaque ligne affiche le **hash** (identifiant unique) et le **message** du commit. Exemple :
```
d0995d6 fichier .gitignore
b44dc9e Petite coquille
d956f7f Mise a jour du contenu
...
a4ddd93 Correction des fautes d'orthographe
```

### Se déplacer à un commit précis

```bash
git checkout a4ddd93
```

Remplacez `a4ddd93` par le hash du commit qui vous intéresse (les 7 premiers caractères suffisent).

Après cette commande, tous les fichiers du projet reviennent **exactement** à l'état qu'ils avaient au moment de ce commit. Ouvrez `index.html` dans un navigateur pour voir le site à cette étape.

> **Attention :** Git affichera un message "HEAD detached". C'est normal : vous êtes en mode lecture seule, vous "visitez" un point dans le passé sans modifier l'historique.

### Voir ce qu'un commit a changé

```bash
git show a4ddd93
```

Cette commande affiche les **lignes ajoutées** (en vert, précédées de `+`) et les **lignes supprimées** (en rouge, précédées de `-`) par ce commit.

### Voir les différences entre deux commits

```bash
git diff a4ddd93 5286bea
```

Affiche tout ce qui a changé entre le commit `a4ddd93` (correction orthographe) et le commit `5286bea` (création des pages).

### Revenir au dernier commit (présent)

```bash
git checkout main
```

Tous les fichiers reviennent à leur état actuel (le plus récent).

### Résumé des commandes utiles

| Commande | Ce qu'elle fait |
|---|---|
| `git log --oneline` | Liste tous les commits avec leur hash |
| `git checkout <hash>` | Se déplace à un commit précis |
| `git show <hash>` | Affiche les modifications d'un commit |
| `git diff <hash1> <hash2>` | Compare deux commits |
| `git checkout main` | Revient au présent |

---

## Ressources pour aller plus loin

Si vous voulez continuer à apprendre le HTML et le CSS :

- [MDN Web Docs (en français)](https://developer.mozilla.org/fr/) — la référence pour tout ce qui concerne le web
- [OpenClassrooms – Créez votre site web](https://openclassrooms.com/fr/courses/1603881-creez-votre-site-web-avec-html5-et-css3) — un cours complet pour débutants
- [CSS-Tricks – A Complete Guide to Grid](https://css-tricks.com/snippets/css/complete-guide-grid/) — tout sur CSS Grid (en anglais)
- [Squoosh](https://squoosh.app) — outil gratuit pour optimiser les images avant de les mettre en ligne
