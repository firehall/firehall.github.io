---
layout: post_page
title: Débuter avec Sass et Compass

published: true
---

(Rappel: Il faut avoir installé Ruby, NodeJs et Python sur son ordinateur [ >> Rappel sur Windows](http://blog.firehall.fr/jekyll/2014/05/15/installer-jekyll-sur-windows.html)  

Ouvrez votre termninal de commande (comme celui de NodeJS par exemple) :

### Sass

Installation de Sass :

    gem install sass
    
Et voilà! :)

On peut vérifier que tout est ok, en _checkant_ la version installée :

    sass -v
    
Au besoin on peut le mettre à jour :

    gem update sass
    
#### Source :
[http://sass-lang.com/install](http://sass-lang.com/install)  

    
### Compass

Installation de compass :

    gem install compass

Utilisation de compass :

    compass w
    
On créait un fichier de config à la racine du projet 

    cd path/to/project
    
Contenu de config.rb

    http_path = "/"
    css_dir = "/css/"
    sass_dir="/sass/"
    images_dir = "/img/"
    javascripts_dir = "/"
    
_On utilisera ce fichier surtout pour indiquer où se trouve le fichier de développement (sass_dir) et où compiler le fichier css de production (css_dir)_

#### Source :
[http://www.grafikart.fr/tutoriels/html-css/framework-css-compass-140](http://www.grafikart.fr/tutoriels/html-css/framework-css-compass-140)  
    
### Trucs et astuces

_Je commence à peine à utiliser Sass/compass, personnelement je préfère commencer doucement et je l'utilise donc sur des points précis qui me permettent de gagner du temps sur mes développements. Il est donc fort propable, que cette partie s'étoffe avec le temps._

####Charger des bibliothèques de Compass

Un des avantages qui à mon sens, saute aux yeux, est la gestion des préfixes vendeurs, dans le cas de spécificités CSS3. On peut ainsi décider de charger toute les bibiliothèques de Compass ou au contraire, piocher uniquement ce que l'on veut. C'est ce que je fais actuellement en chargeant uniquement la bibliothèque CSS3 :

On édite donc notre fichier sass/styles.scss et on y ajoute :

    @import "compass/css3";
    
A partir de là je peux par exemple définir des arrondis sur mes boites, sans avoir à me préoccuper du rendu suivant le navigateur :

    .selecteur{
        @include border-radius(15px);
    }
    
Dans cet exemple, j'applique un arrondi de 15px sur les 4 angles de ma boite.

Je peux aussi définir une valeur par défaut (par exemple 10px)  :

    $default-border-radius: 10px;
    
Il me suffit alors de faire appel à la propriété sans préciser de valeur :

        .selecteur{
            @include border-radius;
        }
        
Il existe bien entendu des propriétés CSS3 qui englobent de nombreuses valeurs, c'est le cas par exemple de box-shadow. 
On va également pouvoir définir une fois pour toutes les réglages qui correspondent à la charte graphique :

    $default-box-shadow-h-offset: 0px;
    $default-box-shadow-v-offset: 5px;
    $default-box-shadow-blur: 0px;
    $default-box-shadow-spread: null;
    $default-box-shadow-color: rgba(0,0,0,0.2);
    $default-box-shadow-inset: null;
    
On peut ensuite l'utiliser simplement de cette manière :

    .selecteur{
        @include box-shadow;
    }
    
Si on veut utiliser des valeurs spécifiques sans les déclarer préalablement (de manière isolée) :

    single-box-shadow($hoff, $voff, $blur, $spread, $color, $inset)
    
Soit, pour un exemple concret :

    .selecteur{
        @include single-box-shadow(5px, 5px, 10px, null, #333, null);
    }
    
####Créer des variables simples

Encore plus simple, et tout aussi pratique, on peut créer des variables toutes simples sous forme de mot-clé pour se référer à des valeurs qui seraient autrement bien plus délicates à retenir!  
Par exemple, je travaille sur un site dont la charte emploi un rouge/bordeaux en couleur de fond, qui a pour valeur hexadécimale : #661212, je peux simplement faire :

    $redBg: #661212;
    
Lorsque je serai en cours d'intégration de ma maquette, je pourrai alors appeler cette couleur très simplement :

    .selecteur{
        background: $redBg;
    }
    
C'est aussi valable pour des polices, des valeurs numériques, ... Tout ce qu'on veut en fait!

    $sansSerif: 'Source Sans Pro', sans-serif;
    
    //usage :
    .selecteur{
        font-family: $sansSerif;
    }
    
    $big: 1200px;
    
    //usage :
    .selecteur{
        width: $big;
    }
    

#### Source :
[http://compass-style.org/reference/compass/](http://compass-style.org/reference/compass/)  


