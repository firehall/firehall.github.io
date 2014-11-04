---
layout: post_page
title: Base de travail pour développer un site avec CmsMadeSimple

published: true
---

Je développe des sites avec CmsMadeSimple (CMSMS) depuis plus de 5 ans maintenant et j'avoue que c'est un CMS que j'apprécie particulièrement, que ce soit pour sa très grande souplesse, sa prise en main intuitive et son respect des standards (web et accessibilité).  
Dans cet article, je présente sans prétention la manière dont j'installe et utilise ce CMS.

###Installation

1. Je récupère la dernière version du CMS (et sa traduction FR) sur [le site officiel français](http://www.cmsmadesimple.fr/telecharger-cms).

2. Je dézippe les archives et les fusionne pour obtenir une version complète du cms (EN + FR).

3. Je transfert l'ensemble des fichiers sur le ftp et modifie les droits sur les dossiers suivants (777 _ou 755 pour OVH_) : 

* tmp/templates_c
* tmp/cache
* uploads
* uploads/images
* modules

4. Suivant l'hébergeur (pour des serveurs mutualisés) j'active une version récente de php5 (ex: chez ovh on créait un fichier .htaccess `SetEnv PHP_VER 5` (php5.2), `SetEnv PHP_VER 5_3` (php5.3) etc.)

4. Je créé un fichier (vide) "config.php" que je place à la racine de mon site.

5. Je lance l'install : http://url-du-site/install, je suis toutes les étapes (prévoir une bdd sql5).

6. Je supprime (ou renomme) le dossier "install".

7. Je complète éventuellement le site avec mes propres dossiers (img, js etc...) :

* css
* fonts
* img
* js

_Le CMS possède bien entendu sa propre gestion des CSS (performante!), mais j'ai tendance à plutôt utiliser une feuille de style externe, issue d'une première intégration (html-css-js) d'après les maquettes du projet..._

###Gabarits

Les balises Smarty utiles (voir indispensables) (dans l'ordre) :

####Balises de métadonnées (entre <head> et </head>):
    
On place cette balise en tout début de fichier, on évite tout espace ou saut de ligne avant celle-ci) : 

    {process_pagedata}
    
Titre de la page | nom du site (défini durant l'install et modifiable via l'admin) :

    <title>{title} | {sitename}</title>

Métadonnées :  

    {metadata}

Les feuilles de styles (css) :  

    {cms_stylesheet}
    


####Balises de métadonnées (entre <body> et </body>):

La balise qui affiche le menu (on peut choisir le template, les modifier ou en ajouter directement via ftp : "modules/MenuManager/templates/nom_template.tpl" :  

    {menu template='cssmenu.tpl'}
    
N'afficher que le premier niveau du menu (parents) :

    {menu template='cssmenu.tpl' collapse="1"}
    
N'afficher que le niveau 2 :  

    {menu template='cssmenu.tpl' childrenof="alias-de-la-page"}
    
Le titre de la page en cours :

    {title}
    
Le fil d'arianne (breadcrumbs) :  
    
    {breadcrumbs delimiter=">"}

Le contenu principal de la page :  

    {content}
    


####Gabarits plus complexes (plusieurs zones de saisie):

De base, dans l'édition d'une page on peut saisir le titre de la page, le nom qui sera utilisé pour le menu, et le contenu.  
Mais on peut aller plus loin et faciliter la saisie de l'utilisateur final sans qu'il risque (ou presque) de ruiner la mise en page de son site.  
Pour ce faire, on peut définir plusieurs zones de saisies. Celà se fait en deux temps : on initilalise les zones de contenues puis on les appelle dans le gabarit.

**L'initialisation se fait en tout début de document, tout de suite après `{process_pagedata}`** :  

    {content assign='monbloc' label="Mon bloc" tab="nom de l'onglet" wysiwyg=true oneline=true}
    
_**assign** : Le nom du bloc, tel qu'on va l'appeler plus loin dans le gabarit._  
_**label** : Le nom du bloc dans la page d'admin_  
_**tab** : l'onglet dans lequel apparaitra le bloc dans l'admin_  
_**wysiwyg** : activer le wysiwyg ou non (valeurs: true ou false)_  
_**oneline** : champ input, ou zone de texte (textarea - par défaut) dans l'admin (valeurs: true ou false).

Comme évoqué, on peut ajouter autant de zones de textes que l'on veut, mais il en faut au moins une (qui prendra la forme que nous venons de voir, et qui sera obligatoire (sans quoi on ne pourra pas valider la page).

Ajouter une seconde zone de saisie :  

    {content block=nom du bloc assign='monbloc' label="Mon bloc" tab="nom de l'onglet" wysiwyg=true oneline=true}
    
_**block** : Définit qu'il s'agit d'un bloc de contenu secondaire_

On peut ensuite "appeler" les blocs dans la partie contenu du gabarit (<body></body>) :

    {$nom_du_block1}
    (...)
    {$nom_du_block2}
    (...)

####Autres balises utiles:

**Liens pages internes** :  

    {cms_selflink page="alias-de-la-page" text="nom du lien" class="class-css"}
    
ou :  

    <a href="{cms_selflink href="alias-de-la-page"}>Nom du lien</a>

**Ancres** :

    {anchor anchor='id de l'élément' text='texte à afficher'}
    
**Plan du site** :

    {site_mapper show_all="1" excludeprefix="recherche"}
    
_**show_all="1"** => montre les pages non actives dans le menu_  
_**excludeprefixe="aliaspage"** => n'affiche pas les pages dont l'alias est précisé (ex: resultat du module de recherche)._ 

**Activer le debug (afficher les variables des templates dans une modale) :**

    {debug}

**Blocs de Contenus Globaux (BCG)** :

    {global_content name='nom'}
    
_Les BCG sont très utiles, notament pour fractionner des sites qui ont plusieurs gabarits, je les utilise notament pour isoler header et footer, qui sont identiques peu importe le gabarit (la mise à jour est ainsi simplifiée, puisqu'elle ne se fait qu'une fois, à la manière de ce que fait un include en php...)_


**Formulaire de recherche :**

    {search searchtext="rechercher..." lang="fr_FR" resultpage="recherche" search_method="post"}

    
####Optimiser le CMS :

**Url rewrite:**

1. Editer config.php

    `$config['url_rewriting'] = 'mod_rewrite';`
     
2. sur le ftp : télécharger doc/htaccess.txt
Le placer à la racine du site et le renommer : .htaccess

**Permettre l'envoi de mail :**

Admin > Extensions > Cmsmailer
Méthode d'envoi des mails : mail (_= méthode mail de php_).

**Afficher du Javascript dans un gabarit :**

	{literal}	
        //ICI LE JAVASCRIPT
	{/literal}

####Astuces de grand-mère ;) 

**Affichage conditionnel**

__Exemple :__ indiquer dans le gabarit de n'afficher une info que si on est sur une page donnée :

Dans l'édition d'une page, aller au champ "Balises Smarty spécifiques pour cette page :" et ajouter :

    {assign var="contentpage" value="valeur"}
    
Puis dans le gabarit (ou dans la page), on met en place la condition :

    {if $contentpage=="valeur"}
        //contenu à afficher que pour la page en question		
    {/if}

**Limiter le nombre de caractères à afficher (balise smarty)**

Un exemple avec le module de news, on affiche que les 300 premiers caractères du sommaire (code inséré dans une gabarit de sommaire d'article):

    {eval var=$entry->summary|truncate:300:" (...)"}
    
**Affichage aléatoire (randomize) (exemple avec des photos)**

1. Créer un dossier sur le ftp ex: uploads/random
		
2. Renommer les photos en "image1.jpg" => "imagen.jpg" et les ajouter dans le dossier (ftp).
		
3. Dans le gabarit :
		
        <img src="uploads/images/random/image{1|rand:n}.jpg" alt="galerie photo" width="185"/>   

    
