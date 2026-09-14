# Grok Bot n’apprend rien de ses échecs. WikiSkill corrige cela dans le produit même.

Grok Bot sait déjà transformer une tâche réussie en procédure, puis cette procédure en ronde que l’ordinateur distant rejouera même le portable rabattu. C’est écrit dans la documentation, cela tient, et c’est précisément le chemin que le produit a prévu.

Ce qu’il ne sait pas faire, c’est conserver ce qui a raté, le mettre en ordre, et n’adopter une nouvelle manière de faire que si elle bat la précédente sur un jeu que l’exécutant n’a pas vu.

Le 27 août 2026, Google Research et Virginia Tech ont publié *WikiSkill: Compiling Agent Experience into Persistent Knowledge for Skill Evolution* (arXiv 2608.27454). Ce n’est ni une offre Workspace ni un carnet de notes. C’est une boucle à quatre rôles et trois couches, dont Grok Bot possède déjà les pièces. Le lot qui les assemble se trouve ici :

https://github.com/zepef/wikiskill-grok-bot

## Ce que le mémoire dit vraiment

Les trois couches n’ont pas la même durée de vie, et c’est tout l’intérêt du dispositif.

Les traces brutes enregistrent les appels d’outils, les résultats, les succès et les échecs, puis on n’y touche plus. Le wiki recueille les régularités (cause première, parade, preuves) dans un index, un journal et un registre d’effet, sans aucun retour arrière, de sorte qu’un correctif refusé reste écrit pour ne pas être représenté. Les procédures, elles, vivent dans des fichiers SKILL.md, et on les ramène en arrière dès que la note d’épreuve n’augmente pas.

Quatre rôles portent cette séparation. L’exécution fait le travail avec les procédures en vigueur seulement. La tenue du wiki distille les traces en pages. La proposition n’écrit qu’une création ou qu’un correctif par tour. Le sas n’accepte le changement que si la note d’épreuve dépasse la meilleure note tenue.

Les résultats publiés parlent d’eux-mêmes : Gemini-3.5-Flash passe de 49,5 % à 68,1 %, LiveMath de 33 à 72,6, le tableur de 50,5 à 76,6, et un modèle de neuf milliards de paramètres muni de procédures évoluées bat un modèle de vingt-sept milliards qui n’en a pas.

La mesure qui compte pour Grok Bot est plus sévère : si l’agent de production lit le wiki du formateur, la note retombe de 63,7 à 60,9, parce que les traces cessent de montrer les manques de la procédure. Les exécutants ne voient donc que les procédures en vigueur, et le wiki reste privé au couple tenue / proposition.

Un autre chiffre mérite d’être signalé : une procédure née d’un petit modèle a fait chuter un modèle plus grand de 50,5 à 18,1. C’est la raison d’être du registre d’effet, qui consigne tout ce qui a été tenté, accepté ou refusé, et pourquoi.

## Ce que Grok Bot donne déjà

Un agent, dans ce produit, c’est un métier, une mémoire et une conversation. L’ordinateur distant partagé (dossier /workspace, navigateur, invite de commandes) continue de tourner une fois l’écran du portable rabattu.

Une procédure dit la manière, et six champs suffisent à la rendre utile : quand s’en servir, quelles entrées et quels accès, quel enchaînement, comment contrôler le résultat, quel livrable, et ce qui exige une autorisation. Une ronde dit le moment : cinquante au plus par agent, vingt comptes rendus visibles.

L’activation se fait agent par agent, sous Réglages, puis Extensions, puis Les vôtres. Un salon réunit de deux à six agents ; la barre oblique appelle une procédure, le @ appelle un agent. « Enseigner une tâche », en dix minutes au plus, pose la procédure initiale. Les autorisations, la revue automatique, les règles d’équipe et le catalogue interne (offres Équipes et Entreprise) ferment le tableau.

L’ordre officiel ne s’inverse pas : une tâche, puis une procédure stable, puis une ronde. WikiSkill s’insère après la procédure stable ; avant, il n’y a rien à faire évoluer.

## Le trou

L’historique d’une ronde ne garde que vingt passages, ce qui ne constitue pas une couche de traces. « Enregistrer ceci comme procédure » n’est pas un correctif ponctuel versionné, le produit n’offre pas de note d’épreuve native, et aucune cloison par dossier n’empêche tout le monde de voir /workspace.

Les branchements tiennent au compte plutôt qu’à l’agent, et les agents ne forment pas une frontière de sûreté : la documentation le dit sans détour. On n’installe donc pas WikiSkill comme un produit Google ; on réalise l’algorithme avec les pièces déjà présentes.

## Le pupitre : trois agents, un salon, tes exécutants inchangés

Tes exécutants gardent leur métier. On ajoute seulement l’Archiviste, le Proposant et l’Arbitre.

Les exécutants font le travail, avec les procédures du métier, le journal des traces et la garde. L’Archiviste tient le wiki et passe à 2 h. Le Proposant n’écrit qu’un correctif par tour et passe à 2 h 30. L’Arbitre tient le sas et passe à 3 h.

La Boucle réunit l’Archiviste, le Proposant, l’Arbitre et toi. Aucun exécutant n’y entre : s’ils voyaient le wiki se discuter, l’isolement décrit par le mémoire serait rompu. La grille d’activation, sous Extensions puis Les vôtres, est la vraie barrière, pas l’arbre des fichiers.

## Où vivent les trois couches

```
/workspace/wikiskill/
  raw/AAAA-MM-JJ/<agent>-<tâche>.jsonl
  wiki/{index,log,skill-impact,patterns}/
  skills/{active,proposed,archive}/
  bench/{train,val,graders}/
  STATE.md
```

Les procédures en service restent dans le système de procédures de Grok Bot. Le dossier /workspace porte les preuves, le wiki et la quarantaine. Après acceptation et ton feu vert, on passe par la commande native « enregistrer ou mettre à jour la procédure », puis on n’active la procédure que chez les exécutants concernés ; en offre Équipes, on passe par le catalogue interne.

## L’algorithme, dans le produit

Quand l’exécutant termine une tâche, la procédure de journal ajoute une ligne aux traces, sans secret et sans corps de courrier. À 2 h, l’Archiviste lit les traces du jour, écrit les pages du wiki, dépose un résumé dans la Boucle, et ne touche aucune procédure en service. À 2 h 30, le Proposant lit le wiki et le registre d’effet, écrit un seul candidat en quarantaine, dépose l’écart dans la Boucle, et n’active rien. À 3 h, l’Arbitre joue le jeu d’épreuve : si la note reste inférieure ou égale à la meilleure note tenue, le candidat part à l’archive avec une ligne de refus et le service ne change pas ; si la note est supérieure, l’acceptation attend ton feu vert, puis viennent l’enregistrement et l’activation chez les exécutants.

Sans jeu d’épreuve et sans barème, l’Arbitre s’arrête sur la mention « pas de banc d’essai ». Lancer la boucle sans cela, c’est du théâtre. « Enseigner une tâche » pose la procédure initiale ; ce n’est pas l’évolution.

## Un lundi matin dans un essaim Marketing

Prenons une petite équipe qui n’a rien d’extraordinaire : trois exécutants déjà en place, plus le pupitre WikiSkill qu’on vient de décrire. Le Rédacteur écrit les textes. Le Veilleur ramène les sujets, les tournures adverses, les questions qui reviennent. Le Diffuseur prépare la mise en ligne sur X et sur LinkedIn, et il n’envoie jamais sans ton autorisation. Aucun de ces trois-là n’entre dans la Boucle.

Lundi, 11 h 40. Le Rédacteur livre un message de lancement. L’accroche promet « gratuit pour toujours ». L’offre réelle, sur la page, tient quatorze jours. Le Diffuseur, fidèle à la procédure en vigueur, prépare la publication et demande le feu vert. Quelqu’un signe trop vite. Le message part. Le public le lit plus attentivement que la page. Les réponses fusent, le ton bascule, il faut rectifier en public. En fin de tâche, la procédure de journal ajoute une ligne sous `raw/2026-09-14/` : échec, code court `offre-surevaluee`, aucune phrase de message, aucun jeton, aucun nom.

Mardi, autre incident plus banal : une adresse de prévisualisation a glissé dans le corps, et une accroche déjà refusée la semaine d’avant a été rejouée. Deux traces de plus. Toujours rien dans le wiki que les exécutants puissent ouvrir.

À 2 h, l’Archiviste lit seulement les fichiers nouveaux. Il n’écrit pas « faire attention aux offres ». Il écrit une page de motif, ancrée dans les traces nommées : symptôme, cause première, parade qui a tenu, parades déjà rejetées. Le registre d’effet reçoit la même histoire, pour que le Proposant ne représente pas demain le correctif qu’on a déjà écarté. Un résumé court tombe dans la Boucle. Le Rédacteur ne le voit pas.

À 2 h 30, le Proposant n’ouvre pas trois procédures « tant qu’on y est ». Il prend le trou que le wiki documente et que la procédure `lancement-message` ne couvre pas encore, et il écrit un candidat en quarantaine : toute promesse chiffrée ou définitive doit citer la page d’offre avant la demande d’autorisation, et toute accroche déjà portée en refus dans le registre d’effet est interdite. L’écart est déposé dans la Boucle. Rien n’est activé.

À 3 h, l’Arbitre joue huit lancements tenus à l’écart, que les exécutants n’ont pas eus sous les yeux pendant la semaine. Avec la procédure en vigueur, cinq sur huit tiennent. Avec le candidat, sept sur huit tiennent. La note d’épreuve dépasse la meilleure note tenue. L’Arbitre n’enregistre rien tout seul : il pose l’acceptation, les notes, l’écart, et il attend ton autorisation. Toi seul actives la nouvelle procédure, et seulement chez le Diffuseur et le Rédacteur. Le Veilleur n’en a pas besoin. Le Diffuseur, même après cela, n’envoie toujours pas sans autorisation.

Ce que l’exemple change, par rapport à « on va mettre le wiki dans un dossier partagé », tient en trois refus. On ne met pas le Rédacteur dans la Boucle « pour qu’il s’améliore tout seul » : le mémoire a mesuré que l’acteur de production qui lit le wiki du formateur rend les traces plus pauvres, donc la procédure plus fragile. On ne laisse pas le Proposant publier. On ne lance pas les rondes tant que les huit lancements d’épreuve ne sont pas dans `bench/val`, avec un barème : sans ce jeu, l’Arbitre s’arrête, et la semaine n’est qu’un théâtre de comptes rendus.

Le lundi suivant, la même offre trop vaste ne repasse pas la procédure. L’essaim n’a pas « appris la promotion ». Il a cessé de payer deux fois le même mensonge d’accroche.

## Isolement : ce qui tient, ce qui ne tient pas

Cela tient dès que l’on combine l’activation par agent, la Boucle fermée, l’invisibilité des procédures de tenue, de proposition et de sas pour l’exécutant, la règle d’équipe qui interdit aux exécutants de lire le wiki, et la revue automatique qui exige une autorisation pour enregistrer, mettre à jour ou activer une procédure, envoyer, effacer, ou toucher le service.

Cela ne tient pas dès que l’on affirme que les agents sont isolés, qu’un dossier wiki suffira, ou que les vingt comptes rendus d’une ronde tiennent lieu de traces. La vraie cloison, dès que des secrets risquent d’entrer dans les traces, reste un second compte et un second ordinateur, et non un quatrième agent.

## Mise en place : quatre collages, pas d’invite de commandes

Le dépôt est ici :

https://github.com/zepef/wikiskill-grok-bot

On colle d’abord prompts/create-bots.md, puis prompts/create-group.md, on envoie ensuite prompts/init-workspace.md à l’Archiviste, et ce n’est qu’après un passage d’essai à la main que l’on colle prompts/create-routines.md. On termine par la grille de TEAM.md sous Extensions, Les vôtres, et l’on y ajoute la règle d’équipe.

## Travers à éviter

Activer la tenue du wiki sur un exécutant « pour qu’il s’améliore tout seul » est précisément le geste dont le mémoire a mesuré la perte. Mettre un exécutant dans la Boucle, se fier aux vingt comptes rendus, laisser le Proposant activer la procédure, fondre exécutant, archiviste et proposant dans un seul agent, lancer les rondes avant le jeu d’épreuve, ou charger quatre-vingts procédures de métier sur chaque agent « au cas où » : autant de manières de casser la boucle.

## Ce que cela change le lundi

Il ne s’agit pas de faire comme si la machine connaissait déjà tes fichiers : les branchements s’en chargent. Il s’agit d’empêcher l’essaim de payer deux fois la même erreur, et de transformer les règles non écrites en fichiers SKILL.md versionnés, éprouvés, et signés par un humain avant d’entrer en vigueur.

Le mémoire montre aussi que les procédures transmises battent souvent celles qu’un modèle a fait naître tout seul. Faire évoluer sur Grok Bot puis rééprouver ailleurs est donc prévu ; encore faut-il rééprouver, toujours.

Lot sous licence MIT :

https://github.com/zepef/wikiskill-grok-bot

Mémoire :

https://arxiv.org/abs/2608.27454

Documentation des procédures et des rondes :

https://docs.x.ai/grok-bot/skills-routines-and-automations

Retrouvez toutes mes créations numériques et d’intelligence artificielle en source ouverte sur https://le-lab-x.com/fr dès aujourd’hui. Vous pourrez également accéder gratuitement à mon cursus de formation Grok Bot / SpaceXAI Full Stack sur YouTube et TikTok.
