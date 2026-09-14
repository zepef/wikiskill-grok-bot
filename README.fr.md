# WikiSkill pour Grok Bot
<img width="1984" height="992" alt="image" src="https://github.com/user-attachments/assets/a6afc6df-7eb1-4ad4-9088-a14a0667ad12" />

Adaptation, dans le produit seulement, de [WikiSkill](https://arxiv.org/abs/2608.27454) (Google Research, 27 août 2026).

Pas d'invite de commandes extérieure. Pas de pilote hors Grok Bot. Pas de livret métier.

Grok Bot sait déjà : faire une tâche → enregistrer une procédure → planifier une ronde.

Ce lot ajoute la boucle qui manque :

1. garder les traces des succès **et** des échecs
2. compiler un wiki persistant que les **exécutants n'ont pas le droit de lire**
3. proposer **une** modification de procédure par tour
4. n'adopter la procédure que si la note d'épreuve monte vraiment

Mémoire : Tang et al., *WikiSkill: Compiling Agent Experience into Persistent Knowledge for Skill Evolution*, [arXiv:2608.27454](https://arxiv.org/abs/2608.27454).

Article X (FR) : [docs/article-x/fr.md](docs/article-x/fr.md)  
X Article (US) : [docs/article-x/us.md](docs/article-x/us.md)

## Pourquoi Grok Bot

| WikiSkill (mémoire) | Pièce Grok Bot |
|---|---|
| Agent d'exécution | Tes agents exécutants déjà en place |
| Couche des traces | `/workspace/wikiskill/raw/` |
| Couche wiki | `/workspace/wikiskill/wiki/` + conversation de l'Archiviste |
| Couche des procédures | Procédures Grok Bot, **activées par agent** |
| Tenue du wiki | Agent **Archiviste** + ronde de nuit |
| Proposition | Agent **Proposant** + ronde |
| Sas | Agent **Arbitre** + autorisation humaine |
| Isolement | Activation par agent + règle d'équipe + salon séparé |

Contrainte du produit : tous les agents d'un compte partagent **un** ordinateur distant. Les agents ne sont pas une frontière de sûreté.

## Pupitre

Trois agents nouveaux. Tes exécutants restent tes exécutants.

| Agent | Métier | Procédures actives | Ronde |
|---|---|---|---|
| Tes exécutants | le travail | métier + `wikiskill-log-trace` + `wikiskill-worker-guard` | les tiennes |
| **Archiviste** | traces → wiki | `wikiskill-maintain` | 02:00 |
| **Proposant** | un correctif par tour | `wikiskill-propose` | 02:30 |
| **Arbitre** | sas de note | `wikiskill-gate` | 03:00 |

Salon **la Boucle** = Archiviste + Proposant + Arbitre + toi. Dans les consignes produit, le même salon s'appelle **Loop**.

**Aucun exécutant dans la Boucle.**

## Mise en place (4 collages)

1. Coller `prompts/create-bots.md`
2. Coller `prompts/create-group.md`
3. Envoyer `prompts/init-workspace.md` à l'Archiviste
4. Après un passage d'essai à la main, coller `prompts/create-routines.md`

Puis : **Réglages → Extensions → Les vôtres**, grille de [`TEAM.md`](TEAM.md).

Les consignes collées dans Grok Bot restent en anglais : c'est la langue du produit.

## Licence

MIT. Le mémoire appartient à Google Research / Virginia Tech. Ce dépôt est une adaptation indépendante. Ce n'est ni un produit xAI ni un produit Google.

Lab X : https://le-lab-x.com/fr
