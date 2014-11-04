---
layout: post_page
title: Problèmes liés à la mise en cache de fichiers sur un serveur Web

published: true
---

Tôt ou tard l'intégrateur web est confronté à des problèmes liés à la configuration des serveurs web. Parmis eux, l'un des plus courants et la mise en cache de fichiers. Ceci est d'autant plus vrai lorsqu'on est ammené à travailler sur un serveur mutualisé, sur lequel on a pas forcément la main et où les possibilités sont limitées .

Il m'arrive ainsi de temps en temps, de devoir modifier un fichier CSS ou JS sur un environnement de production et de rencontrer ce problème lié au cache : on a beau rafraichir, vider le cache navigateur, rien n'y fait, les mises à jour ne sont pas prises en compte en temps et en heure.

_Ce type de situation est d'autant plus vrai lorsqu'on ne travaille pas sur un CMS. Ces derniers ayant bien souvent leur propre système de mise en cache (voir de minification) qui règlent le problème (un petit tour dans les préférences du CMS et le cache est désactivé!)._

La solution proposée aujourd'hui a le mérite d'être très simple à mettre en place et (à priori) de fonctionner à tous les coups. Je l'ai en tout cas mise en pratique très récemment sur un serveur mutualisé d'OVH. 

Il s'agit d'__étendre le nom du fichier avec la fonction date de php__. Pour que la mise en cache ne fasse plus effet, il faut simplement que le nom du fichier change en permanence (en tout cas après chaque mise à jour), la solution radicale est donc d'utiliser les minutes et les secondes ce qui donne (par exemple pour une feuille de style css) :

    <link rel="stylesheet" href="path/to/css/styles.css?q<?php echo date('i-s'); ?>">
    
Résulat : à chaque rechargement de la page, le nom du fichier sera modifié, le cache est donc tout simplement impossible.

A noter que c'est une solution qu'il est préférable d'utiliser uniquement lorsque le problème apparait, une fois les modifications terminées il est conseillé de rebasculer sur un nom de fichier statique pour permettre la mise en cache et gagner en performances.