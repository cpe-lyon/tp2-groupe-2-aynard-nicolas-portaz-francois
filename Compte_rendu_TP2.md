*TP2 - Bash*
============

*Exercice 1 - Variables d'environnement*
------------

**1**
Dans quels dossiers bash trouve-t-il les commandes tapées par l’utilisateur?  
Il les trouves dans les dossiers bash présent dans le dossier bin maid aussi dans la varibale $PATH

**2**
Quelle variable d’environnement permet à la commande **cd** tapée sans argument de vous ramener dansvotre répertoire personnel ?  
La variable $HOME.

**3**
Explicitez le rôle des variables **LANG,PWD,OLDPWD,SHELL et _**.  
*LANG : est la variable définit la langue
*PWD : permet de savoir dans quel repertoire on se trouve (Print Working Directory)
*OLDPWD : Répertoire dans lequel on se trouvait avant de faire un cd
*SHELL : intepréteur de commande utilisateur
*_ : emplacement de la commande printenv

**4**
Créez une variable locale MY_VAR(le contenu n’a pas d’importance). Vérifiez que la variable existe.  
MY_VAR=test
echo $MY_VAR -> affiche test

**5**
apez ensuite la commande bash. Que fait-elle? La variable MY_VAR existe-t-elle? Expliquez. A la fin de cette question, tapez la commandeexitpour revenir dans votre session initiale.  
Quand on refait echo, cela affiche test 

**6**
Transformez MY_VAR en une variable d’environnement et recommencez la question précédente. Expli-quez.  
xport MY_VAR=test
echo $MY_VAR -> affiche test
Après si on fait bash, quand on refait echo, cela affiche test.
Explivaton : variable locale n'est dispo que dans le bash dans lequel on se trouve donc dès que l'on fait un nouveau bash ou que l'on tape exit on n'aura plus cette variable. Lorsque l'on fait export, la variable est dispo partout.

**7**
Créer la variable d’environnement NOMS ayant pour contenu vos noms de binômes séparés par un espace.Aﬀicher la valeur de NOMS pour vérifier que l’affectation est correcte  
export NOMS=Portaz Aynard  
echo $NOMS  
le résultat est Portaz  
Pour mettre l'space il faut écrire : export NOMS='Portaz Aynard'

**8**
Ecrivez une commande qui aﬀiche ”Bonjour à vous deux, binôme1 binôme2!” (où binôme1 et binôme2sont vos deux noms) en utilisant la variable NOMS.  export NOMS  
export NOMS='Bonjour à vous deux, Portaz et Aynard'
echo $NOMS

**9**
Quelle différence y a-t-il entre donner une valeur vide à une variable et l’utilisation de la commande unset?  
Unset efface de la mémoire les variables passées en paramètres. 

**10**
Utilisez la commande echo pour écrire exactement la phrase :$HOME =chemin (où chemin est votre dossier personnel d’après bash)  
echo ':$HOME ='$HOME



*Programmation Bash*
------------


*Contrôle de mot de passe*
------------



*Expressions rationelles*
------------


*Contrôle d'utilisateur*
------------


*Factorielle*
------------


*Le juste prix*
------------


*Le juste prix*
------------


