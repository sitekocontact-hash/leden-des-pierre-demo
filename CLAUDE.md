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

## Direction artistique — écrin à bijoux, fond sombre

**Cette direction remplace la précédente** (claire, zen, cascade WebGL, ouverture
cinématographique GSAP). Elle a été demandée explicitement par la cliente. L'ancienne
version reste consultable dans l'historique git et sur la branche
`claude/website-design-creation-yodgt1` — ne pas y revenir sans demande.

- **Ambiance** : l'intérieur d'un écrin. Le fond est le velours, le laiton est la monture,
  les pierres sont la seule vraie couleur de la page.
- **Un seul écran, un seul fichier** : `index.html` contient le HTML, le CSS et le JS.
  Aucun framework, aucune étape de build, aucune dépendance externe hors polices.

### Palette (obligatoire, fixée par la cliente)

| Rôle | Valeur |
| --- | --- |
| Fond principal | `#241F29` (aubergine/charbon) — creux `#1C1821` |
| Panneaux | `#2C2632` |
| Laiton (accent) | `#B98A4D` — clair `#D7AD75` |
| Texte | `#F3EDE3` (ivoire) — secondaire `#B3A7AE` |

### Typographie

- Titres : **Fraunces** (serif chaleureux, axes `SOFT` et `WONK` utilisés)
- Texte courant : **Inter**, graisse légère (300–500)

## Tics de page générée — à ne jamais réintroduire

La cliente a rejeté ces réflexes nommément. Ils sont interdits sur ce projet :

- fond crème + accent terracotta (c'était l'ancienne direction, elle est abandonnée) ;
- cartes identiques à coins arrondis avec la même ombre grise douce, façon SaaS ;
- labels en CAPITALES espacées, eyebrows au-dessus de chaque titre ;
- flèche `→` accolée au texte des boutons et des liens ;
- numérotation `01 / 02 / 03` sur du contenu qui n'est pas une séquence ;
- chaînes de méta jointes par des points médians (`A · B · C`).

**La collection ne se fait pas en cartes.** Elle est un **plateau unique** (`.tray`), divisé
par des filets, comme les logements d'un écrin de bijoutier : les pièces appartiennent
visiblement au même coffret. Ne pas la refactoriser en quatre cartes flottantes.

## Animation

**Une seule animation dans toute la page** : l'ouverture du hero (le texte monte, les
pierres apparaissent), jouée une fois au chargement. Rien d'autre — ni apparition au
défilement, ni effet au survol des pièces. C'est une contrainte de la cliente, pas un
manque.

Elle est en CSS pur, déclenchée par une classe posée en JS. Le principe : le script ajoute
`js` sur `<html>` avant le premier rendu, ce qui seul active l'état de départ. Sans JS, la
règle ne s'applique pas et la page est simplement visible. Rien n'attend un script pour
exister.

`prefers-reduced-motion` annule l'état de départ : tout est visible d'emblée.

## Logo

Le logo original est un cercle doré avec branche d'eucalyptus, cristaux gravés, « L'Eden »
en serif, « des Pierres » en anglaise dorée, puis « Sonia ». Il est **reconstitué en SVG**
dans `index.html` (symboles `#seal-decor` pour la version complète et `#mark-small` pour
l'icône de navigation). Réutiliser ces symboles plutôt que de repartir d'une image bitmap :
ils restent nets à toute taille et se colorent via les variables `--logo-gem`,
`--logo-leaf` et `--logo-leaf-deep`, plus le dégradé `#brass-facet`.

## Illustration des pierres

Le hero n'a pas de photo : quatre pierres facettées en SVG (améthyste, œil-de-tigre, quartz
rose, labradorite), en polygones avec dégradés radiaux. Chaque pierre a une table centrale
plus claire et des facettes latérales assombries ou éclaircies — sans ces facettes, on lit
un polygone plat et non une pierre taillée.

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
- **Seule dépendance externe : Google Fonts** (Fraunces et Inter). Plus de GSAP : une seule
  animation en CSS ne le justifie pas, et cela retire une dépendance CDN.
- Toujours respecter `prefers-reduced-motion`.
- **Le focus clavier doit rester visible partout** : contour laiton plein de 2 px, jamais
  supprimé. Vérifié par parcours au clavier, pas à l'œil.
- **Contrastes** : tout texte doit passer AA sur son fond réel (4,5:1, ou 3:1 au-delà de
  24 px). À vérifier par mesure, y compris le texte secondaire `#B3A7AE` et le laiton.
- Responsive : navigation repliée sous 620px, plateau en deux colonnes sous 940px puis en
  une seule sous 620px.
- Textes en français, apostrophes typographiques, pas d'emoji dans l'interface.
