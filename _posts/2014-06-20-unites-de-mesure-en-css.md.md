---
layout: post_page
title: Les unités de mesure en CSS

categories: css
tags:
- css
- tutoriel
published: false
---



### Intro

px + em + rem + %
em = ?
rem = ?

### Px et Em

On sait que (approximativement) 1em = 16px.

Commencons donc doucement, en créant deux div. La première ".unite-px" contiendra des textes exprimés en pixels; la seconde ".unite-em", contiendra des textes exprimés en em.
Dans chacune de ces divs nous allons insérer: 
- trois balises titre : h1, h2 et h3, avec respectivement : 24px, 20px et 18px (soit: 1.7143em, 1.4286em et 1.2857em)
- une balise paragraphe : 16px (soit: 1em)
- une balise span : 12px (soit : 0.8571em).
- En css on définit également la taille standard de la div .unite-px : 16px et .unite-em : 1em.

Remarque: pour convertir facilement des px en em, je ne saurais que trop conseiller ce lien : http://soqr.fr/vertical-rhythm/ (mais nous en reparlerons).

Voir le résultat step 01: http://firehall.fr/blog/2014-06/unites-de-mesure/step01.html

A ce stade, tout va bien, hormis le fait qu'il faille faire au départ des calculs qui donnent des résultats avec des chiffres après la virgule... ;)

Maintenant, saviez-vous que par défaut la taille de police de body est 16px, ce qui tombe plutôt bien puisque c'est la taille de police que nous avons choisi de définir pour notre div.
Que se passe-t-il maintenant si on reset cette mesure, et qu'on passe par exemple à 14px?

Voir le résultat : step02 http://firehall.fr/blog/2014-06/unites-de-mesure/step02.html

Eh oui, comme A. einstein l'avait prédit, tout est relatif... et ca n'épargne pas les CSS... D'ailleurs dans CSS il y a cascade, autrement dit, il y a un phénomène de réactions en chaine.
Ce qu'il faut retenir avec l'unité EM, c'est qu'elle est relative à ses ancêtres. Il est donc peu interessant (voir carrément à proscrire) de définir une valeur à des éléments du DOM qui ont des ancêtres. Pour être plus exact, il est même primordial d'indiquer cette valeurs aux balises qui se situent à l'origine du DOM: html et/ou body.

############################################
FIN ARTICLE

