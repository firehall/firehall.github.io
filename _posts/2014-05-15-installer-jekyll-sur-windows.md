---
layout: post_page
title: Installer Jekyll Sur Windows

categories: Jekyll
tags:
- Jekyll
- tutoriel
published: true
---

Jekyll est un générateur de site statique (pas de base de données). Il se révèle particulièrement adapté aux développeurs qui souhaitent se créer un site rapidement et totalement maintenable dans un IDE, sans avoir à passer par une interface d'administration.

###Windows et lignes de commande

Développé pour Linux/Unix et Mac OS, Jekyll n'est pas "officiellement" supporté sur Windows, on trouve pourtant de nombreuses pistes pour l'installer sur cet OS (à commencer par le <a href="http://jekyllrb.com/docs/windows/#installation">site officiel de Jekyll</a>).

Pour une install en local, il est nécessaire d'installer Ruby et il est fortement conseillé d'en faire de même avec Python pour profiter de la coloration syntaxique.

Ruby (et Python) proposent plusieurs versions Windows (32 et 64 bits). Pourtant, après plusieurs essais infructueux sur deux PC différents (et tous deux en Win7 64 bits) il apparait que les versions 32 bits sont plus stables (en tout cas plus faciles à faire fonctionner) : <a href="http://www.firehall.fr/jekyll/dnl/jekyll-sur-windows.zip">Voici un zip à télécharger, contenant les versions que j'ai installé</a> et pour lesquels je vais détailler la procédure d'installation.

###Installation de Ruby

<ol>
    <li><a href="http://www.firehall.fr/jekyll/dnl/jekyll-sur-windows.zip">Si ce n'est pas encore fait, télécharger et décompresser l'archive.</a></li>
    <li>Double-cliquer sur <strong>"rubyinstaller-1.9.3-p545.exe"</strong> et l'installer dans c:\Ruby193 (cocher les 3 boites de dialogue).
</li>
<li>Créer le dossier : <strong>c:\Ruby193\devkit</strong></li>
<li>Extraire <strong>"DevKit-tdm-32-4.5.2-20111229-1559-sfx.exe"</strong> dans le dossier créé précédement : <strong>c:\Ruby193\devkit</strong> (is s'agit du kit de développement Ruby)</li>
<li>Ouvrir la console windows (démarrer > Exécuter > cmd) pour se rendre dans le dossier d'install du devkit :
{% highlight ruby %}
cd "C:\Ruby193\devkit"
{% endhighlight %}
Initialisation et installation du kit :
{% highlight ruby %}
ruby dk.rb init
{% endhighlight %}
{% highlight ruby %}
ruby dk.rb install
{% endhighlight %}
</li>
</ol>

Ruby et son kit de dev sont maintenant installés.

###Installation de Jekyll

Il est <strong>important de passer par l'invit de commande Ruby</strong> <em>(Ce sera d'ailleurs le cas pour le reste de l'article)</em> :
Démarrer > (tous les programmes) > Ruby 1.9.3 -545 > <strong>"Start Command Prompt With Ruby"</strong> pour lancer l'installation de Jekyll :
{% highlight ruby %}
gem install jekyll
{% endhighlight %}
<em>Le curseur clignote un peu, la procédure peut prendre un peu de temps.</em>

Si tout est ok, Jekyll est maintenant installé. On pourrait s'arrêter là, mais il est toutefois intéressant d'installer Python pour profiter de la coloration syntaxique.

###Installation de Python

<ol>
    <li>Installer <strong>python-2.7.6.exe</strong> en utilisant les paramètres par défaut.</li>
    <li>En faire de même avec <strong>setuptools-3.5.1.win32-py2.7.exe</strong> (paramètres par défaut).</li>
    <li>Et enfin avec : <strong>pip-1.5.5.win32-py2.7.exe</strong> (paramètres par défaut).</li>
    <li>Ajouter les <strong>variables d'environnement</strong> :
    touche windows + pause > Paramètres systèmes avancés > Variables d'environnement :
    Modifier (ou créer) la variable Utilisateur PATH :
    C:\Python27\Scripts;
    Modifier (ou créer) la variable Systèmes PATH :
    C:\Ruby193\bin;C:\Python27\;</li>
<li>On installe alors la gem Pygments, qui va permettre la coloration syntaxique : 
On ouvre l'invit de commande Ruby :
{% highlight ruby %}
pip install Pygments
{% endhighlight %}
</li>
<li>Il semble que toutes les versions de Pygments ne sont pas stables sur Windows, on va donc faire en sorte d'<strong>utiliser la version 0.5.0.</strong>
On commence par vérifier la version qu'on vient d'installer : 
{% highlight ruby %}
			gem list
{% endhighlight %}
On repère la ligne :
{% highlight ruby %}
Pygments.rb
{% endhighlight %}
S'il ne s'agit pas de la version 0.5.0, on va donc la désinstaller (dans mon cas : 0.5.4) :
{% highlight ruby %}
gem uninstall pygments.rb --version "=0.5.4"
{% endhighlight %}
Puis on installe la version souhaitée :
{% highlight ruby %}
gem install pygments.rb --version "=0.5.0"
{% endhighlight %}
</li>
</ol>

Python est maintenant installé, on va pouvoir lancer Jekyll en local.

###Lancer Jekyll dans le navigateur
<ol>
<li>On créer un nouveau dossier de test : <strong>c:\test\</strong></li>
<li>Toujours avec l'invit de commande Ruby, on se rend dans ce dossier :
{% highlight ruby %}
cd c:\test
{% endhighlight %}
On y installe la version de base de Jekyll :
{% highlight ruby %}
jekyll new jekyll-site
{% endhighlight %}
Cette action va créer un nouveau dossier "jekyll-site" dans c:/test avec les fichiers et dossiers minimum pour utiliser Jekyll.
</li>
<li>
On se rend dans le dossier "jekyll-site" :
{% highlight ruby %}
cd jekyll-site
{% endhighlight %}
Et on lance le serveur :
{% highlight ruby %}
jekyll serve
{% endhighlight %}
</li>
<li>
Il ne reste plus qu'à ouvrir un navigateur et se rendre à l'adresse : <strong>"http://localhost:4000"</strong> pour découvrir le site.
</li>
</ol>

###Ressources :
Site officiel de Jekyll : <a href="http://jekyllrb.com">http://jekyllrb.com</a><br/>
Téléchargement de Ruby et de son kit de développement : <a href="http://rubyinstaller.org/downloads/">href="http://rubyinstaller.org/downloads/</a><br/>
Téléchargement de Python : <a href="https://www.python.org/download/">https://www.python.org/download/</a><br/>
Téléchargement de SetupTools (Python) : <a href="http://www.lfd.uci.edu/~gohlke/pythonlibs/#setuptools">http://www.lfd.uci.edu/~gohlke/pythonlibs/#setuptools</a><br/>
Téléchargement de PIP (Python) : <a href="http://www.lfd.uci.edu/~gohlke/pythonlibs/#pip">http://www.lfd.uci.edu/~gohlke/pythonlibs/#pip</a><br/><br/>
<strong>Autres tutos sur l'installation de Jekyll sur Windows:</strong><br/>
<a href="https://github.com/juthilo/run-jekyll-on-windows/">https://github.com/juthilo/run-jekyll-on-windows/</a><br/>
<a href="https://www.youtube.com/watch?v=EtqZVTIro_c">https://www.youtube.com/watch?v=EtqZVTIro_c</a>

