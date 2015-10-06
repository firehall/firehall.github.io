---
layout: post_page
title: Améliorer l'ergonomie du module CGCalendar (CMSMadeSimple)
published: true
---
  
_CGCalendar est un module de __gestion de calendrier__ spécifique au CMS "CmsMadeSimple". On peut l'installer directement depuis le "gestionnaire de modules" de son site CMSMS, ou le [télécharger sur la Forge](http://dev.cmsmadesimple.org/project/files/623)._

CGCalendar est un module très pratique et assez simple à configurer, comme tout bon module CMSMS, on appréciera particulièrement les facilités avec lesquels on va pouvoir modifier ou créer différents types de gabarits, pour coller avec une charte graphique ou le fonctionnement attendu du module.

Je lui trouve malgré tout un défaut assez rebutant, __son ergonomie__.

A l'instar de certains widgets, tel que celui de Google Calendar, c'est à mon sens, un module qui devrait fonctionner en Ajax par défaut, ce qui lui permettrait de ne pas recharger la page à chaque fois qu'on navigue dans le calendrier.  
Pour peu que votre calendrier se trouve en bas-de-page, dès que vous allez utiliser la navigation du module (pour par exemple changer de mois), votre site va se recharger et vous forcer ainsi à "scroller" en bas de page à chaque fois.  
Ca n'en a pas l'air comme ca, mais celà peut pourtant devenir particulièrement irritant...

### Etape 1 : utiliser AJAX pour ne pas rafraichir la page

Cette manipulation va empêcher la page de se rafraichir (seul le calendrier va se recharger, en gardant le curseur au niveau de la page en cours)

Dans le gabarit de page, on ajoute l'appel à Jquery (de préférence, dans <head>, même si celà va à l'encontre des bonnes pratiques, nous y sommes obligé car du JS va s'exécuter également dans le template du module) :

    <script src="http://code.jquery.com/jquery-1.11.1.min.js"></script>

Dans le gabarit du module (un modifié, ou un nouveau...) on va ajouter le script permettant de ne pas recharger l'ensemble de la page :

#### Le Javascript
    <script type='text/javascript'>
    /* <![CDATA[ */
      {literal}
    function ajax_load(url,dest)
    {  
     var tmp = url + "&showtemplate=false";
     var tmp2 = tmp.replace(/amp;/g,'');
     $(dest).load(tmp2); 
    }
      {/literal}
    /* ]]> 
    </script>

#### Et plus loin les bonnes balises
    <div style="display: none;">{* a simple wrapper *}
    <div id="cal-dayview"></div> (...)
    (...)
    <caption class="calendar-month">
    <span class="calendar-prev"><a class="calendar-nav ajaxLink" href="{$navigation.prev}" onclick="ajax_load('{$navigation.prev}','#calendar'); return false;">&laquo;</a></span>
     {$date|date_format:'%b %Y'}
    <span class="calendar-next"><a class="calendar-nav ajaxLink" href="{$navigation.next}" onclick="ajax_load('{$navigation.next}','#calendar'); return false;">&raquo;</a></span>
    </caption>

### Etape 2 : Afficher les détails dans une popup

Pour aller plus loin, je vous propose d'afficher les détails d'un calendrier dans une popup qui s'afficherait lorsque l'on clique sur le détail d'un évènement. Ces élèments n'étant pas dans un autre gabarit, la page n'aura pas à être rechargé, l'information s'affichera d'autant plus vite.

Il faut en premier lieu télécharger un script js de popup. Je vous propose celui de [leanModal](http://leanmodal.finelysliced.com.au/), qui s'y prête bien, car il permet d'afficher/masquer plusieurs popup à la fois (indispensable pour afficher les détails de plusieurs jours différents par exemple) : [télécharger le script](http://www.firehall.fr/jekyll/dnl/jquery.leanModal.min.js).

On ajoute l'appel à la librairie JS dans le template de page :

    <script src="js/jquery.leanModal.min.js" type="text/javascript">

Enfin, on modifie le gabarit du calendrier :

#### Le Javascript
    $(function() {
          $('a[rel*=leanModal]').leanModal({ top : 200, closeButton: ".modal_close" });   
      });

#### La bonne structure html
    {foreach from=$day.events item=event}
    	<li class="profile">
    	<!-- masqué par CSS au chargement de la page -->
    	<div id='popup{$event.event_id}' style="display: none;" class="modal">
      	<p>
        	<strong>{$event.event_title}</strong><br />
        	( ... ICI LES AUTRES INFOS DE DETAIL A FAIRE FIGURER ...)
      	</p>
    	<a class="calendar-event trigger {$statut} popup-button" rel="leanModal" href="#popup{$event.event_id}">
     		{$event.event_title|summarize:20}
    	</a>
    	</li>
    {/foreach}   

En résumé, on créer une div __#popup{$event.event_id}__ par défaut masquée en CSS (display: none;), puis on créait un lien qui va permettre d'ouvrir la popup ("href="popup{$event.event_id}") auquel on ajoute __"rel="leanModal"__.

{$event.event_id} va permettre d'attribuer un ID unique à chaque popup et permettre ainsi au script de définir quelle popup correspond à quel titre d'évènement.

#### Pour finir, on oublie pas les styles CSS, qui vont masquer la modale par défaut et la styler correctement lorqu'elle s'affiche 

    #lean_overlay {
    position: fixed;
    z-index:100;
    top: 0px;
    left: 0px;
    height:100%;
    width:100%;
    background: #000;
    display: none;
    }
    
    .modal{
    background: #fff none repeat scroll 0 0;
    border-radius: 5px;
    box-shadow: 0 0 4px rgba(0, 0, 0, 0.7);
    display: none;
    padding: 30px;
    width: 600px;
    }