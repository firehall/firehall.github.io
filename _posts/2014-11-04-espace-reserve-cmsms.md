---
layout: post_page
title: Un espace réservé sur CmsMadeSimple

published: true
---

CmsMadeSimple ne propose par défaut un système d'espace réservé, il est revanche assez aisé d'en mettre un en place, et qui plus est (comme d'habitude avec ce CMS) le faire coller parfaitement avec les besoins d'un projet.


### 1. Les modules à installer

####FrontEndUsers  (FEU)
Le module qui va permettre de créer du contenu réservé. Il va permettre également la création d'utilisateurs, de groupes et les gabarits de connexion / déconnexion.  
_Dépendance :  CGExtensions_

####CustomContent
Permet d'attribuer différents types de contenus en fonction du public (dans une page: possibilité de sélectionner l'option "contenu réservé").
_Dépendance : FrontEndUsers_

####SelfRegistration
Permet aux utilisateurs de se créer un compte (ou en faire la demande).  
_Dépendance : CGExtension et FrontEndUsers_

### 2. Configurer le module FEU

__Utilisateurs/Groupes > Gestion des utilisateurs du site__

__Onglet: Propriétés de l'utilisateur__  
"Ajouter une propriété."  
Il va falloir créer au minimum deux champs : __e-mail (type : email)__, qui va servir d'identifiant à l'utilisateur final et son champ mot de passe (type: texte - Stocker ces données de manière cryptée dans la base de données: OUI).  

__Onglet: Groupes__  
"Ajouter un groupe."  
On donne un nom au groupe et en second temps on définit parmis les champs créés précédement, s'ils sont obligatoires, optionnels, cachés etc...

__Onglet: Utilisateurs__  
On va pouvoir gérer ici les utilsateurs (appartenance aux groupes, modifications d'infos, suppression et bien sur création).  
"Ajouter un utilisateur"
On va nous demander de remplir les champs créés précédement et l'appartenance à au moins un groupe.  
En cliquant sur suivant, on va nour redemander l'adresse e-mail, puis on revalide.

__Gabarits__  
On peut modifier différents gabarits : __connexion, déconnexion, changement de paramètres, oubli de mot de passe, récupération de l'id etc..__  

### 3. Adapter les gabarits  

Rque: On peut modifier les gabarits pour inclure les conditions (utile si par exemple on veut qu'un seul gabarit soit utilisé pour les gens connectés ou non, avec du contenu spécifique uniquement accessibles aux personnes authentifiées), ou on peut définir qu'un contenu, une page pour être précis, ne soit accessible qu'aux personnes connectées (on édite une page, type de contenu : "Contenu protégé"). A noter que cette dernière action ne permet pas d'affiner la restriction à un groupe en particulier. Pour celà il va faloir mettre des conditions dans les gabarits :

__Contenu visible par un utilisateur connecté :__  

    {if $ccuser->loggedin()}
    **Contenu protégé**
    {/if}
    
__Contenu visible par un utilisateur connecté ET membre du groupe 'user':__  

    {if $ccuser->loggedin() && $ccuser->memberof('user')}
    **Contenu protégé**
    {/if}
    
__Formulaires de connexion :__  
Notre site dispose désormais de contenus accessibles uniquement aux utilisateurs enregistrés. Encore faut-il que ces personnes puissent se connecter!

Dans une __page__, un __gabarit de page__ ou un __"bloc de contenu globaux" (BCG)__ :  

    {FrontEndUsers}
    
__Formulaire de déconnexion :__  

    {FrontEndUsers form="logout"}
    
#### Autres réglages 

__onglet OPTIONS:__  
- afficher dans le menu  
- actif  
- pas cachable  
- pas de recherche dans la page  
- alias: private_nom-de-alias  

_le préfixe "private_" va permettre d'exclure les pages dans un éventuel menu ou plan du site : (excludeprefix="private")_  

__Ne pas afficher la page de connexion quand loggé :__  
a. Créer une page avec le formulaire de connexion :  
    {FrontEndUsers}
			
b. Dans les paramétrages de FEU => quand user connecté rediriger vers une sous-page de la page de connexion.  
			
c. Dans les balises smarty spécifiques à la page de connexion :  
    {if $ccuser->loggedin()}
        {redirect_page page='ma-sous-page'}
    {/if}

###4. Demande de création de compte avec validation manuelle

Il peut arriver qu'on veuille laisser la possibilité à l'internaute de faire une demande de création de compte qui sera ensuite validée (ou non) par l'administrateur du site.

Ceci est parfaitement possible, il va simplement falloir un peu jongler avec le module FEU :

####Création de deux groupes
Nous allons créer deux groupes :  
- __user__ qui contiendra les utilisateurs validés.  
- __temp__ qui contiendra les utilisateurs en attente de validation.  

Par défaut, toutes les demandes d'inscriptions se soldent par une adhésion au groupe "temp" :  
Utilisateurs/Groupes > Gestion des utilisateurs du site > Réglages (en haut à droite)  
__Onglet "authentification intégrée" : Groupe par défaut pour les nouveaux utilisateurs : temp__  
__Onglet "Préférences" : Notifications par email : Lorsqu'un nouvel utilisateur est créé (et juste en-dessous on oublie pas d'entrer l'adresse e-mail qui doit recevoir la notification__  
Groupes autorisés : on met en surbrillance uniquement le groupe user (ainsi les membres du groupe temp n'auront dans les faits accès à rien).

A ce stade, à chaque fois que quelqu'un va s'inscrire : il sera automatiquement inscrit dans le groupe temp et l'administrateur recevra un mail indiquant cette création.  
Une fois les infos du compte validée, il n'y a plus qu'à basculer l'utilisateur dans le groupe définitif : "user" et lui envoyer un email lui confirmant son inscription.




### Sources :
[http://jc.etiemble.free.fr/abc/index.php?page=private2n](http://jc.etiemble.free.fr/abc/index.php?page=private2n)  
[http://jc.etiemble.free.fr/abc/index.php/realisations/trucs-astuces/private2n](http://jc.etiemble.free.fr/abc/index.php/realisations/trucs-astuces/private2n)  
[http://www.cmsmadesimple.fr/forum/viewtopic.php?id=4092](http://www.cmsmadesimple.fr/forum/viewtopic.php?id=4092)