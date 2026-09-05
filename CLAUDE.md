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

- **Ambiance** : nature et minéral, immersif, **clair et zen**. Lumière douce, contrastes
  bas, matière plutôt que couleur. Le site respire le bien-être, pas la bijouterie.
- **Parti pris chromatique** : jour. Grès pâle, argile, taupe, or patiné très désaturé,
  encre chaude pour le texte. **Jamais de fond vert**, jamais de couleur saturée ou
  « boostée » — la marque vend des pierres **100 % naturellement teintées, non traitées**,
  le visuel doit rester fidèle à ça.
- **Un seul temps sombre** assumé dans la page : le bandeau de la phrase signature.
- **Animations attendues** (le client en veut, explicitement), toutes en **GSAP** :
  - **Ouverture cinématographique** : une scène de pierre mouillée plein écran pendant
    ~2,5 s, puis le logo émerge en fondu + léger zoom, puis la scène se retire vers le hero.
    La scène est **générée en WebGL** (shader de bruit fractal avec domaine déformé,
    reflets spéculaires d'eau, grain fin) — aucun fichier vidéo ni photo à fournir. Repli
    en dégradé Canvas 2D si WebGL est indisponible.
  - Titres qui montent ligne par ligne, bandeau de pierres défilant, cartes qui s'inclinent
    au survol, apparitions progressives au scroll via **ScrollTrigger**.
  - Une **interaction réelle** : l'atelier où l'on change la pierre et où les perles du
    bracelet se recomposent en cascade.
  - **Profondeur du hero** : six plans (ciel, falaise et cascade, brume, feuillage, pierres
    de premier plan, grain) qui glissent les uns sur les autres à la souris. Amplitude
    maximale ~10 px sur le plan le plus profond, lissage à 6 % par image : la scène dérive
    avec une inertie de caméra, elle ne suit pas le curseur. Les plans avant partent à
    l'inverse des plans arrière. Sans souris, dérive lente et autonome.
    Ce qui crée la profondeur, c'est d'abord la perspective atmosphérique et le flou de
    mise au point, pas la vitesse.
- **Règle non négociable** : aucune section ne doit rester invisible en attendant un scroll.
  Conciliation avec ScrollTrigger : on ne masque **que** les éléments déjà hors écran au
  chargement, et un filet de sécurité (8 s) rétablit tout élément dont le déclencheur n'est
  jamais parti. Le premier écran est toujours complet.


## Typographie

- Titres : **Cormorant Garamond** (serif, capitales fines, italique pour les mots accentués)
- Script de marque : **Mrs Saint Delafield** (reprend le « des Pierres » du logo, usage rare)
- Texte courant : **Jost** en graisse légère (200–400)

## Palette (version claire, pierre naturelle)

| Rôle | Valeur |
| --- | --- |
| Papier / fond | `#FAF7EF` — fond alterné `#F1EBDE`, creux `#E4DBC6` |
| Pierre (traits, bordures) | `#CFC5AC` — profond `#A99C7C` |
| Or patiné (accent) | `#9C8557` — clair `#C1AA80`, texte `#6C5A3A` |
| Mousse (accent rare, jamais en fond) | `#7E8871` — profond `#545C48` |
| Encre (texte) | `#322C24` — secondaire `#6C6353`, titres `#211D18` |


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
réflexes par défaut, mais **jamais sur le brief de marque ci-dessus** (direction claire et
zen, teintes naturelles non saturées, animations obligatoires, logo reconstitué en SVG).

## Conventions techniques

- HTML/CSS/JS autonome, sans framework ni build. Tout tient dans `index.html`.
- Seule dépendance externe : **GSAP + ScrollTrigger** (CDN cdnjs, version épinglée).
  Toutes les animations passent par GSAP, pas par des `@keyframes` dispersés.
- **L'ouverture doit toujours se fermer**, quoi qu'il arrive : `endIntro()` est idempotente
  et appelée par la timeline GSAP, par le repli CSS, et par un garde-fou à 5,2 s. Sur une
  machine lente, l'horloge de GSAP peut être affamée et la timeline ne jamais atteindre son
  terme — le visiteur ne doit pas rester bloqué sur l'écran d'ouverture.
- **Jamais deux moteurs d'animation lourds en même temps** : le shader WebGL de l'ouverture
  s'arrête avant que la boucle de parallaxe démarre. Ils se disputaient le GPU et gelaient
  la timeline (mesuré : 15 images en 7 s).
- **Pas de `filter: blur()` sur une grande surface animée.** Le flou est cuit dans le canvas
  au moment de la peinture. Deux halos floutés en plein écran coûtaient à eux seuls la
  moitié de la fluidité de la page (17 → 61 images/s une fois retirés). Un dégradé radial
  est déjà doux, il n'a pas besoin d'être flouté.
- Les calques du décor sont peints **une seule fois**, en basse résolution, un par image,
  et seulement après l'ouverture : la peinture ne doit jamais bloquer le fil principal.
- Polices via Google Fonts, images et icônes en SVG intégré.
- Toujours respecter `prefers-reduced-motion` : couper rideau, particules, parallaxe et
  rotations, garder la page lisible.
- Responsive : menu replié sous 1040px, grilles en une colonne sous 640px.
- Textes en français, apostrophes typographiques, pas d'emoji dans l'interface.
