---
layout: post_page
title: Héberger Jekyll sur github-pages

categories: jekyll
tags:
- Jekyll
- tutoriel
published: true
---

Troisième et dernier article sur la présentation de Jekyll, découvrons aujourd'hui comment l'héberger sur github-pages.  

___Prérequis:__ Avoir installé jekyll en local ([sur windows?](http://blog.firehall.fr/jekyll/2014/05/15/installer-jekyll-sur-windows.html))_  
[Installer NodeJS](http://nodejs.org/download/)  
[Installer Git](http://git-scm.com/downloads) *pour ce dernier, sur windows, on prendra soin de choisir l'option "Run Git form the Windows Command Prompt", dans l'écran concernant l'ajustement des variables d'environnement.*  
[Plus d'infos sur l'installation de NodeJs et GIT sur l'article d'Alsacréations concernant Bower](http://www.alsacreations.com/tuto/lire/1609-bower-pour-les-nuls.html)

### Créer une page Github

Pour héberger son site sur Github, il faut bien entendu commencer par [se créer un compte sur ce dernier](https://github.com/).  
Une fois fait, il faut se connecter et créer un "repository" __qui doit être nommé de la façon suivante :__  
__[nom_du_compte].github.io__ *(dans mon cas : firehall.github.io)*  

Pour les *windowsiens*, on vérifie qu'on a bien les variables d'environnement suivantes (PATH utilisateur) (sinon on les ajoute) :  

    C:\Users\******\AppData\Roaming\npm; C:\Program Files (x86)\Git;
    
### Clone, Add, Commit et Push!

On va cloner sur notre ordinateur le répertoire que l'on vient de créer sur github :  
Pour ce faire, on ouvre la console (de préférence celle de GIT ou de Node) :

    cd c:/[dossier_en_local_pour_cloner]
    git clone https://github.com/firehall/firehall.github.io
    clone http
    
Voilà notre repository est clonée en local.  
Libre à nous maintenant de placer les fichiers de Jekyll dans le dossier "firehall.github.io" (modifiez firehall, par votre compte bien sûr...).

Pour envoyer les modifications en ligne, il ne reste plus qu'à taper les commandes comme suit :

    git add --all
    git commit -m "Mon premier commit"
    git push
    
Dans la première ligne on indique qu'on prend en compte l'ensemble des modifs éffectuées. Ensuite on donne un nom à notre commit et enfin on "push", c'est-à-dire qu'on transfère les fichiers sur les serveurs distants.

### Ca ne marche pas (parce-que je suis sur windows?)

Personnellement j'ai eu quelques difficultés à faire ces manips (suivant le pc, à chaque fois sur un environnement Windows (7 pro, 64bits)), voici quelques petits conseils :  
Si le push ne fonctionne pas, on peut tenter de le forcer :

    git push -f
    
Si votre ordi est sur un environnement réseau sécurisé, il va peut-être falloir configurer la connexion SSH (si vous avez par exemple une erreur du type __error user unknown__).  
Pour ce faire, suivez les instruction de [l'aide de github](https://help.github.com/articles/generating-ssh-keys)  

Il faudra ensuite redéfinir les accès :

    git remote set-url origin git@github.com:firehall/firehall.github.io
    git push
    
On vous demandera ensuite d'entrer la phrase associée à la clé SSH (et votre login/mdp github).

Si rien de tout ca ne marche (ca m'est arrivé ;)), il reste la solution "pour les faibles" ;) : __utiliser l'application github pour windows__.  
Alors ok, ce n'est pas très gratifiant (pas de push en lignes de commandes ;)), mais ca marche parfaitement bien et au final c'est tout ce qui compte, non?  
[Github pour windows](https://windows.github.com/)

### Utiliser son nom de domaine

A ce stade votre Jekyll est en ligne sur github avec une adresse de type : __"firehall.github.io"__
Si vous avez votre propre nom de domaine, vous pouvez tout à fait l'utiliser avec vos pages Github :  
Il suffit de créer un fichier CNAME à la racine du projet (firehall.github.io) avec votre nom de domaine : 

    www.firehall.fr
    
Connectez-vous à l'administration de votre hébergeur pour y renseigner un champ A qui fera pointer votre domaine sur l'IP de github : __204.232.175.78__.  
Il ne reste plus qu'à attendre la propagation des DNS et le tour est joué!

__Edit 07/11/2014__

### Configurer un sous-domaine

Pour configurer un sous-domaine, on créer un fichier CNAME à la racine du projet, avec pour valeur le sous-domaine, dans mon cas :

    blog.firehall.fr
    
On se connecte ensuite à l'administration de l'hébergeur du domaine pour y créer un champ CNAME, qui pointera vers le sous-domaine page-utilisateur, dans mon cas :

    blog 0 IN CNAME firehall.github.io.

    
### D'autres sources et ressources utiles sur le sujet:

[http://martinbuberl.com/blog/setup-jekyll-on-windows-and-host-it-on-github-pages/](http://martinbuberl.com/blog/setup-jekyll-on-windows-and-host-it-on-github-pages/)  
[https://help.github.com/categories/20/articles](https://help.github.com/categories/20/articles)  
[https://help.github.com/articles/creating-pages-with-the-automatic-generator](https://help.github.com/articles/creating-pages-with-the-automatic-generator)  
[https://pages.github.com/](https://pages.github.com/)  
[http://christopheducamp.com/2013/12/21/demarrer-avec-pages-github/](http://christopheducamp.com/2013/12/21/demarrer-avec-pages-github/)  
[http://www.thinkful.com/learn/a-guide-to-using-github-pages/](http://www.thinkful.com/learn/a-guide-to-using-github-pages/)  
[http://nicoespeon.com/fr/2013/04/faire-son-blog-avec-jekyll/](http://nicoespeon.com/fr/2013/04/faire-son-blog-avec-jekyll/)  
[http://hugogiraudel.com/2013/02/21/jekyll/](http://hugogiraudel.com/2013/02/21/jekyll/)