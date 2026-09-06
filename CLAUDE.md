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

## Direction artistique — la cascade tient la page

**Cette direction remplace les précédentes** (claire et zen ; puis écrin aubergine sur fond
plat). Demandée explicitement par la cliente : elle veut un fond cinématique, une eau qui
descend en continu, et que **le fond domine le contenu** — « limite qu'on voit plus
l'arrière-image que l'image tout court ». Les versions antérieures restent dans l'historique
git et sur `claude/website-design-creation-yodgt1`.

- **Le fond est le site.** Un canvas WebGL fixe, en `position: fixed` sur tout le viewport,
  derrière l'intégralité de la page. Ce n'est pas un décor de hero : l'eau continue de
  descendre derrière la collection, le savoir-faire et le contact.
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

## La cascade : ce qui la fait lire comme de l'eau

Une première version avait été rejetée — « on dirait que c'est peint par un peintre ».
Le défaut n'était pas le manque de détail mais la **forme du bruit**. Trois principes, à ne
pas défaire :

1. **Bruit *ridged*** (`1 - |2n-1|`) et non un fbm ordinaire. Un fbm étiré donne des bandes
   molles ; le ridged donne des crêtes nettes, qui est la forme d'une lame d'eau qui se
   déchire.
2. **Forte anisotropie.** Une cellule de bruit doit être une vingtaine de fois plus haute
   que large (`sx` ≈ 13–40 contre `sy` ≈ 1–2,5). C'est le rapport `sx/sy` qui fait la chute.
   Des cellules presque carrées donnent de la fumée marbrée, pas une cascade.
3. **Une lumière.** L'eau ne se reconnaît pas à sa texture mais à ses reflets : lumière
   chaude rasante venue de la droite, éclats spéculaires calculés en puissance sur les
   crêtes, et côté gauche laissé dans l'ombre. Cette ombre à gauche **est** ce qui porte le
   texte du hero — c'est l'éclairage de la scène, pas un voile posé dessus.

S'y ajoutent trois nappes à des vitesses différentes (le glissement entre elles donne
l'épaisseur du rideau) et une enveloppe lente sur `x` pour que certaines colonnes portent
plus d'eau que d'autres.

**Garde-fous obligatoires** : demi-résolution, 3 octaves, 30 images/seconde, arrêt quand
l'onglet passe en arrière-plan, et **repli en deux temps** — d'abord la résolution baisse,
et seulement si cela ne suffit pas l'image se fige. Une eau immobile derrière tout un site
se voit beaucoup plus qu'une eau un peu moins fine. En `prefers-reduced-motion`, une seule
image est peinte puis plus rien. Sans WebGL, le dégradé CSS du canvas prend le relais.

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
lit comme un coffret ouvert au-dessus de la chute.

## Animation

L'eau ne s'arrête jamais : c'est le fond, pas un effet. **La seule animation d'interface**
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

Le hero ne montre plus d'illustration : il est tenu par l'eau et le titre seuls. Les quatre
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
