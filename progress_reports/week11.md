# Week 11

## 24/06/2024

Aujourd'hui, j'ai travaillé sur mon rapport de stage car il est à rendre avant demain. J'ai justifié l'ensemble des paragraphes qui étaient alignés à droite puis j'ai relu mon résumé qui était trop long. J'ai changé certaines tournures de phrases afin de racoursir un peu cette partie mais elle est encore trop longue. J'ai finalement choisi de retravailler cette partie entièrement sans rentrer trop dans les détails.

J'ai ensuite refait une relecture complète de mon rapport de stage en corrigeant les petits détails qui ne vont pas.

Pour finir la journée j'ai travaillé sur l'application, j'ai regardé pour avoir un moyen d'avoir juste certains fichiés affiché dans le file explorer de l'application. Malheureusement je n'ai pas trouvé de solution qui répond à ce problème pour le moment.

Armand:

Relecture de rapport vite fait correction aussi d'erreurs d'anglais

Travail sur le projet, fin de refactor de comment on s'occupe de la nouvelle tab (bien plus opti) + ajout fonctions en prévision d'ajout de fonctionnalitées dans cette même tab (pour swap et link)

## 25/06/2024

Aujourd'hui, j'ai travaillé sur l'application, j'ai décidé de ne pas trvailler sur ce que je faisait hier mais plutôt sur une autre idée que j'ai eu. Il n'était pas possible de directement charger le dernier project ouvert dans l'application. Grâce à un fichiers je veux ajouter une action permettant de charger le dernier projet ouvert directement sans ouvrir la recherche dans le file explorer.

Pour faire ça j'ai ajouté deux fonctions, une pour charger le nom du dernier project depuis un fichier et une autre pour le sauvegarder dans ce même fichier. Ces fonctions sont appelées dès que l'utilisateur veut charger le dernier projet et dès qu'il en ouvre un autre.

J'ai pas eu de problème et tout a marché correctement du premier coup donc je suis allé travailler sur le system documentation du project où on note tout ce qu'on a ajouté afin de mettre un tutoriel de comment mettre en place la nouvelle feature last project dans l'application.

Ensuite, j'ai travaillé sur le MenuBar de l'application, en effet celui ci est écouté mais les racourcis clavier ne sont pas encore implémentés. J'ai donc ajouté un écouteur d'évenement qui va écouter quand l'utilisateur va presser ctrl + quelque chose. Cet écouteur marche pas car on dirais que l'action est déjà prise en compte ailleur mais qu'elle ne fait rien. Il faudrait écouter chaque action individuellement pour régler ça.

Armand:
  Aujourd'hui j'ai commencer a travailler sur l'implémentation du swap & du link directement dans notre onglet. Pour ce faire, j'ai prit la même approche que pour la selection, c'est a dire que j'ai décidé de greffer les cliques afin qu'ils envois les informations a l'environment 3D. Pour cela, on a transformer les fonctions s'occupant de gerer les liens et les swap dans le display en "slots" afin qu'on puisse envoyer des signaux spéciaux dépuis notre tab que le display va recevoir. Il va donc considérer ce que nous avons envoyé de la même manière qu'il aurait considérer un clique fait sur un marqueur. Actuellement, les nouveaux boutons marchent, même si c'est quelque peu compliqué a gérer.
  

## 26/06/2024

Aujourd'hui, j'ai travaillé sur l'application, j'ai continué ce que je faisais la veille, c'est à dire gérer correctement les raccourcis clavier. J'ai trouvé une solution qui est d'ajouter un signal au MenuBar qui sera emit à chaque fois qu'une action va être effectuée individuellement. De cette manière seul le nouveau signal sera écouté dans la mainwindow mais celui ci sera émit par chaque action triggered individuellement donc les raccourcis clavier seront pris en compte.

J'ai réussi à implémenter ça sans trop de problème et je vais l'ajouter au system documentation du project.

Pour continuer la journée, j'ai travaillé sur la sub application Swapping Corrector. En effet, celle ci n'a pas de shortcut, par conséquent, j'ai décidé d'en ajouté. Une fonction récupérant l'événement "keyPressed" existe déjà donc j'ai juste à la modifier. Globalement, j'ai ajouté des raccourcis clavier pour chaque bouton et j'ai facilité la navigation entre les différents tab de l'application.

J'ai réussi à implémenter ça sans trop de problème et je vais l'ajouter au system documentation du project.

Armand:
  Aujourd'hui j'ai déjà refactor ce que j'ai fait la veille. En effet, je veux qu'on puisse savoir visuellement quels marqueurs sont selectionnés car pour le Swap, c'est compliqué sinon. Pour cela je voulais garder entièrement en interne les markers séléctionner. Cela aurait pu marcher mais si jamais un changement était fait dans l'implémentation de la selection des markeurs dans le dislay, cela ne marcherait surement plus bien. J'ai donc décider de laisser tous être gérer par les signaux, en implémentant des nouvelles connections qui vont gérer dynamiquement les marqueurs sélectionné.
  Une fois cela fait, il fallait que je trouve comment afficher visuellement quand un marqueur est sélectionner. Pour ce faire, j'ai voulu travailler avec les QStyleSheet mais cela est compliqué et n'aurait pas vraiment de sens dans notre application vu qu'elle n'en utilise jamais. J'ai donc décider pour le moment de simplement changer le texte des boutons sélectionés afin qu'on puisse voir d'un coup d'oeil quels marqueurs sont selectionnés.

## 27/06/2024

Aujourd'hui, j'ai continué à travailler sur l'application. On a emplémenté beaucoup de fonctionnalités en plus et on commence à ne plus savoir quoi faire. Ainsi on va essayer d'organiser un meeting le plus vite possible pour voir ce qu'on peut faire pour la suite. En  attendant j'ai continué à ajouter des raccorucis clavier. J'ai voulu permettre à l'utilisateur de bouger l'environment 3D avec les flèches du clavier. J'ai donc ajouté un écouteur d'événement qui va écouter les flèches du clavier et qui va bouger l'environment 3D en conséquence. Cependant ça n'a pas marché, je pense que l'événement est déjà utilisé ailleur dans l'application il ne fait rien mais de tout de façon la rotation de l'environement 3D  de CameraManager et assez complexe et il est difficile et pas sécurisé de le diriger avec les flèches du clavier.

J'ai ensuite remarqué que si on ouvre un fichier d'un projet et qu'on active ensuite le color mode, la page du fichier reste ouverte alors qu'on a désactivé. J'ai chnagé le code pour fermer le projet et toutes les fenêtres ouvertes quand on active le color mode.

Armand:
  Aujourd'hui j'ai continuer a rendre notre tab plus utilisable. Pour cela, j'ai gardé en interne un QVector de listes d'index de markeurs, afin qu'on puisse voir, quand on clique sur un bouton, les autres markeurs vers lesquels ce qu'on vient de cliquer est lié sont visuellement visible.
De cette manière, toutes les listes sont link, et j'ai permit a l'utilisateur de maintenant deselectionner un markeur (pour le mettre en couleur) depuis notre tab.
Pour cela on a simplement une liste de boolean où quand un markeur est selectionné il est mit en true, et sinon c'est en false.

## 28/06/2024

Aujourd'hui, j'ai travaillé sur l'application. J'ai ajouté une feature que je voulais implémenté depuis longtemps. En effet j'ai implémenté la possibilité de sauvegarder des photos depuis les caméras dans des dossiers choisis. J'ai simplement ajouté divers boutons et raccorucis clavier permettant de prendre une image à un instant t de depuis chaque camera ouverte et ensuite de laisser l'utilisateur les sauvegarder dans les dossier de son choix. Comme je veux que l'option soit active uniquement quand le live view est activé j'ai dû ajouter quelques conditions mais rien de bien compliqué.

Une fois la feature implémentée j'ai édité le system documentation du projet pour ajouter un tutoriel de comment mettre en place cette nouvelle feature.

Armand:
  Tous marche maitneannt avec des fix de problèmes concernant les boutons "swap" et une refonte de la manière dont on gère les signaux pour selectionner visuellement des markeurs
