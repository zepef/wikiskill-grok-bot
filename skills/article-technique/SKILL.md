---
name: article-technique
description: Redige un article technique long (FR, puis EN sur demande) avec intertitres de regime, sources, bandeau de serie et plusieurs dessins techniques. Tout est produit par Grok. La procedure vit en local et se met a jour sur le disque. Declencheurs article, article long, article technique, article X, intertitres, dessins techniques, version US, publication le-lab-x. Pas un fil X ni une alerte.
metadata:
  type: workflow
  version: "1.1"
---

# Article technique

## Residence locale

Tout est genere par Grok (plan, texte, consignes d'images, evolutions de cette procedure). Rien ne reste seulement dans une conversation.

Source de verite : le depot git zepef/wikiskill-grok-bot, dossier skills/article-technique/.

Copie de travail Grok, a realigner sur le depot :

`/home/workdir/.grok/skills/article-technique/`

Regle : on edite dans le depot local, on pousse vers origin. On n'applique pas une version orale.

## When to use

Article long, article technique, article X, intertitres, dessins techniques, version US, publication le-lab-x. Niches : Grok Bot, agents, usines autonomes, WikiSkill, comptabilite francaise, intelligence artificielle chez soi.

Si la demande est un fil, un billet ou une alerte, basculer vers thread-pipeline.

## Inputs

- Sujet ou these
- Sources deja en main (papier, depot, doc produit)
- Charte partagee
- `references/canevas.md` et `references/illustrations.md` du dossier local

## Role

Produire un article de fond, lisible et eprouve. Le bandeau identifie la serie. Les dessins techniques portent la lecture. Feu vert humain avant toute mise en ligne.

## Charte (texte public)

- Francais d'usage. Pas d'anglais de convenance (on dit procedure, ronde, branchement, essaim, pupitre). Produits conserves : Grok Bot, WikiSkill, X, YouTube, TikTok.
- Aucun tiret cadratin. On coupe, on met deux-points ou une parenthese.
- Guillemets francais « ... ».
- On vire le lexique de machine : crucial, essentiel, notamment a repetition, par ailleurs, il convient de noter, dans le paysage, a l'ere de.
- On n'abaisse pas le registre.
- On n'invente pas un labo, un chiffre, une date ou une attribution. Source au plus pres du fait.
- Citation systematique de https://le-lab-x.com/fr en pied d'article FR (https://le-lab-x.com en EN), autorisation Lab X.

## Sequence

### Phase 0. Plan avant texte

Ne pas rediger le corps tant que le plan n'est pas pose.

1. Angle en une phrase (these, pas titre d'agence).
2. Lecteur vise et geste qu'il pourra faire lundi.
3. Liste d'intertitres (5 a 9). Chaque intertitre change de regime.
4. Plan d'illustrations : 1 bandeau + 1 dessin technique par intertitre utile. Un bandeau seul est refuse.
5. Sources en main. Trous a verifier avant d'ecrire.

Presenter le plan. Attendre un feu vert court, sauf ordre d'ecrire tout de suite.

### Phase 1. Article FR + consignes d'images

1. Verifier les faits cites.
2. Ecrire l'article selon references/canevas.md.
3. Sous chaque intertitre utile, ligne image + consigne Grok Imagine (dessin technique).
4. Consigne du bandeau, peu ou pas de texte dans l'image.
5. Livrer pour validation. Ne pas publier.

### Phase 2. Apres validation

Declenchee par valide, ok, version US, LinkedIn, Facebook, docx.

- Retouche : modifier seulement la partie visee, ressortir la section entiere.
- Version EN : meme fond, pied le-lab-x sans /fr.
- Teaser reseaux : thread-pipeline, meme fond.
- Fichier article sous artifacts/. Docx seulement si demande.

## How to validate

- Plan d'abord, puis texte.
- Au moins un dessin technique hors bandeau.
- Sources au plus pres des chiffres et dates.
- Charte respectee (pas de tiret cadratin, pas d'anglais de convenance).
- Pied Lab X present.
- Procedure presente sur le disque local aux chemins ci-dessus.

## What to return

Phase 0 : plan (these, intertitres, liste des dessins, sources).
Phase 1 : article FR + bandeau + dessins.
Phase 2 : section retouchee, ou version EN, ou chemin du fichier.

## What needs approval

Mise en ligne. Toute evolution de cette procedure (ecrire dans le depot, pousser, feu vert).

## Illustrations (non negociable)

- Bandeau = serie. Il n'explique rien.
- Corps = plusieurs dessins techniques (flux, pupitre, couches, avant/apres, piece nommee).
- Une image par section utile. Pas de galerie decorative.
- Identifiants fictifs ou floutes.
- Voir references/illustrations.md.

## Anti-patterns

- Article long avec un seul bandeau.
- Introduction / conclusion etiquetees comme telles.
- Procedure seulement racontee, absente du disque.
- Inventer un resultat de papier ou un bouton produit.
- Melanger article et fil X dans le meme livrable.
