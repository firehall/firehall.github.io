---
layout: post_page
title: Optimiser un projet web avec Grunt

published: true
---

Gruntjs permet d'automatiser un certains nombres de tâches , telles que : concatener et minifier des fichiers css ou js, vérifier des erreurs de code etc...  

__Prérequis :__ Pour utiliser Grunt il faut avoir installé Nodejs.

Voici un rapide résumé des actions à réaliser pour optimiser les fichiers d'un projets web.

On ouvre une nouvelle invit de commande NodeJs et on se rend dans le bon dossier :

    cd chemin_dossier
    
__rappel: pour parcourir des dossiers sur un autre disque que c:, il convient en premier de temps d'entrer la lettre du lecteur__
    
    ex: E:
    
On installe grunt de manière permanente :

    npm install -g grunt-cli

On créer un fichier json relatif au projet :

    npm init
    
__A ce stade un fichier package.json est créé à la racine du projet__

On installe grunt dans le projet :

    npm install grunt --save-dev
    
On créer un nouveau fichier : _Gruntfile.js_ 

    module.exports = function(grunt){
    
        grunt.initConfig({
        
            //Ici la config des modules
        
        });
        
        //Ici la liste des tâches
    }
    

###Quelques fonctions utiles :

On se rend sur le site de grunt, dans la section plugin et on cherche les plugins interessants. __remarque__ on préfèrera les plugins commencant par "contrib-", correspondants à des plugins mis en place par les développeurs de grunt:

###Task
Ce module simplifie le processus d'installation des fonctions (dans le fichier Gruntfile.js) :

    npm install --save-dev load-grunt-tasks
    
Gruntfile.js : 

        module.exports = function(grunt){
        
        //Task
        require('load-grunt-tasks')(grunt);
        
        grunt.initConfig({
        
            //Ici la config des modules
        
        });
        
        //Ici la liste des tâches
        grunt.registerTask('default', []);
    }

###Concaténation js: contrib-concat

    npm install grunt-contrib-concat --save-dev
    
Gruntfile.js:

    //Combiner les fichiers js
	  concat: {  		
	    fusion: {
	      src: ['scripts/script1.js', 'scripts/script2.js'],
	      dest: 'scripts/prod/script-concat.js',
	    }
	  }
      
###Uglify : Minifier du js

    npm install grunt-contrib-uglify --save-dev
    
Gruntfile.js:

    uglify: {
        //ne pas modifier les noms de variables => utile pour angular.js par ex
        options: {
            mangle: false
        },
        dist: {
            files: {
                'scripts/prod/min.js': ['scripts/prod/script-concat.js']
            }
        } 
    }
    
###JShint : repérer des erreurs js

    npm install grunt-contrib-jshint --save-dev
    
Gruntfile.js:

    //chercher erreurs de js
    jshint: {
 	  all: ['scripts/*.js'],
 	  // *=> tous les js.
 	  // Chercher dans sous dossier :
 	  // 'scripts/**/*.js'
 	  //exclure un fichier :
 	  //'!scripts/nom_fichier.js'
 	}
      
###cssmin : Concatener et minifier des css

    npm install grunt-contrib-cssmin --save-dev
    
Gruntfile.js:

    cssmin: {
        combine: {
		    files: {
		      'css/min.css': ['css/feuille_style01.css', 'css/feuillesty_le02.css']
		    }
		  }
    }
    
###watch : Autoexecution de grunt lorsqu'une modification est détectée 

    npm install grunt-contrib-watch --save-dev
    
Gruntfile.js:

    watch: {
        css: {
		    files: ['css/*.css', '!css/min.css'], //on ignore les fichiers minifiés
		    tasks: ['cssmin'],
		    options: {
		      spawn: false,
		      livereload: false, //pour utiliser livereload
		    },
            //On peut faire de même avec le js
		    //js: {
		   // files: ['scripts/*.js']
		   // tasks: ['jshint', 'uglify'],
		   // options: {
		   //   spawn: false,
		  // },
        },
    }
    
Fichier Gruntfile.js final :

    module.exports = function(grunt){
        
        //Task
        require('load-grunt-tasks')(grunt);
        
        //Ici la config des modules
        grunt.initConfig({
        
            //Combiner les fichiers js
	       concat: {  		
	           fusion: {
	               src: ['scripts/script1.js', 'scripts/script2.js'],
	               dest: 'scripts/prod/script-concat.js',
	           }
	       },
           
           uglify: {
                //ne pas modifier les noms de variables => utile pour angular.js par ex
                options: {
                    mangle: false
                },
                dist: {
                    files: {
                    'scripts/prod/min.js': ['scripts/prod/script-concat.js']
                    }
                } 
            },
        
            //chercher erreurs de js
            jshint: {
              all: ['scripts/*.js'],
              // *=> tous les js.
              // Chercher dans sous dossier :
              // 'scripts/**/*.js'
              //exclure un fichier :
              //'!scripts/nom_fichier.js'
            },
        
            cssmin: {
                combine: {
                    files: {
                      'css/min.css': ['css/feuille_style01.css', 'css/feuillesty_le02.css']
                    }
                }
            },
            
            
            watch: {
                css: {
                    files: ['css/*.css', '!css/min.css'], //on ignore les fichiers minifiés
                    tasks: ['cssmin'],
                    options: {
                      spawn: false,
                      livereload: false, //pour utiliser livereload
                    },
                    //On peut faire de même avec le js
                    //js: {
                   // files: ['scripts/*.js']
                   // tasks: ['jshint', 'uglify'],
                   // options: {
                   //   spawn: false,
                  // },
                },
            }
            
        
        });
        
        //Ici la liste des tâches
        grunt.registerTask('default', ['concat', 'uglify', 'jshint', 'cssmin', 'watch']);
    }
    
On peut maintenant lancer l'ensemble des taches :

    grunt
    
Ou une tâche indépendamment (ex: cssmin)

    grunt cssmin
    
On peut aussi réutiliser cette config dans un autre projet, pour celà il suffit de copier/coller les fichiers "Gruntfile.js" et "package.json" puis on se place dans le nouveau dossier :

    cd dossier_autre_projet
    
    npm init
    
    grunt
    
###_Bonus (minus?)_ : Minifier des images avec imagemin

_Je n'en ai pas parlé plus tôt car je n'ai pas réussi à le faire fonctionner chez moi (win7 64bits), malgré de nombreuses tentatives (upgrade/downgrade des plugins, de npm, NodeJs, Git et Grunt)..._  
Voici toutefois la marche à suivre : 

     npm install grunt-contrib-imagemin --save-dev
    
Gruntfile.js:

    imagemin: {                          
  		dist: {                         
  		    files: [{
  		    expand: true,                  
  		    cwd: 'img/',                   
  		    src: ['*.{png,jpg,gif}', '**/*.{png,jpg,gif}'],   
  		    dest: 'min/'                  
  		    }]
        }
    }

###Ressources:
[http://gruntjs.com/](http://gruntjs.com/)  
[Un tuto vidéo très sympa de Grafikart](http://www.grafikart.fr/tutoriels/grunt/grunt-introduction-470)