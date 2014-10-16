---
layout: post_page
title: ListIt2 le metamodule de CMSMS

published: false
---

###Installation

ListIt2 (ou ListItExtended), s'installe comme tous les modules CMSMS, depuis l'interface d'administration :  
**Extensions > Gestionnaire de Modules > ListIt2**  

Uhe fois installé, pour l'utiliser il va falloir créer une (ou plusieurs) instance(s):  
**Extensions > ListIt2 > Créer une instance**  

L'instance est dès lors disponible sous la forme **ListIt2nomdumodule** dans : **Contenu > ListIt2nomdumodule**  
Dans l'onglet "options" on peut renommer l'instance pour un nom plus compréhensible, définir le nombre d'éléments à afficher sur une seule page (dans l'admin), définir le préfix d'url ou encore les critères à faire apparaitre dans la liste (utile pour afficher et trier par catégorie).  
_**Rque:** Pour voir le nouveau nom du module, il va falloir vider le cache de cmsms :  
**Administration du site > Maintenance du système > cache et contenu > vider le cache**_

###Créer les champs de son module

On va ensuite créer nos champs, directement dans l'onglet **Définition de champs**.

####Créer et gérer des catégories

1. On choisit en **type de champ : catégories**

2. On donne le nom qu'on veut

3. On choisit pour **alias : category**

4. On se rend ensuite dans **l'onglet : catégories** et on clique sur **Ajouter catégorie**, pour les créer.

On va dès lors pouvoir afficher une catégorie précise de son instance, directement dans le gabarit d'une page de cette manière :

    {ListIt2monmodule category="alias-de-la-category"}
    
Bizarrement, afficher le nom de la catégorie d'un item, dans un gabarit ListIt2 est relativement compliqué.
En effet le code suivant ne va pas afficher le nom de la catégorie, mais plutôt son ID (un chiffre) :
    
    {$item->fielddefs.category.value}
    
Une solution existe, bien qu'un peu biaisée... 
    
    <!-- On sait que l'id de la catégorie "toto" = 1 -->
    {if {$item->fielddefs.category.value} ==1}
        toto
    {/if}
    
####Créer un champ file (image)

01. Type de champ: **File upload**

02. Type de fichiers autorisés : **gif,jpeg,jpg,png**

03. Répertoire : **repertoire1/{$item_id}/repertoire2**  
_Cette technique permet de classer les images par item. Si on ne fait pas ca, on risque à terme d'écraser les fichiers._

Dans le gabarit de notre Instance ListIt2, on va pouvoir appeler notre image de cette manière :

    {if {$item->fielddefs.alias-du-champ.value} !=NULL}
        {capture assign='url'}{root_url}/uploads/repertoire1/{$item->item_id}/repertoire2/{$item->fielddefs.alias-du-champ.value}{/capture}
        {CGSmartImage src=$url filter_croptofit="160,205"}
    {/if} 
    
_Dans cet exemple j'utilise en complément le module **CGSmartImage** qui permet entre autre de recadrer à la volée les images._

####Instancier un champ en particulier

Suivant la maquette et le brief d'un site, on va parfois avoir besoin d'afficher les champs au cas par cas (plutôt que faire une boucle qui va _standardiser_ leur affichage).  
Pour appeler un champ spécifique : 

    {$item->fielddefs.alias-du-champ.value}
    
On pourrait aussi décider d'afficher un bout de code, QUE si le champ est rempli :

    {if {$item->fielddefs.alias-du-champ.value} !=NULL}
        <div>{$item->fielddefs.alias-du-champ.value}</div>
    {/if}
    
###Exemple de gabarit ListIt2

_Cet exemple fonctionne aussi bien pour un gabarit de sommaire, que de détail_

    {if $items|@count > 0}
	   {foreach from=$items item=item}
            {$item->fielddefs.alias-du-champ.value}
            (...)
	   {/foreach}
    {/if}
    

    

