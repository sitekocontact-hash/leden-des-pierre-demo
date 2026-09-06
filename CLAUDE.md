# L'Eden des Pierres — brief de marque et direction artistique

Ce fichier est lu automatiquement par Claude Code à chaque session sur ce dépôt.
Il sert de mémoire : plus besoin de réexpliquer la direction à chaque fois.

## La marque

- **Nom** : L'Eden des Pierres · **Créatrice** : Sonia
- **Produit** : bracelets et créations en **pierres naturelles et perles**, montés à la main,
  perle par perle. Jamais de série : chaque pièce est unique.
- **Vend aujourd'hui sur Facebook** ; le site est la vitrine qui prend le relais.
- **Positionnement** : artisanal, sincère, haut de gamme sans ostentation. La créatrice parle
  à la première personne ("je sélectionne", "j'aime ces différences").
- **Argument central** : une pierre naturelle n'est jamais identique à une autre. Les
  différences de teinte, de dessin, d'inclusion et de transparence ne sont pas des défauts,
  c'est la signature de la pierre.

## Pierres travaillées (référence)

Améthyste (quartz violet) · Quartz rose (laiteux) · Citrine (quartz miel) ·
Labradorite (feldspath chatoyant) · Œil de tigre · Pierre de lune (feldspath opalescent).

## Direction artistique — la mer tient la page

**Cette direction remplace les précédentes** (claire et zen ; écrin aubergine sur fond
plat ; puis cascade nocturne). Demandée par la cliente : un fond cinématique, une eau
animée en continu, et **le fond qui domine le contenu** — « limite qu'on voit plus
l'arrière-image que l'image tout court ». Les états antérieurs restent dans l'historique
git : la cascade est le commit juste avant celui de la mer, récupérable d'un `git revert`.

- **Le fond est le site.** Un canvas WebGL fixe, en `position: fixed` sur tout le viewport,
  derrière l'intégralité de la page. Ce n'est pas un décor de hero : la mer respire derrière
  la collection, le savoir-faire et le contact.
- **Un seul écran, un seul fichier** : `index.html` contient le HTML, le CSS et le JS.
  Aucun framework, aucune étape de build, aucune dépendance externe hors polices.

### Palette

| Rôle | Valeur |
| --- | --- |
| Eau profonde (fond) | `#0B1013` — creux `#101A1E` |
| Panneaux (translucides) | `rgba(9,14,17,0.72)`, plateau `rgba(6,10,12,0.85)` |
| Laiton (accent, vient du logo) | `#B98A4D` — clair `#D7AD75` |
| Texte | `#F3EDE3` (ivoire) — secondaire `#A9B4B6` |

Le fond sombre n'est pas qu'un choix esthétique : **de l'ivoire sur de l'eau noire tient le
contraste sans qu'on ait à poser quoi que ce soit sur l'image.** C'est ce qui règle
définitivement le problème du voile clair, rejeté à plusieurs reprises.

### Typographie

- Titres : **Fraunces** (serif chaleureux, axes `SOFT` et `WONK` utilisés)
- Texte courant : **Inter**, graisse légère (300–500)

## La mer : ce qui la fait lire comme de l'eau

Une cascade avait d'abord été tentée, puis rejetée — « peinte par un peintre ». La leçon
vaut pour toute eau calculée : **ce n'est pas la quantité de bruit qui fait le réalisme,
c'est la géométrie et la lumière.** Trois principes, à ne pas défaire :

1. **La perspective.** Chaque pixel sous l'horizon est reprojeté sur un plan d'eau
   (`z = 0.30 / (profondeur + 0.010)`). La distance explose près de l'horizon, donc la houle
   s'y écrase d'elle-même. Sans cette reprojection, les vagues gardent la même taille
   partout et la mer devient un papier peint.
2. **L'allée de lumière.** C'est la signature d'une mer éclairée : large et diffuse près de
   l'horizon, resserrée et piquée d'éclats au premier plan. Elle se calcule sur la **pente**
   de la houle (différence finie), jamais sur sa hauteur.
3. **L'extinction des rides au loin.** Les fréquences fines sont éteintes avec la distance
   (`fade`), sinon elles moirent près de l'horizon — le défaut qui trahit immédiatement une
   mer calculée.

Le soleil est à droite : **la gauche du cadre reste dans son ombre, et c'est cette ombre qui
porte le texte du hero.** L'éclairage de la scène, pas un voile posé dessus.

**Adaptation au format, obligatoire.** En portrait le texte occupe toute la largeur : il n'y
a plus de flanc sombre où le loger. Le shader lit donc le rapport d'aspect et, en portrait,
sort le soleil du cadre (`SUN` 0,84 → 1,06) et bride les éclats spéculaires (`sparkle` à
0,22). Mesuré : sans ce bridage, le sous-titre tombe à 1,5:1. C'est bien l'éclat spéculaire
qu'il faut réduire, pas la luminosité d'ensemble — assombrir toute la scène rendait l'image
terne sans régler le contraste.

**Garde-fous obligatoires** : demi-résolution, 30 images/seconde, arrêt quand l'onglet passe
en arrière-plan, et **repli en deux temps** — d'abord la résolution baisse, et seulement si
cela ne suffit pas l'image se fige. Une eau immobile derrière tout un site se voit beaucoup
plus qu'une eau un peu moins fine. En `prefers-reduced-motion`, une seule image est peinte
puis plus rien. Sans WebGL, le dégradé CSS du canvas prend le relais.

## Tics de page générée — à ne jamais réintroduire

La cliente a rejeté ces réflexes nommément. Ils sont interdits sur ce projet :

- fond crème + accent terracotta ;
- cartes identiques à coins arrondis avec la même ombre grise douce, façon SaaS ;
- labels en CAPITALES espacées, eyebrows au-dessus de chaque titre ;
- flèche `→` accolée au texte des boutons et des liens ;
- numérotation `01 / 02 / 03` sur du contenu qui n'est pas une séquence ;
- chaînes de méta jointes par des points médians (`A · B · C`).

**La collection ne se fait pas en cartes.** Elle est un **plateau unique** (`.tray`), divisé
par des filets, comme les logements d'un écrin de bijoutier. Posé sur l'eau sombre, il se
lit comme un coffret ouvert au-dessus de la mer.

## Animation

La mer ne s'arrête jamais : c'est le fond, pas un effet. **La seule animation d'interface**
est l'ouverture du texte du hero, jouée une fois au chargement. Rien d'autre — ni apparition
au défilement, ni effet au survol des pièces.

Elle est en CSS pur, déclenchée par une classe posée en JS. Le script ajoute `js` sur
`<html>` avant le premier rendu, ce qui seul active l'état de départ. Sans JS, la règle ne
s'applique pas et la page est simplement visible.

## Logo

Le logo original est un cercle doré avec branche d'eucalyptus, cristaux gravés, « L'Eden »
en serif, « des Pierres » en anglaise dorée, puis « Sonia ». Il est **reconstitué en SVG**
dans `index.html`. Seule l'icône de navigation (`#mark-small`) est utilisée sur cette
version ; la version complète du sceau (`#seal-decor`, cercle gravé, cristaux et branche
d'eucalyptus) reste disponible dans l'historique git si une page en a besoin. Réutiliser ces
symboles plutôt que de repartir d'une image bitmap : ils restent nets à toute taille et se
colorent via le dégradé `#brass-facet`.

## Emplacements des pierres

Le hero ne montre plus d'illustration : il est tenu par la mer et le titre seuls. Les quatre
pierres restent dans le plateau de la collection, sous forme de dégradés radiaux aux teintes
de chaque pierre, marqués « Photo à venir » en attendant les vraies photos.

## À faire fournir par la cliente

- **Le lien WhatsApp et l'adresse de la page Facebook** : les deux boutons de la section
  contact portent des URL de remplacement, signalées par un commentaire dans le HTML.
- **Photos réelles des créations.** Les quatre emplacements `.plate` affichent « Photo à
  venir » sur un dégradé aux teintes de la pierre concernée.
- Éventuellement : tarifs (aujourd'hui « Prix sur demande »), délais, conditions d'envoi.

## Skills de design installés

Le dépôt embarque trois compétences sous `.claude/skills/` (voir leur README) :

- **`impeccable`** — direction artistique et contrôle qualité.
- **`ui-ux-pro-max`** — base consultable de styles, palettes, associations de polices.
- **`frontend-design`** (Anthropic) — direction visuelle, repérage des tics de mise en page.

Les utiliser pour toute nouvelle page ou refonte, mais **jamais contre le brief ci-dessus** :
la palette, la typographie et la liste des tics interdits viennent de la cliente.

## Conventions techniques

- HTML/CSS/JS autonome, sans framework ni build. Tout tient dans `index.html`.
- **Seule dépendance externe : Google Fonts** (Fraunces et Inter). Pas de GSAP : l'eau est
  en WebGL et l'unique animation d'interface est en CSS.
- **Contraste au-dessus d'un fond qui bouge** : il se mesure sur plusieurs images, pas sur
  une capture. Le pire cas est le seul qui compte.
- Toujours respecter `prefers-reduced-motion`.
- **Le focus clavier doit rester visible partout** : contour laiton plein de 2 px, jamais
  supprimé. Vérifié par parcours au clavier, pas à l'œil.
- **Contrastes** : tout texte doit passer AA sur son fond réel (4,5:1, ou 3:1 au-delà de
  24 px). À vérifier par mesure, y compris le texte secondaire `#B3A7AE` et le laiton.
- Responsive : navigation repliée sous 620px, plateau en deux colonnes sous 940px puis en
  une seule sous 620px.
- Le hero doit tenir dans un seul écran : surveiller la taille du titre, il déborde vite.
- Textes en français, apostrophes typographiques, pas d'emoji dans l'interface.
