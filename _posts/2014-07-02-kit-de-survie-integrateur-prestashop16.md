---
layout: post_page
title: Kit de survie de l'intégrateur Prestashop 1.6

categories: prestashop, intégration
tags:
- prestashop
- tutoriel
published: true
---



### Intro

Ce résumé ne concerne que le layout de Prestashop, à savoir le header, le footer et la fenêtre principale. Le contenu à proprement parler (les produits, les catégories, les modules) nécessiteraient chacun des pages entières de tuto...

### Les fichiers tpl du thème

Remarque : nous ferons ici systématiquement référence aux fichiers .tpl du thème de base.

#### 01. header.tpl
En résumé, il comprends le début de la structure (html, head, metadonnées, styles, appel aux js etc..., body) jusqu'à la div #center_column.
Les éléments placées dans cette dernière balise constituent le coeur même des informations.
On notera de nombreuses conditions smarty (matérialisées par les balises {if...}[conditions]{/if}), parmis lesquelles des conditions d'affichage qui peuvent modifier complètement la mise en page :
- Affichage ou non d'une colonne gauche et affichage ou non d'une colonne droite.
Ces informations sont dans un premier temps conditionnées par des class de la balise body :
{if $hide_left_column} hide-left-column{/if}{if $hide_right_column} hide-right-column{/if} (l.64)
Puis plus loin, on trouve la condition d'affichage de la colonne gauche (left_column) :
{if isset($left_column_size) && !empty($left_column_size)}<div id="left_column" class="column col-xs-12 col-sm-{$left_column_size|intval}">{$HOOK_LEFT_COLUMN}</div>{/if} (l.111).

#### 02. footer.tpl
Dans ce template on va bien entendu trouver les infos relatives au footer et la fermeture des balises body et html, mais aussi les conditions d'affichage de la colonne droite (right_column).
{if isset($right_column_size) && !empty($right_column_size)}<div id="right_column" class="col-xs-12 col-sm-{$right_column_size|intval} column">{$HOOK_RIGHT_COLUMN}</div>{/if} (l.28)

### Les hooks

![Les hooks du theme standard de prestashop 1.6](/img/prestashop16-home-hooks.jpg)

#### Les hooks du header

##### displayBanner

Il correspond à la bannière de pub en haut de page : 
- Matérialisé dans header.tpl (l.77)
- Module concerné : 
01 Bloc bannière  - v1.3
Désactiver le module peut suffire "visuellement", en revanche pour faire les choses biens il conviendrait de supprimer de header.tpl  (l.74 à 80):
<div class="banner">
    <div class="container">
        <div class="row">
            {hook h="displayBanner"}
        </div>
    </div>
</div>

##### displayNav

Il correspond aux éléments de navigations de la partie haute du header.
- Matérialisé dans header.tpl (l.84)
- Modules concernés :
02 Bloc informations clients
    Dans les faits il correspond au compte client (connexion, édition de compte et déconnexion, lorsqu'un utisateur est connecté).
Bloc devises
    Un bloc présentant les différentes devises de paiement acceptées (pas visible par défaut, il faut activer les devises).
Bloc langues
    Un bloc avec les drapeaux des différentes langues, lorsque le multilingue est activé (ce qui n'est pas le cas par défaut).
03 Bloc contact
    Concrètement, ce module affiche le numéro de téléphone et le lien contactez-nous.
    
##### displayTop

- Matérialisé dans header.tpl (l.96) {if isset($HOOK_TOP)}{$HOOK_TOP}{/if}
- Modules concernés :
04 Bloc recherche rapide
    Le moteur de recherche
05 Bloc panier
    Le bouton panier
06 Menu haut horizontal
    Le menu principal
Bloc informations clients
    Dans les faits il correspond au compte client (connexion, édition de compte et déconnexion, lorsqu'un utisateur est connecté).
Pages introuvables
Mots clés
    Gestion Backend.
Bloc liste de cadeaux
    Module désactivé par défaut.
    
##### displayTopColumn

- Matérialisé dans header.tpl (l.108) 
- Modules concernés :
07 Diaporama (image slider) pour votre page d'accueil
    Le slide en homepage
08 Configurateur de thèmes
    Module qui permet de gérer certains éléments du thème (notament le petit bouton pour modifier les couleurs du thème), mais aussi les images de produits à droite du slider en homepage.


##### displayLeftColumn

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

##### displayRightColumn

- Matérialisé dans footer.tpl (l.28)
- Module concerné : 
Par défaut, aucun module n'est accroché à ce hook.

##### displayFooter

- Matérialisé dans footer.tpl (l.37)
- Modules concernés : 
09 Bloc newsletter
    Inscription à la lettre d'informations
10 Bloc social
    Réseaux sociaux
11 Bloc catégories
    Afficher les catégories
12 Bloc CMS
    Liens vers les pages CMS
13 Bloc Mon compte dans le pied de page
    Liens vers les pages relatives au compte client
14 Bloc informations de contact
    Coordonnées complètes
Récupération des données statistiques
    Invisible en front-end, permet de gérer les stats du site
Configurateur de thèmes.
