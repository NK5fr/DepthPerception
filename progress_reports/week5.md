# Week 5

## 13/05/2024

Pour commencer la journée, nous avons chercher à voir si des fonctionnalités de notre application, que nous n'avions pas encore testées, marchaient correctement.
Nous avons donc commencer par vérifier si la sauvegarde le chargement des fichiers de configuaration marchaient, et après avoir vérifié, ça ne marche pas.

Nous avons cherché à comprendre pourquoi ça ne marchait pas, et nous avons trouvé que la sauvegarde des paramètres de fichiers était faite pour les caméras de base, pourtant nous utilisons des caméras avec Spinnaker et donc les paramètres ne sont pas les mêmes.
Nous allons donc devoir modifier la sauvegarde des paramètres pour qu'elle soit compatible avec les caméras Spinnaker.

Nous avons du faire une petite pause car le pc lag énormément et on ne pouvait plus travailler correctement.

Après avoir utilisé la save avec spinnaker nous avons pu sauvegarder les paramètres de la caméra. On a remarqué ensuite que le chargement des paramètres est également flou au niveau des caméras spinnaker et va devoir créer également des fonctions pour charger les paramètres de ces caméras. Le principal problème est que les paramètres ne sont pas les même que les caméras de base. De plus de nombreuses classes et méthodes existent dans le code pour les caméras spinnaker mais ne sont pas utilisées ou sont incomplètes.
Le chargement des paramètres de la caméra ne fonctionnait pas non plus, la raison étant que la méthode pour mettre a jour les paramètres se faisait un nombre de fois égale a une variable qui a laquelle nous ne touchions pas. Après avoir changé la variable, le chargement des paramètres fonctionne correctement, ce qui nous donne un chargement et une sauvegarde fonctionnelle.

Nous avons ensuite changé de pc car les bugs de celui habituel nous empêchait de travailler. Nous avons commencé à regarder toutes les parties inutiles du au fait que nous utilisons uniquement les caméras avec spinnaker. Nous avons mis ces parties inutiles en commentaire car nous ne savons pas si pouvons les enlever ou pas.

Nous avons également commenté des lignes à propos de threads qui provoquent une erreur à la fermeture de l'application. Finalement sans ces lignes les caméras ne sont plus repérées donc on va les remettre et regarder pourquoi ça ne marche pas.

Nous avons aussi une autre erreur qui est que lorsqu'on essaie de fermer la fenêtre d'une caméra l'application plante. L'erreur vient du fait que lorsqu'on envoie l'image on ne vérifie pas si le fenêtre est fermée ou non. Nous avons donc rajouté une vérification pour voir si la fenêtre est fermée ou non et si elle est fermée on n'envoie pas d'image.

Pour finir la journée nous avons corrigé une action d'un bouton qui ne fonctionnait pas. En effet il y avait un bouton permettant de gérer l'activation du tracker de la souris sur les images mais il n'y avait pas d'action associé à ce bouton. Après divers recherches nous avons trouvé quoi lancer à l'activation de ce bouton et nous avons donc associé une action.

## 14/05/2024

Pendant le début de cette journée nous avons principalement fait des recherches sur les rapports de stage et sur ce qu'on va mettre dedans. On s'est aussi renseigné sur markdown mais il semble finalement que certains aspect du rapport sont difficiles à faire et que google docs apporte également des outils efficaces pour un meilleur rendu.

On a ensuite fait un mini meeting avec Tomas Holt pour voir ce qui est à faire pour la suite du projet car nous avons corrigé de nombreuses fonctionnalité et on avait beaucoup de question sur qu'il nous restait encore à faire et à quel point pouvont nous modifier l'application. 

Après ce mini meeting nous avons cherché à compiler le projet sur windows sans succès. Il semblerait que le version du compilateur c++ n'est pas correct mais même après avoir changé la version et testé plusieurs options nous n'avons pas réussi à compiler le projet. Nous avions déjà eu cette erreur avant mais c'était avec un projet contruit différament donc nous ne pouvons pas corriger l'erreur comme on l'avait déjà fait.

On a passé ensuite le reste de la journée à résoudre ce problème. Cependant nous n'avons pas réussi à avoir de bons résultats et nous ne sommes même pas sûr de où provient vraiment le problème. Nous avons trouvé que le problème venait d'un fichier nommé qmake.stash il semblerait qu'il contient de fausses indications à propos du compilateur c++ donc on l'a supprimé temporairement pour voir si ça changeait quelque chose. Nous n'avons plus l'erreur mais nous en avons d'autres car nous devons régler de nombreux problèmes de librairies et de dépendances. Le fichier qu'on a supprimé servait à enregistrer des informations de compilation qui sont obsolète pour nos dernières versions.

## 15/05/2024

Pour la première heure de cette journée nous avons continué nos recherches sur comment compiler et lancer le projet sur windows. Cependant la liste des imports et des dépendances est très longue et elle n'est pas très claire. Nous avons des problèmes avec l'import d'opengl et de glu notamment. Après avoir tenté beaucoup de choses et fait de nombreuses recherches nous n'avons pas eu de résultats concluants.

J'ai ensuite un peu aidé armand pour l'import du projet sur linux car j'ai changé des choses de le fichier .pro et certaines importations ne marchaient plus. Après avoir changé quelques lignes dans le fichier .pro le projet a pu être importé correctement. Je suis ensuite retourné sur windows pour essayer de compiler le projet. J'ai essayé de chercher comment corriger les erreurs en changeant l'importation des librairies mais il semble que les erreurs sont plus profondes que ça. L'origine de l'erreur est difficile à déceler donc c'est assez compliqué de la corriger. De plus je n'ai pas trouvé de personnes ayant les mêmes erreurs sur internet donc je peux juste supposer les différentes raisons de celle ci.

La partie windows du .pro est beaucoup plus fournie que celle pour linux et en plus on dirait que tout est généré automatiquement donc c'est difficile de savoir ce qui est important et ce qui ne l'est pas. J'ai donc essayé de supprimer des parties du .pro pour voir si ça changeait quelque chose mais ça n'a pas eu d'effet. J'ai donc remis les parties supprimées et J'ai continué à chercher d'autres solutions.

J'ai enfin réglé les problèmes de GLU.h, en effet le fichier gl.h qui est nécessaire dans glu.h ne trouvait pas le type WINGDIAPI. J'ai ajouté un include de windows.h juste avant l'include de glu.h. Il a pu trouver les types correctement et le fichier GLU.h n'a plus affiché d'erreurs. Il reste cependant plusieurs autres erreurs du même type à régler. En effet beaucoup de fichiers affichent l'erreur 'byte' symbole ambigu. Depuis c++17 il y a deux types byte, il y a usigned char byte et std::byte. Ilfaut donc trouver un moyen de les différencier pour que le compilateur ne soit pas perdu. Dans un premier temps je vais supprimer tous les using namespace std et corriger les erreurs que cela inclut pour voir si ça change quelque chose. Cela n'a pas changé grand chose et le compilateur est toujours perdu.

Finalement il restait beaucoup de "using namespace std" dans le code j'ai donc tout supprimé et j'ai adapté le code. j'ai dû remplacer certains max et min par qMax et qMin car le code n'arrivait pas à trouver std::max et std::min en raison du fait qu'il voulait absolument prendre max et min des fichiers windows (inutilisable sur linux). J'ai pu compiler et lancer l'application.

Armand:
- J'ai passé la matinée a faire des recherches sur l'erreur de GLU que Nathan rencontrait, mais je n'ai rien trouvé, je suis donc passé sur la résolutions de certains problèmes sur Linux
- Résolution des "incorrect sRGB profile" warning pour les icones
- J'ai passé le reste de la journée a traquer les erreurs de Thread, mais je n'ai pas eu le temps de trouver la source du problème et de le résoudre, même si j'ai trouvé quel méthode / quel instruction semble causé ce problème. La solutions serait surement de "simplement" recoder la détéction des caméras, qui est la cause du problème.


## 16/05/2024

Pour commencer la journée j'ai testé quelques fonctionnalités de l'application sur windows pour voir si tout est bien connecté. J'ai remarqué rapidement qu'il n'y avait pas de paramètres de caméra. La raison était que certain fichier n'était pas présent dans le projet, certainement que nous les avons supprimé sans faire exprès lors de leur manipulation. J'ai donc récupéré ces fichiers dans les backups et j'ai pu lancer l'application correctement en les ajoutant dans les fichiers.

Maintenant qu'on peut lancer le code sur windows, il ne reste plus qu'à améliorer l'application. Il y a quelques ajouts qu'on pourrait faire comme une checkbox pour activer la couleur ou mettre des événements sur la toolbar en haut de l'application ainsi qu'ajouter des raccourcis clavier pour les boutons de la toolbar... La priorité cependant est de déjà nettoyer le code, il y a beaucoup de parties sur FlyCapture qui ne sont pas utilisées et qui sont inutiles. Il faudrait donc les enlever pour que le code soit plus lisible et plus facile à comprendre. Il y a également beaucoup d'import dans le fichier .pro losqu'on utilise windows et je ne sais pas si ils servent vraiment tous. Il faudrait voir ce qui est supprimable ou non.

Cependant je n'ai pas commencé tout ça maintenant j'ai plutôt commencé à rédiger un rapport sur l'évolution de Camera Manager. Ce rapport contiendra toutes les indications d'installation. Ce qu'il faut changer pour faire touner sur les dernières versions. Ce qu'on a ajouté au code. En somme il y aura tout sur comment passer de 2019CameraManager à 2024CameraManager.

Armand:

J’ai continuer les recherches sur les Thread sans toujours trouver la raison du problème, et je me suis 
donc penché sur un problème sous Windows que nous avons qui fait que l’image récupérée par la 
caméra ne semble pas prendre toute la taille de la fenêtre sous Windows, tandis qu’elle prend toute la 
place dans la fenêtre sous Linux. 
J’ai aussi cherché et trouvé où ce calcul était fait, mais je ne comprends pas d’où vient l’erreur, étant 
donné qu’il semble que sous Windows, le programme ne comprends pas la vraie taille de la fenêtre. Le 
calcul est bon mais la donnée qu’il récupère ne semble pas être la bonne. Le problème que je rencontre 
est que le code est très complexe et qu’il n’y a absolument pas de documentation quand a ce que les 
méthodes font, ce qui rends la compréhension et la navigation du code très ardue. 
