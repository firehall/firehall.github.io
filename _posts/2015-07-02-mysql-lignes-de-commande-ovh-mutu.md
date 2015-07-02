---
layout: post_page
title: MySQL en ligne de commandes (Windows), sur un hébergement OVH Mutualisé
published: true
---

Prérequis:  
_Il faut disposer de l'offre mutualisé PRO au minimum pour pouvoir accéder à mySQL en ligne de commande._

### Télécharger et configurer putty

[ >> Télécharger PUTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)  

_Putty est un programme qui va vous permettre de vous connecter à votre hébergement en SSH._  

Exécutez le logiciel, dans __'Session'__, renseignez l'adresse FTP de votre hébergement dans le champ _'Host Name (or IP address)'_ (laissez le port sur 22), exemple :

    ftp.mondomaine.fr

Validez en cliquant sur le bouton __"open"__.  

La console s'ouvre et vous demande maintenant votre __login FTP__ :  

    login as: [votre_login_ftp]
 
Validez par entrée puis renseignez votre __mot de passe ftp__ :  

    Password : [votre_mot_de_pass_ftp]

Si tout est ok vous aurez un message de confirmation type :  

    Welcome to OVH

### Accéder à MySQL

Toujours dans la console de putty, tapez la commande suivante pour accéder à la base de données de votre choix (celle-ci doit avoir été créé au préalable depuis le manager) :  

    mysql -h [nom_du_serveur] -u [nom_utilisateur] -p[mot_de_passe] [nom_de_la_base]

__Attention a bien respecter les _espaces_ et ne pas mettre les crochets []__  

Exemple :  

    mysql -h mysql01-01.pro -u toto -p1234 toto

    
Et voilà! :)

Vous pouvez tout de suite vérifier si la base contient déjà des tables : 

    SHOW TABLES;

Ce qui affichera l'ensemble des tables. Pour connaitre la structure d'une table en particulier, faites : 

    DESCRIBE nom_de_la_table;

Pour vous déconnecter proprement :

    EXIT

Pour manipuler plus en détails les structures et les données de vos tables, consultez la documentation de MySQL ou le tuto d'Openclassroom :  

[ >> Documentation de MySQL](http://dev.mysql.com/doc/)  

[ >> Tuto MySQL sur le site Openclassroom](https://openclassrooms.com/courses/administrez-vos-bases-de-donnees-avec-mysql)  



