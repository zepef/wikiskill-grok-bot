# WikiSkill Desk — pupitre Grok Bot

Groupe de trois agents spécialisés. Tes exécutants restent tes exécutants.
Ne crée un quatrième agent que si tu n’as pas encore d’exécutant.

Limite du produit : 2 à 6 agents par salon. Ce pupitre en prend 3.

## Pupitre

| Agent | Métier | Procédures à activer | Procédures à refuser | Ronde |
|---|---|---|---|---|
| **Archivist** | Compile les traces en wiki. N’exécute jamais le travail métier. | `wikiskill-maintain` | procédures métier, écriture via connecteurs | 02:00 |
| **Coach** | Propose **un** correctif de procédure par tour. N’écrit pas le wiki. | `wikiskill-propose` | procédures métier, `wikiskill-maintain` | 02:30 |
| **Referee** | Joue le jeu d’épreuve. Accepte ou ramène en arrière. | `wikiskill-gate` | procédures métier d’écriture | 03:00 |
| Tes exécutants | Font le travail. Lisent seulement les procédures en vigueur. | procédures métier + `wikiskill-log-trace` + `wikiskill-worker-guard` | `wikiskill-maintain`, `wikiskill-propose`, `wikiskill-gate` | les tiennes |

## Convention d’accès (ce n’est pas un droit sur les fichiers)

Les exécutants **peuvent** :
- lire les procédures Grok Bot qui leur sont activées
- écrire un fichier dans `/workspace/wikiskill/raw/AAAA-MM-JJ/`
- lire `/workspace/wikiskill/skills/active/` si besoin d’une copie locale

Les exécutants **ne peuvent pas** :
- ouvrir `/workspace/wikiskill/wiki/`
- ouvrir `/workspace/wikiskill/raw/` des autres jours « pour s’en inspirer »
- lire `skill-impact.md`
- enregistrer ou modifier une procédure Grok Bot
- activer une procédure proposée

Archivist **peut** lire raw + wiki, écrire le wiki, jamais toucher aux procédures activées des exécutants.
Coach **peut** lire le wiki + skill-impact + skills/active, écrire skills/proposed/, jamais le raw complet si un résumé Archiviste existe.
Referee **peut** lire skills/proposed + bench, écrire skills/active seulement après sas favorable et autorisation humaine.

## Règle d’équipe à coller (offres Équipes / Entreprise)

```
Isolement WikiSkill
- Les agents exécutants n’ouvrent jamais /workspace/wikiskill/wiki ni skill-impact.md.
- Les agents exécutants n’ajoutent des traces que sous /workspace/wikiskill/raw/.
- Seul Archivist peut modifier /workspace/wikiskill/wiki.
- Seul Coach peut écrire /workspace/wikiskill/skills/proposed.
- Seul Referee peut mettre en service une procédure proposée, et seulement si la note d’épreuve dépasse la meilleure note tenue, plus une autorisation humaine.
- Ne jamais mettre en service une procédure qui autorise l’envoi, l’achat, l’effacement ou l’écriture en production sans approval_required: true.
- Les connecteurs tiennent au compte : les rôles d’agents ne sont pas une frontière de sûreté.
```

## Revue automatique

Exiger une autorisation pour :
- enregistrer / modifier / activer une procédure
- envoyer un message hors du salon dit la Boucle
- écraser un fichier hors `/workspace/wikiskill/raw/` et `/workspace/wikiskill/wiki/`
- toute action d’envoi, d’achat, d’effacement ou d’écriture en service
