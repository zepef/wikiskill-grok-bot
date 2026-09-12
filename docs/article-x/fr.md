# Grok Bot n’apprend rien de ses échecs. WikiSkill corrige cela dans le produit même.

Grok Bot sait déjà transformer une tâche réussie en procédure, puis cette procédure en ronde que l’ordinateur distant rejouera même le portable rabattu. C’est écrit dans la documentation, cela tient, et c’est précisément le chemin que le produit a prévu.

Ce qu’il ne sait pas faire, c’est conserver ce qui a raté, le mettre en ordre, et n’adopter une nouvelle manière de faire que si elle bat la précédente sur un jeu que l’exécutant n’a pas vu.

Le 27 août 2026, Google Research et Virginia Tech ont publié *WikiSkill: Compiling Agent Experience into Persistent Knowledge for Skill Evolution* (arXiv 2608.27454). Ce n’est ni une offre Workspace ni un carnet de notes : c’est une boucle à quatre rôles et trois couches, dont Grok Bot possède déjà les pièces. Le lot qui les assemble se trouve ici :

https://github.com/zepef/wikiskill-grok-bot

## Ce que le mémoire dit vraiment

Les trois couches n’ont pas la même durée de vie, et c’est tout l’intérêt du dispositif.

Les traces brutes enregistrent les appels d’outils, les résultats, les succès et les échecs, puis on n’y touche plus. Le wiki recueille les régularités — cause première, parade, preuves — dans un index, un journal et un registre d’effet, sans aucun retour arrière. Les procédures vivent dans des fichiers SKILL.md, et on les ramène en arrière dès que la note d’épreuve n’augmente pas.

Quatre rôles portent cette séparation. L’exécution fait le travail avec les procédures en vigueur seulement. La tenue du wiki distille les traces en pages. La proposition n’écrit qu’une création ou qu’un correctif par tour. Le sas n’accepte le changement que si la note d’épreuve dépasse la meilleure note tenue.

Les résultats publiés : Gemini-3.5-Flash passe de 49,5 % à 68,1 %, LiveMath de 33 à 72,6, le tableur de 50,5 à 76,6. Si l’exécutant lit le wiki du formateur, la note retombe de 63,7 à 60,9.

## Le pupitre

Tes exécutants gardent leur métier. On ajoute l’Archiviste (2 h), le Proposant (2 h 30) et l’Arbitre (3 h). La Boucle réunit ces trois agents et toi. Aucun exécutant n’y entre.

## Mise en place

https://github.com/zepef/wikiskill-grok-bot

Coller prompts/create-bots.md, puis prompts/create-group.md, envoyer prompts/init-workspace.md à l’Archiviste, puis après un passage d’essai coller prompts/create-routines.md.

Mémoire : https://arxiv.org/abs/2608.27454
