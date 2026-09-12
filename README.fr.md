# WikiSkill pour Grok Bot

[English](README.md) · [Article X (FR)](docs/article-x/fr.md) · [X article (US)](docs/article-x/us.md)

Adaptation de [WikiSkill](https://arxiv.org/abs/2608.27454) (Google Research, 27 août 2026) sur les pièces de **Grok Bot** seulement.

Pas d’invite de commandes extérieure. Pas de pilote hors produit. Pas de livret métier.

Grok Bot sait déjà faire une tâche, enregistrer une procédure et planifier une ronde. Ce lot ajoute la boucle qui manque :

1. garder les traces des succès **et** des échecs ;
2. compiler un wiki persistant que **les exécutants ne doivent pas lire** ;
3. proposer **une** modification de procédure par tour ;
4. ne mettre la procédure en service que si la note d’épreuve monte vraiment.

Mémoire : Tang et al., *WikiSkill: Compiling Agent Experience into Persistent Knowledge for Skill Evolution*, arXiv:2608.27454.

## Pourquoi Grok Bot

| WikiSkill (mémoire) | Pièce Grok Bot |
|---|---|
| Agent d’exécution | Tes agents exécutants déjà en place |
| Couche des traces | `/workspace/wikiskill/raw/` (écriture à la suite seulement) |
| Couche wiki | `/workspace/wikiskill/wiki/` + conversation de l’Archiviste |
| Couche des procédures | Procédures Grok Bot, **activées par agent** |
| Tenue du wiki | Agent **Archivist** + ronde de nuit |
| Proposition | Agent **Coach** + ronde |
| Sas | Agent **Referee** + autorisation humaine |
| Isolement | Activation par agent + règle d’équipe + salon séparé |

Contrainte du produit : tous les agents d’un compte partagent **un** ordinateur distant (`/workspace`, connecteurs). Les agents ne sont pas une frontière de sûreté. L’isolement est d’organisation, pas un droit sur les fichiers.

## Pupitre

Trois agents nouveaux. Tes exécutants restent tes exécutants.

| Agent | Métier | Procédures actives | Ronde |
|---|---|---|---|
| Tes exécutants | le travail | procédures de métier + `wikiskill-log-trace` + `wikiskill-worker-guard` | les tiennes |
| **Archivist** | traces → wiki | `wikiskill-maintain` | 02:00 |
| **Coach** | une création ou un correctif par tour | `wikiskill-propose` | 02:30 |
| **Referee** | n’accepter que si la note d’épreuve dépasse la meilleure note tenue | `wikiskill-gate` | 03:00 |

Salon **la Boucle** = Archivist + Coach + Referee + toi.

**Aucun exécutant dans la Boucle.** Ils ne doivent pas voir le wiki s’écrire.

## Mise en place (quatre collages)

1. Coller [`prompts/create-bots.md`](prompts/create-bots.md).
2. Coller [`prompts/create-group.md`](prompts/create-group.md).
3. Envoyer [`prompts/init-workspace.md`](prompts/init-workspace.md) à Archivist.
4. Après **un passage d’essai à la main**, coller [`prompts/create-routines.md`](prompts/create-routines.md) sur chaque agent propriétaire.

Puis : **Réglages → Extensions → Les vôtres** et activer selon la grille de [`TEAM.md`](TEAM.md).

Ne pas lancer les rondes de nuit avant que `/workspace/wikiskill/bench/val` contienne des tâches réservées et un barème. Sans cela, Referee doit s’arrêter.

## Licence

MIT. Le mémoire appartient à Google Research / Virginia Tech. Ce dépôt est une adaptation indépendante de la méthode publiée à Grok Bot. Ce n’est ni un produit xAI ni un produit Google.
