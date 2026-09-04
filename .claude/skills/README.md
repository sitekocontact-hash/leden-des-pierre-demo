# Skills installés dans ce projet

Ces compétences sont chargées automatiquement par Claude Code à chaque session
ouverte sur ce dépôt. Elles ne servent qu'à guider le travail de design — elles ne
modifient rien toutes seules.

| Skill | Origine | Licence | Ce qu'elle apporte |
| --- | --- | --- | --- |
| `impeccable` | [pbakaus/impeccable](https://github.com/pbakaus/impeccable) v4.1.3 | Apache 2.0 | Direction artistique exigeante + 23 commandes (`polish`, `audit`, `critique`, `animate`, `bolder`, `quieter`, `harden`…) et un détecteur d'anti-patterns qui scanne le HTML/CSS produit. |
| `ui-ux-pro-max` | [nextlevelbuilder/ui-ux-pro-max-skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) | MIT | Base de données locale consultable : 79 styles visuels, 192 palettes produit, 74 associations de polices, 119 règles UX, 105 icônes, 17 presets GSAP, 25 types de graphiques, 22 stacks. |

## Comment s'en servir

- Elles se déclenchent d'elles-mêmes quand la demande porte sur du design d'interface.
- Elles peuvent aussi être appelées à la main : `/impeccable polish index.html`,
  `/impeccable audit`, `/impeccable animate`, `/ui-ux-pro-max`.
- `ui-ux-pro-max` se consulte en ligne de commande, par exemple :
  `python3 .claude/skills/ui-ux-pro-max/scripts/search.py --domain style --max-results 3 "nature artisan bijoux"`

## Mise à jour

Ces dossiers sont des copies figées (« vendorisées »), pas des sous-modules Git.
Pour récupérer une version plus récente : recloner le dépôt source et remplacer le
dossier correspondant sous `.claude/skills/`.

## Note pour `impeccable`

La compétence attend idéalement deux fichiers à la racine du projet :

- `PRODUCT.md` — la vérité produit (à écrire avec la cliente via `/impeccable init`)
- `DESIGN.md` — le système visuel en place (générable via `/impeccable document`)

Sans eux, les commandes de raffinement fonctionnent quand même en lisant le code existant.
Le brief de marque vit pour l'instant dans le `CLAUDE.md` à la racine.
