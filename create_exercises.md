# Pour aller plus loin : créez votre propres exercices

## Structure des exercices existants et limites

Aujourd'hui les exercices sont organisés autour de 28 notions, elle-même regroupées en 4 catégories :

**Feu - Nombres et Calculs**
> - Nombres entiers
> - Nombres décimaux
> - Multiples et diviseurs
> - Manipulation de fractions
> - Manipuler les grands nombres
> - Divisions Euclidiennes
> - Interprétation de problèmes

**Eau - Gestion de données et fonctions**
> - Proportionnalité
> - Pourcentages
> - Lecture de tableaux
> - Lecture de graphiques
> - Diagrammes radar
> - Diagrammes en barres
> - Diagrammes circulaires

**Vent - Espace et Géométrie**
> - Symétrie axiale
> - Droites, segments et demi-droites
> - Les angles
> - Les cercles
> - Les quadrilatères
> - Reconnaissance de triangles
> - Médiatrices et hauteurs

**Terre - Grandeurs et mesures**
> - Les longueurs
> - Les masses
> - Les durées
> - Les prix
> - Les périmètres
> - Les aires
> - Les volumes

Par ailleurs chaque notion possède 4 niveaux de difficulté (de 1 à 4) et chaque niveau possède un nombre variable d'exercices (de 3 à 6).

## Créer un nouvel exercice

Il est bien plus facile de rajouter un exercice dans une notion existante que de créer une nouvelle notion. Nous ne détaillerons donc ici que la **création d'exercices au sein une notion déjà existante**.

Prenons un exemple pour rendre le guide plus concret. Mettons que j'ai envie de créer un nouvel exercice au sein de la notion **Les périmètres** se situant dans la catégorie **Terre - Grandeurs et mesures**.

Demandez à votre administrateur web un accès au serveur où est stocké le code de Navadra. Une fois dans le répertoire du code naviguez dans le répertoire **generators/challenges**.
Vous verrez ici les différentes catégories mentionnées précédemment :
> - earth : Terre - Grandeurs et mesures
> - fire : Feu - Nombres et Calculs
> - water : Eau - Gestion de données et fonctions
> - wind : Vent - Espace et Géométrie
> - base : quelques exercices de calcul mental qui ne servent que pour le tutoriel

Dans notre exemple, ouvrez le dossier **earth**. 
Les dossiers qui apparaissent correspondent au notion de la catégorie Terre - Grandeurs et mesures :
> - lengths : Les longueurs
> - weights : Les masses
> - durations : Les durées
> - prices : Les prix
> - perimeters : Les périmètres
> - areas : Les aires
> - volumes : Les volumes

Dans notre exemple, ouvrez le dossier **perimeters**. 
Les dossiers qui apparaissent correspondent au niveau de difficulté estimé de l'exercice au sein de la notion "Périmètres". Il y a toujours 4 niveaux de difficulté (de 1 à 4). Supposons que vous souhaitiez rajouter un exercice de difficulté **2**. Vous ouvrez donc le dossier 2.

Les fichiers qui apparaissent correspondent aux 6 exercices de difficulté 2 au sein de la notion "Périmètres".
Vous pouvez en créer un 7° en faisant un copier-collé d'un exercice existant et en le renommant "earth_perimeters_2_7.json".

Nous verrons dans la rubrique suivante comment paramètrer cet exercice. En attendant, il reste une dernière manipulation à faire pour que ce nouvel exercice soit pris en compte par notre algorithme d'apprentissage adaptatif :
> - Rendez vous dans le répertoire webroot/js/utils/challenge_choice.js
> - Au début du fichier une variable "exercises" définit le nombre d'exercices contenus dans chaque notion.
> - Repérez la ligne concernant la notion "Périmètres" (perimeters). Elle se situe à la ligne n°160 du fichier.

Il nous reste plus qu'à remplacer la ligne correspondant à la difficulté 2. 
Changez :
"perimeters" : {
	"1" : 5,
	"2" : **6**,
	"3" : 6,
	"4" : 4
}
Par :
"perimeters" : {
	"1" : 5,
	"2" : **7**,
  "3" : 6,
	"4" : 4
}

Sauvegardez le fichier.
Vous avez bel et bien rajouté un nouvel exercice mais qui est pour l'instant une copie conforme d'un exercice déjà existant.
Dans la rubrique suivante vous apprendrez à paramétrer ce nouvel exercice.

## Configurer votre nouvel exercice

Le plus simple pour paramétrer un nouvel exercice est de s'inspirer d'un exercice assez semblable.
Pour cela, vous pouvez vous connecter **avec votre compte Prof** sur Navadra puis vous rendre sur la page :

www.VOTRE_NOM_DE_DOMAINE/app/controllers/test_challenge.php

Remarquez en bas à droite de la page les différents champs déroulant. Vous pouvez sélectionner une catégorie, une notion, un niveau de difficulté et un numéro d'exercice pour tester l'exercice de votre choix.

Supposez que votre nouvel exercice s'inspire du 1° exercice du niveau 2 de périmètre et que vous souhaitiez consulter cet exercice. Il vous suffit de sélectionner dans l'ordre :
> - Terre
> - Périmètres
> - 2 (niveau de difficulté)
> - 1 (numéro de l'exercice)

Vous pourrez ainsi vous entraîner en boucle sur des exemples de cet exercice.

Il ne vous reste maintenant plus qu'à adapter votre nouveau fichier "earth_perimeters_2_7.json" en vous inspirant de "earth_perimeters_2_1.json".

Nous n'avons malheureusement pas de documentation exhaustive concernant toutes les possibilités de paramétrage des exercices (c'est pour cela que nous recommandons de s'inspirer d'exercices existants) mais voici quelques explications sur les différents paramètres du fichier json :
> - **timer** : le temps de base dont dispose le joueur pour résoudre l'exercice (en millisecondes). Ce temps de base s'adaptera par la suite à chaque joueur.
> - **type** : cela définit le type d'exercice (1 = champ de texte, 2 = QCM (une seule réponse), 3 = QCM (plusieurs réponses), 4 = phrases à trou, 5 = exercices de géométrie interactifs).
> - **question** : la question posée à l'utilisateur (les balises HTML sont acceptées).
> - **view** : paramètre facultatif, dans cet exemple définit un repère orthonormé allant de -20 à 20 sur les x et de -10 à 10 sur les y.
> - **answer** : la/une bonne réponse qui sera affichée à l'utilisateur.
> - **criteria** : le(s) critère(s) qu'utilisera le programme pour évaluer si une réponse est bonne ou mauvaise.
> - **type_answer** : définit si une ou plusieurs réponses sont attendues.
> - **var** : les différentes variables utilisées dans l'exercice. La plupart des variables sont définies aléatoirement entre une borne inférieure et une borne supérieure. Par exemple "random(-7,-1)" renverra un nombre aléatoire compris entre -7 et -1.
> - **hint** : ce qui sera affiché à l'utilisateur s'il clique sur "Rappel cours" lorsqu'il répond faux à cet exercice. Ce paramètre accepte les balises HTML.

Une fois que vous avez fini de paramétrer votre nouvel exercice, sauvegardez le sur le serveur de votre établissement.

Pour le tester il suffira de vous rendre à nouveau sur :

www.VOTRE_NOM_DE_DOMAINE/app/controllers/test_challenge.php

Puis de sélectionner : 
> - Terre
> - Périmètres
> - 2 (niveau de difficulté)
> - 7 (numéro de l'exercice)

Bravo, vous avez créé votre premier exercice et il sera maintenant accessible pour vos élèves !

**Important** : Si vous pensez être amené à créer des exercices, il sera bien plus pratique de demander à votre administrateur web un environnement de pré-production pour pouvoir créer et tester vos nouveaux exercices bien plus rapidement. Une fois satisfait, il vous suffira de passer toutes ces modifications d'un coup sur le serveur de votre établissement et vous n'aurez aucun aller-retour à faire.