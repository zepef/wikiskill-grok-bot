# Illustrations article technique

## Regle

Un bandeau seul est insuffisant. Article long = plusieurs illustrations, surtout des dessins techniques. Une image par section utile, pas une galerie.

## Bandeau (serie)

- Format 2:1 (depot / article), variante 1280x640 si besoin.
- Identite : mascotte ou objet de serie, mur, affichette ou piece centrale.
- Logos produits seulement s'ils sont deja dans l'identite validee (Grok Bot, WikiSkill).
- Peu ou pas de texte dans l'image. Le titre vit dans l'article.
- Lumiere de cinema, esthétique technique sobre.
- Consigne type :

```
Illustration editoriale nette, format paysage 2:1, [piece centrale],
mur technique sobre, lumiere de cinema, bleus profonds et papier blanc,
haut niveau de detail, aucun texte dans l'image --ar 2:1 --stylize 250
```

## Dessins techniques (corps)

Un dessin par intertitre qui change de regime. Sujets utiles :

- flux (entree, geste, sortie, refus)
- pupitre (roles, salon ferme, executants a l'ecart)
- couches (traces / wiki / procedures) avec durees de vie differentes
- arbre de fichiers (noms lisibles, pas un dump)
- avant / apres d'un incident
- piece nommee (etiquette, brouillon, banc d'essai)

Interdits : photo d'ambiance, open space flou, cerveau lumineux, handshake, stock « IA ».

## Consignes

- Style editorial net ou schema technique, pas peinture.
- Composition lisible a largeur article.
- Identifiants, adresses, objets de boite : fictifs ou floutes.
- Texte dans l'image : seulement une etiquette courte deja validee (nom de role, nom de couche). Sinon aucun texte.
- Meme famille visuelle que le bandeau (lumiere, couleurs, niveau de detail).
- Format paysage, `--ar 16:9` sauf schema carre demande.

Modele :

```
Schema technique editoriale net, [sujet], [metaphore unique],
fond sombre de salle de conduite, lumiere de cinema,
bleus profonds et cyan discret, haut niveau de detail,
aucune marque, aucun texte superflu --ar 16:9 --stylize 250
```

## Production

- Lister les dessins en phase 0. Ne pas les inventer apres coup pour « habiller ».
- Sous chaque intertitre concerne, ligne `image :` + consigne prete a coller.
- Boite reelle interdite dans une capture. Crop serré si on montre un ecran.
- Feu vert sur le texte et sur les images, separement si besoin.
