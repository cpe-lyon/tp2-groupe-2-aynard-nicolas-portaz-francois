*TP2 - Bash*
============

*Exercice 1 - Variables d'environnement*
------------

**1**
Dans quels dossiers bash trouve-t-il les commandes tapées par l’utilisateur?  
Il les trouves dans les dossiers bash présent dans le dossier bin maid aussi dans la varibale $PATH

**2**
Quelle variable d’environnement permet à la commande **cd** tapée sans argument de vous ramener dans votre répertoire personnel ?  
La variable $HOME.

**3**
Explicitez le rôle des variables **LANG,PWD,OLDPWD,SHELL et _**.  
*LANG : est la variable qui définit la langue
*PWD : permet de savoir dans quel repertoire on se trouve (Print Working Directory)
*OLDPWD : Répertoire dans lequel on se trouvait avant de faire un cd
*SHELL : intepréteur de commande utilisateur
*_ : emplacement de la commande printenv

**4**
Créez une variable locale MY_VAR(le contenu n’a pas d’importance). Vérifiez que la variable existe.  
MY_VAR=test
echo $MY_VAR -> affiche test

**5**
Tapez ensuite la commande bash. Que fait-elle? La variable MY_VAR existe-t-elle? Expliquez. A la fin de cette question, tapez la commande exitpour revenir dans votre session initiale.  
Quand on refait echo, cela affiche test.

**6**
Transformez MY_VAR en une variable d’environnement et recommencez la question précédente. Expliquez.  
xport MY_VAR=test
echo $MY_VAR -> affiche test
Après si on fait bash, quand on refait echo, cela affiche test.
Explicaton : variable locale n'est dispo que dans le bash dans lequel on se trouve donc dès que l'on fait un nouveau bash ou que l'on tape exit on n'aura plus cette variable. Lorsque l'on fait export, la variable est dispo partout.

**7**
Créer la variable d’environnement NOMS ayant pour contenu vos noms de binômes séparés par un espace.Afficher la valeur de NOMS pour vérifier que l’affectation est correcte  
export NOMS=Portaz Aynard  
echo $NOMS  
le résultat est Portaz  
Pour mettre l'espace il faut écrire : export NOMS='Portaz Aynard'

**8**
Ecrivez une commande qui aﬀiche ”Bonjour à vous deux, binôme1 binôme2!” (où binôme1 et binôme2 sont vos deux noms) en utilisant la variable NOMS.  export NOMS  
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
Vous enregistrerez vos scripts dans un dossier script que vous créerez dans votre répertoire personnel.Tous les scripts sont bien entendu à tester.Ajoutez le chemin vers script à votre PATH de manière permanente  
export PATH=$PATH:$PWD (à condition que l'on soit dans le bon répertoire : le répertoire script).

*Exercice 2 - Contrôle de mot de passe*
------------
Écrivez un script testpwd.sh qui demande de saisir un mot de passe et vérifie s’il correspond ou non au contenu d’une variable PASSWORD dont le contenu est codé en dur dans le script. Le mot de passe saisi par l’utilisateur ne doit pas s’afficher    
vim testpwd.sh //Crée le fichier si il n'existe pas  
Dans le script : (on n'utilise pas PASSWORD mais directement la valeur)   
```bash
#!/bin/bash
echo 'Saisir un mot de passe'
read -s MDP
if [ "$MDP" == "tp" ]; then echo 'correct'
else echo 'Faux'
        fi
```
Ensuite il faut sortir du script et faire ./testpwd.sh  


*Exercice 3 - Expressions rationnelles*
------------
Ecrivez un script qui prend un paramètre et utilise la fonction suivante pour vérifier que ce paramètreest un nombre réel :  
```bash  
##!/bin/bash
function is_number {
re='^[+-]?[0-9]+([.][0-9]+)?$'
if ! [[ $1 =~ $re ]] ; then 
return 1 
else 
return 0
fi
}

if is_number $1 ; then
        echo 'Nombre' 
else echo 'Pas un Nombre'
fi

```


*Exercice 4 - Contrôle d'utilisateur*
------------
Écrivez un script qui vérifie l’existence d’un utilisateur dont le nom est donné en paramètre du script. Si le
script est appelé sans nom d’utilisateur, il affiche le message : ”Utilisation : nom_du_script nom_utilisateur”,
où nom_du_script est le nom de votre script récupéré automatiquement (si vous changez le nom de votre
script, le message doit changer automatiquement)

```bash  
#!/bin/bash

if [ -z $1 ];then
	echo "Utilisation : $0 nom_utilisateur"
else
	for user in $(cut -d: -f1 /etc/passwd)
	do
		if [ $user = $1 ];then
			echo "Nom d'utilisateur trouvé "
			exit
		fi
	done
	echo "Nom d'utilisateur non trouvé"
fi
```

*Exercice 5 - Factorielle*
------------
Écrivez un programme qui calcule la factorielle d’un entier naturel passé en paramètre (on supposera que l’utilisateur saisit toujours un entier naturel).
```bash  
#!/bin/bash

function factorielle()
{
  FACT=$FACT*$1
  $1="$1"-1
  if ! [ $1 = 1 ]; then
    fact $1
  fi
}

export FACT=1
fact $1
echo "$FACT"
```
*Exercice 6 - Le juste prix*
------------
Écrivez un script qui génère un nombre aléatoire entre 1 et 1000 et demande à l’utilisateur de le deviner.
Le programme écrira ”C’est plus !”, ”C’est moins !” ou ”Gagné !” selon les cas (vous utiliserez $RANDOM).
```bash  
#!/bin/bash

prix=$((RANDOM%1000)+1)

echo "Trouvez la bonne valeur (entre 1 et 1000) : "
while [ $var -ne $prix ]
do
read var
if [ $var -gt $prix ]; then
  echo 'C'est moins !'
fi
if [ $var -lt $prix ]; then
  echo 'C'est plus !'
fi
done

echo 'Gagné !'
```

*Exercice 7 - Statistiques*
------------

*Question 1 & 2 :* Écrivez un script qui prend en paramètres trois entiers (entre -100 et +100) et aﬀiche le min, le max et la moyenne. Vous pouvez réutiliser la fonction de l’exercice 3 pour vous assurer que les paramètres sont bien des entiers.  
Généralisez le programme à un nombre quelconque de paramètres (pensez à SHIFT)  

```bash  
#!/bin/bash
MIN=$1
MAX=$1
MOY=0
TOT=$#
for i in $(seq 1 $#)
do
    if [[ $1 -gt 100 || $1 -lt "-100" ]]; then
        echo "Paramètre éronné"
        exit 1
    else
    if [[ $1 -gt $MAX ]]; then
        MAX=$1
    elif [[ $1 -lt $MIN ]]; then
        MIN=$1
    fi
    MOY=$(($MOY+$1))
    shift
    fi
done
    MOY=$(($MOY/$TOT))
    echo "Valeur max: "$MAX
    echo "Valeur min: "$MIN
    echo "Valeur moyenne: "$MOY
```
*Question 3 :* Modifiez votre programme pour que les notes ne soient plus données en paramètres, mais saisies et
stockées au fur et à mesure dans un tableau  

```bash  
#!/bin/bash
MIN=$1
MAX=$1
MOY=0
TOT=$1
for i in $(seq 1 $1);do
read -p "Choisissez une valeur:" var
do
    if [[ var -gt 100 || var -lt "-100" ]]; then
        echo "Paramètre éronné"
        exit 1
    else
    if [[ var -gt $MAX ]]; then
        MAX=var
    elif [[ var -lt $MIN ]]; then
        MIN=var
    fi
    MOY=$(($MOY+var))
    shift
    fi
done
    MOY=$(($MOY/$TOT))
    echo "Valeur max: "$MAX
    echo "Valeur min: "$MIN
    echo "Valeur moyenne: "$MOY
```

