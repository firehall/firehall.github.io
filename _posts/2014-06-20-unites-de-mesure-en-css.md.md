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

Bien que Jekyll ne soit pas un CMS, il profite également d'un certain nombres d'automatisations qui facilitent l'ajout et la mise à jour des contenus.

Analysons ce qu'il se passer lorsqu'on créer un nouveau site Jekyll :
{% highlight ruby %}
jekyll new mon-blog
{% endhighlight %}
Cette action va créer un nouveau dossier <em>"mon-blog"</em> <strong>contenant les fichiers et dossiers de base:</strong>
{% highlight ruby %}
_includes
_layouts
_posts
_site
_config.yml
index.html
{% endhighlight %}
Il est bien entendu <strong>primordial de respecter la convention de nommage</strong>, à savoir que les dossiers et le fichier de configuration du site commencent invariablement par `_`

`_includes`<br/>
Ce dossier contiendra les fichiers communs à l'ensemble du site, peu importe le gabarit : comme le header, le footer, une sidebar etc...

`_layouts`<br/>
Les différents gabarits de page (ex: une colonne, deux colonnes etc...).

`_posts`<br/>
Les articles (dans le cadre d'un fonctionnement de type blog).

`_site`<br/>
On y trouvera (entre autre) les pages statiques du site.

`_config.yml`<br/>
Le fichier de configuration de notre site. C'est un des fichiers les plus importants, qui se rapproche d'un fichier de type "config.php" pour un site en php.

`index.html`<br/>
La page d'index (accueil)


### Publier un nouvel article

Dans l'arborescence aller dans `_posts`  
Créer un nouveau fichier structuré de cette manière :

     année-mois-jour-tire-du-post.md
	
_Exemple: 2014-05-31-mon-permier-post.md_


La page doit commencer par ( au minimum) les métadonnées suivantes:
	
	---
	layout: post_page
	title: Mon premier post
	---

On définit donc le gabarit à utiliser (layout) et le titre du post.

On pourrait ajouter d'autres métadonnées : 

    ---
    categories: jekyll
    tags:
    - Jekyll
    - tutoriel
    published: true
    ---

Ici on a ajouté une catégorie, des tags et définit que l'article est publié _(pour en faire un draft, il suffit de modifier true par false)_.

####Format de la date

Par défaut la date s'affiche en anglais. Pour l'afficher dans une autre langue, il va falloir la customiser :

Dans `_layout\post_page.html` (valable pour le thème de base), on va donc définir la date comme on le souhaite (dans mon cas : jj mois année): 

<pre>
\{\% assign m = page.date | date: "%-m" \%\}
\{\{ page.date | date: "%-d" \}\}
\{\% case m \%\}
    \{\% when '1' \%\}Janvier
    \{\% when '2' \%\}F&eacute;vrier
    \{\% when '3' \%\}Mars
    \{\% when '4' \%\}Avril
    \{\% when '5' \%\}Mai
    \{\% when '6' \%\}Juin
    \{\% when '7' \%\}Juillet
    \{\% when '8' \%\}Ao&ucirc;t
    \{\% when '9' \%\}Septembre
    \{\% when '10' \%\}Octobre
    \{\% when '11' \%\}Novembre
    \{\% when '12' \%\}D&eacute;cembre
\{\% endcase \%\}
\{\{ page.date | date: "%Y" \}\}
</pre>


###Quelques exemples de formatage en markdown :

#### Italique (balises : `<em></em>`)

    *texte en italique méthode 1*
    _texte en titalique méthode 2_

donnent:  
*texte en italique méthode 1*  
_texte en titalique méthode 2_

#### Gras (balises : `<strong></strong>`)

    **texte en bold méthode 1**
    __Texte en bold méthode 2__

donnent:  
**texte en bold méthode 1**  
__Texte en bold méthode 2__

#### Titres (balises : `<h1></h1>, <h2></h2>...<hn></hn>`)

    # Titre1
    ## Titre2
    ### Titre3
    #### Titre4

#### Paragraphe (balises : `<p></p>`)

    Ceci est un premier paragraphe, il faut sauter une ligne avant et après le texte.

    Ceci est un second paragraphe.

#### Retour à la ligne (balises : `<br/>`)
  
    Ceci est la première phrase d'un paragraphe.  
    Ce retour à la ligne est réalisé en terminant la phrase précédente par deux espaces.

#### Un lien (balises `<a></a>`)

    [lien vers google] (http://www.google.fr "lien vers google (balise title)")

donne :  
[lien vers google](http://www.google.fr "lien vers google (balise title)")

#### Insérer une image (balise `<img/>`)

    ![texte alternatif pour les liseuses par exemple, important pour l'accessibilité!](/img/fh-icon.png "texte pour le titre (balise title (survol de la souris")

![texte alternatif pour les liseuses par exemple, important pour l'accessibilité!](/img/fh-icon.png "texte pour le titre (balise title (survol de la souris")

#### Liste non-ordonnée (balises : `<ul><li></li></ul>`)

    * un élément de liste
    * un deuxième
        * sous-élément

donnent :

* un élément de liste
* un deuxième
    * sous-élément

 ___Rque:__ il est important de sauter une ligne avant le premier élément de liste_

#### Liste ordonnée (balises : `<ol><li></li></ol>`)

    1. un élément de liste
    2. un deuxième

donnent :

1. un élément de liste
2. un deuxième

 ___Rque:__ il est important de sauter une ligne avant le premier élément de liste_

#### Citation (balises : `<blockquote></blockquote>`)

    > Citation dans un élément blockquote

donne : 

> Citation dans un élément blockquote

 ___Rque:__ il est important de sauter une ligne avant le code

#### Paragraphe de code (balises : `<pre></pre>`)
    
    Ce pragraphe de code s'obtient en commencant par 4 espaces.
    Un simple retour à la ligne permet de créer une seconde ligne de code.

 __Rque:__ il est important de sauter une ligne avant le code

#### Balise code `<code></code>`

    `<p></p>`

donne :  
`<p></p>`

 __Rque:__ Sur un clavier windows ` s'obtient en maintenant `Alt Gr` + `7`

#### Les limites de MarkDown...

 Comme on peut le constater, écrire un article pour Jekyll dans un éditeur de texte devient rapidement intuitif et se révèle très productif en terme de temps (pour un développeur, celà peut se révéler même plus rapide que de passer par un éditeur WYSIWYG).

 Pour autant, tout n'est pas parfait. Prenons l'exemple de l'insertion d'une image:  
 Que se passe-t-il si j'avais voulu manipuler la largeur du logo ou ajouter une _class_ à ma balise `<img>`?  
 A priori il existe des solutions (comme [ici](http://stackoverflow.com/questions/14675913/how-to-change-image-size-markdown) ou [là](https://github.com/jeromyanglim/rmarkdown-rmeetup-2012/issues/4)), mais elles semblent dépendre de nombreux facteurs (OS, versions de Ruby, gem de markdown installés... Voir tout ca imbriqué!)  
 Dans ce cas, le plus simple est peut-être encore de passer par ce bon vieux langage html, qui -suprise!- est parfaitement interprété :

     <img src="/img/fh-icon.png" width="100" class="toto"/>

 <img src="/img/fh-icon.png" width="100" class="toto"/>  
 Ce qui produit l'affichage du logo avec une largeur contrainte à 100px et une _class toto_ (qui n'existe pas pour le coup ;) )  
 On peut évidement en faire de même avec n'importe quelle balise html.

 On peut ainsi conclure que si le langage Markdown a ses limites, elles ne sont finalement pas bloquantes étant donné sa grande souplesse d'utilisation qui permet de _mixer_ markdown et html.

### Installer un thème

 Pour aller plus loin avec l'utilisation de Jekyll, on peut bien évidement se créer son propre thème de A à Z.  
 On peut aussi plus simplement en récupérer un et l'installer pour l'utiliser tel quel ou le customiser ([Voici par exemple un site ou l'on peut télécharger différents thèmes](http://jekyllthemes.org/))

Pour installer un nouveau thème, il va falloir installer la Gem Bundler.  

Avec la console Ruby, on se rend dans le dossier d'installation du site Jekyll :

    cd c:\vers\dossier

... Pour y exécuter l'installation de la gem Bundler :  

    gem install bundler

Il ne reste plus qu'à dézipper le thème dans le dossier du site et lancer Jekyll :

	jekyll serve

### Sources :

Markdown
[http://fr.wikipedia.org/wiki/Markdown](http://fr.wikipedia.org/wiki/Markdown)

Formatage de dates avec liquid :
[http://alanwsmith.com/jekyll-liquid-date-formatting-examples](http://alanwsmith.com/jekyll-liquid-date-formatting-examples)