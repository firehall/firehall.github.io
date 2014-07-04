---
layout: post_page
title: Kit de survie de l'intégrateur Prestashop 1.6

categories: prestashop integration
tags:
- prestashop
- tutoriel
published: true
---



Cet article ne concerne que le layout de Prestashop, à savoir le header, le footer et la fenêtre principale. Le contenu à proprement parler (les produits, les catégories, les modules) nécessiteraient chacun des pages entières de tuto...

### Les fichiers tpl du thème

*__Remarque :__ nous ferons ici systématiquement référence aux fichiers .tpl du thème de base.*

#### 01. header.tpl
En résumé, il comprend le __début de la structure__ (html, head, metadonnées, styles, appel aux js etc..., body) jusqu'à la __div#center_column__.  
Les éléments placées dans cette dernière balise constituent le coeur même des informations.
On notera de nombreuses conditions smarty (matérialisées par les balises {if...}[conditions]{/if}), parmis lesquelles des conditions d'affichage qui peuvent modifier complètement la mise en page : __affichage ou non d'une colonne gauche et affichage ou non d'une colonne droite__.  
Ces informations sont dans un premier temps conditionnées par des class de la balise body(l.64) :

    {if $hide_left_column} hide-left-column{/if}{if $hide_right_column} hide-right-column{/if} 
    
Puis plus loin, on trouve la condition d'affichage de la colonne gauche (left_column) (l.111) :  

    {if isset($left_column_size) && !empty($left_column_size)}
      <div id="left_column" class="column col-xs-12 col-sm-{$left_column_size|intval}">
        {$HOOK_LEFT_COLUMN}
      </div>
    {/if}.

#### 02. footer.tpl
Dans ce template on va bien entendu trouver les infos relatives au footer et la fermeture des balises body et html, mais aussi les conditions d'affichage de la colonne droite (right_column) (l.28) :

    {if isset($right_column_size) && !empty($right_column_size)}
      <div id="right_column" class="col-xs-12 col-sm-{$right_column_size|intval} column">
         {$HOOK_RIGHT_COLUMN}
      </div>
    {/if}


### Les hooks

*ci-dessous, la page d'accueil de Prestashop 1.6 : Les couleurs de fonds représentent les hooks, les numéros les différents modules qui les constituent*  

![Les hooks du theme standard de prestashop 1.6](/img/prestashop16-home-hooks.jpg)

#### Les hooks du header

#### displayBanner

Il correspond à la bannière de pub en haut de page :  
- Matérialisé dans header.tpl (l.77)  
- Module concerné :  
__01 - Bloc bannière :__  
La bannière de pub qu'on trouve en haut de page  

#### displayNav

Il correspond aux éléments de navigations de la partie haute du header.  
- Matérialisé dans header.tpl (l.84)  
- Modules concernés :  
__02 - Bloc informations clients :__    
*Dans les faits il correspond au compte client (connexion, édition de compte et déconnexion, lorsqu'un utisateur est connecté).*  
Bloc devises :  
*Un bloc présentant les différentes devises de paiement acceptées (pas visible par défaut, il faut activer les devises).*  
Bloc langues :  
*Un bloc avec les drapeaux des différentes langues, lorsque le multilingue est activé (ce qui n'est pas le cas par défaut).*  
__03 - Bloc contact :__  
*Concrètement, ce module affiche le numéro de téléphone et le lien contactez-nous.*  
    
#### displayTop

Matérialisé dans header.tpl (l.96) {if isset($HOOK_TOP)}{$HOOK_TOP}{/if}  
Modules concernés :  
__04 - Bloc recherche rapide :__  
*Le moteur de recherche*  
__05 - Bloc panier :__    
*Le bouton panier*  
__06 - Menu haut horizontal :__  
*Le menu principal*  
Bloc informations clients :   
*Dans les faits il correspond au compte client (connexion, édition de compte et déconnexion, lorsqu'un utisateur est connecté).*  
Pages introuvables  
Mots clés  
*Gestion Backend.*  
Bloc liste de cadeaux :    
*Module désactivé par défaut.*
    
#### displayTopColumn

Matérialisé dans header.tpl (l.108)  
Modules concernés :  
__07 - Diaporama (image slider) pour votre page d'accueil :__   
*Le slider en homepage*  
__08 - Configurateur de thèmes :__   
*Module qui permet de gérer certains éléments du thème (notament le petit bouton pour modifier les couleurs du thème), mais aussi les images de produits à droite du slider en homepage.*


#### displayLeftColumn

Ce hook n'est pas pris en compte sur la homepage. Pour l'essentiel il est utilisé pour les pages de type "catégorie" et "produit".  
- Matérialisé dans header.tpl (l.112)  
- Modules concernés :  
Bloc meilleures ventes  
Bloc catégories  
Bloc navigation à facettes  
Bloc CMS  
Bloc fabricants  
Bloc mon compte  
Bloc nouveaux produits  
Bloc des logos de paiement  
Bloc promotions  
Bloc magasins  
Bloc fournisseurs  
Bloc mots-clés  
Bloc des derniers produits vus  
Configurateur de thème  

#### Les hooks du footer

#### displayRightColumn

Matérialisé dans footer.tpl (l.28)  
Module concerné :   
Par défaut, aucun module n'est accroché à ce hook.  

#### displayFooter

Matérialisé dans footer.tpl (l.37)  
Modules concernés :   
__09 - Bloc newsletter__  
*Inscription à la lettre d'informations*  
__10 - Bloc social__  
*Réseaux sociaux*  
__11 - Bloc catégories__  
*Afficher les catégories*  
__12 - Bloc CMS__  
*Liens vers les pages CMS*  
__13 - Bloc Mon compte dans le pied de page__  
*Liens vers les pages relatives au compte client*  
__14 - Bloc informations de contact__  
*Coordonnées complètes*  
Récupération des données statistiques  
*Invisible en front-end, permet de gérer les stats du site*  
Configurateur de thèmes.
