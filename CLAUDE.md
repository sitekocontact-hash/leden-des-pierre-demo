# L'Eden des Pierres — brief de marque et direction artistique

Ce fichier est lu automatiquement par Claude Code à chaque session sur ce dépôt.
Il sert de mémoire : plus besoin de réexpliquer la direction à chaque fois.

## La marque

- **Nom** : L'Eden des Pierres · **Créatrice** : Sonia
- **Produit** : bracelets et créations en **pierres naturelles et perles**, montés à la main,
  perle par perle. Jamais de série : chaque pièce est unique.
- **Positionnement** : artisanal, sincère, haut de gamme sans ostentation. La créatrice parle
  à la première personne ("je sélectionne", "j'aime ces différences").
- **Argument central** : une pierre naturelle n'est jamais identique à une autre. Les
  différences de teinte, de dessin, d'inclusion et de transparence ne sont pas des défauts,
  c'est la signature de la pierre.
- **Signature** : « Des pierres naturelles. Des créations qui ont leur propre identité. »

## Pierres travaillées (référence)

Améthyste (quartz violet) · Quartz rose (laiteux) · Citrine (quartz miel) ·
Labradorite (feldspath chatoyant) · Œil de tigre · Pierre de lune (feldspath opalescent).

## Direction artistique voulue

- **Ambiance** : nature et minéral, immersif, **moderne et animé**. Fond nature vivant
  (brume qui dérive, poussière lumineuse, feuillages en parallaxe), pas de page statique.
- **Parti pris chromatique** : nocturne. Verts forêt profonds, sauge, or antique, ivoire.
  Surfaces en verre dépoli plutôt que cartes blanches.
- **Animations attendues** (le client en veut, explicitement) :
  - Animation d'ouverture à l'arrivée : le logo se **dessine** trait par trait, puis le rideau se lève.
  - Le logo vit : halo qui respire, particules en orbite, éclats qui scintillent.
  - Titres qui montent ligne par ligne, bandeau de pierres défilant, cartes qui s'inclinent au survol.
  - Au moins une **interaction réelle** : l'atelier où l'on change la pierre et où les perles
    du bracelet se recomposent.
- **Règle non négociable** : aucune section ne doit rester invisible en attendant un scroll
  (pas d'`opacity: 0` piloté par IntersectionObserver ni `animation-timeline: view()` sans
  état visible de repos). Les animations d'entrée se jouent au chargement.

## Typographie

- Titres : **Cormorant Garamond** (serif, capitales fines, italique pour les mots accentués)
- Script de marque : **Mrs Saint Delafield** (reprend le « des Pierres » du logo, usage rare)
- Texte courant : **Jost** en graisse légère (200–400)

## Palette (version nocturne)

| Rôle | Valeur |
| --- | --- |
| Fond nuit | `#080D08` / `#0C130C` |
| Écorce / mousse | `#111A11` / `#18261A` |
| Sauge | `#9DBA8B` (atténué `#7A9569`) |
| Or | `#D2AC63` (clair `#EBD5A6`, profond `#8E7134`) |
| Ivoire (texte) | `#F1EEE3` — texte secondaire `#A6B29B` |

## Logo

Le logo original est un cercle doré avec branche d'eucalyptus, cristaux gravés, « L'Eden »
en serif, « des Pierres » en anglaise dorée, puis « Sonia ». Il est **reconstitué en SVG**
dans `index.html` (symboles `#seal-decor` pour la version complète et `#mark-small` pour
l'icône de navigation). Réutiliser ces symboles plutôt que de repartir d'une image bitmap :
ils restent nets à toute taille et se colorent via les variables CSS.

## À faire fournir par la cliente

- Photos réelles des créations (les pierres sont pour l'instant des illustrations SVG)
- Coordonnées : email et compte Instagram
- Éventuellement : tarifs, délais de fabrication, conditions d'envoi

## Skills de design installés

Le dépôt embarque deux compétences sous `.claude/skills/` (voir leur README) :

- **`impeccable`** — direction artistique et contrôle qualité, avec ses commandes
  `/impeccable polish`, `audit`, `critique`, `animate`, `bolder`, `quieter`, `harden`.
- **`ui-ux-pro-max`** — base consultable de styles, palettes, associations de polices,
  règles UX, presets d'animation.

Les utiliser pour toute nouvelle page ou refonte de ce projet : elles priment sur les
réflexes par défaut, mais **jamais sur le brief de marque ci-dessus** (direction nocturne,
animations obligatoires, logo reconstitué en SVG).

## Conventions techniques

- HTML/CSS/JS autonome, sans framework ni build. Tout tient dans `index.html`.
- Polices via Google Fonts, images et icônes en SVG intégré.
- Toujours respecter `prefers-reduced-motion` : couper rideau, particules, parallaxe et
  rotations, garder la page lisible.
- Responsive : menu replié sous 1040px, grilles en une colonne sous 640px.
- Textes en français, apostrophes typographiques, pas d'emoji dans l'interface.
