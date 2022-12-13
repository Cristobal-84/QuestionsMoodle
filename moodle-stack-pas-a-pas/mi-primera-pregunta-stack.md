# Ma première question STACK

## Fichier XML

{% file src="../.gitbook/assets/preguntas-DemoStack-12022021-Superficie estancia-20220420-2123.rar" %}
Compression au format .rar du fichier XML Moodle
{% endfile %}

## Description de la question

Il s'agit de préparer une question très simple qui demande de calculer l'aire d'une pièce rectangulaire (cela peut être une cuisine, une salle à manger, une chambre ou une terrasse).

* Les dimensions doivent être comprises entre 5 et 10 mètres.
* Pour l'instant, nous ne demanderons pas d'unités dans la réponse de l'utilisateur.
* Dans le relevé, les dimensions seront affichées au format $$\LaTeX$$ d'une part et en texte brut d'autre part.

## Explication étape par étape de la question

### Variables

![](<../.gitbook/assets/image (56).png>)

{% hint style="info" %}
L'un des points forts des questions STACK est la possibilité de **randomisation**.

Sur [cette page](https://github.com/maths/moodle-qtype\_stack/blob/master/doc/en/CAS/Random.md) se trouvent les fonctions dont nous disposons pour randomiser.
{% endhint %}

Dans ce cas, nous avons utilisé la fonction`rand(lista)` pour choisir au hasard un élément de la liste et la fonction `rand_with_step(límite inferior, límite superior, paso)` pour choisir un nombre compris entre 5 et 10 (les deux inclus) et avancer de un en un.

Les caractères spéciaux (ou avec l'accent dans "habitación") doivent être écrits comme suit :

![](<../.gitbook/assets/image (2).png>)

Comme dernière variable, nous avons choisi tans1 ("teacher answer 1") qui stocke la valeur de la bonne réponse à la question.

{% hint style="info" %}
Dans les exemples de questions (qui se trouvent dans le [cours de démonstration STACK](https://github.com/maths/moodle-qtype\_stack/blob/master/samplequestions/STACK-demo.mbz), qui peut être téléchargé et restauré sur n'importe quelle installation Moodle), TANS est souvent utilisé pour la réponse de l'enseignant.

Dans le cas où nous utilisons des questions préalablement préparées pour créer de nouvelles questions, cela peut faire gagner du temps d'utiliser des variables avec des noms génériques pour les réponses finales puisque, dans la vérification des réponses et dans le feedback, la "bonne réponse" sera utilisée plusieurs fois.
{% endhint %}

## Enoncé

![](<../.gitbook/assets/image (119).png>)

{% hint style="success" %}
Pour écrire des variables dans l'instruction, nous pouvons utiliser :

* `{#nombre_variable#}` affichera la valeur de la variable sous forme de texte brut. Si la variable est une chaîne de texte, elle sera affichée sous forme de texte brut entre guillemets.
* `{@nombre_variable@}` affichera la valeur de la variable sous forme de code $$\LaTeX$$. Si la variable est une chaîne de texte, elle sera affichée sous forme de texte brut sans les guillemets.
{% endhint %}

{% hint style="danger" %}
TRÈS IMPORTANT

Chaque fois que nous voulons inclure un **champ de réponse** (un espace pour que l'utilisateur réponde), nous devons **TOUJOURS introduire LES DEUX** champs suivants :

* `[[input:nombre_campo]]` où nous voulons que le champ de réponse apparaisse,
* `[[validation:nombre_campo]]` où nous voulons que la validation de la réponse apparaisse. Notez qu'il s'agit d'une validation du format de la réponse (décimal/non décimal, numérique, expression algébrique...).

Là où nous voulons que la correction de la validité de la réponse de l'utilisateur apparaisse (généralement en la comparant à la bonne réponse) nous devrons introduire :

* `[[feedback:nombre_feedback]]`
{% endhint %}

{% hint style="warning" %}
Veuillez noter que :

* Nous pouvons inclure plus d'un champ de **feedback** pour un champ de réponse (input).
* Il peut y avoir des champs de réponse sans **feedback**.
* Il peut y avoir un seul **feedback** pour plusieurs champs de réponse.
{% endhint %}

![Résultat que l'utilisateur verrait](<../.gitbook/assets/image (38).png>)

## Annotation

Dans les questions qui incluent des variables aléatoires, Moodle STACK nous demandera de remplir le champ annotation de question avant de pouvoir sauvegarder la question.

Le but d'une annotation de question est de distinguer les différentes versions aléatoires d'une question. L'annotation de question doit donc être un texte **différente pour chacune des variantes de la question**. STACK considèrera que deux versions d'une question sont égales si, et seulement si, leurs annotations de question sont égales.

{% hint style="info" %}
Il est pratique de définir **des annotations de question qui nous aident à identifier facilement à quelle variante de chaque question elles correspondent** puisque, lorsque nous afficherons les variantes de chaque question, la façon de les identifier se fera par l'annotation de question.
{% endhint %}

![](<../.gitbook/assets/image (111).png>)

{% hint style="success" %}
Les annotations de questions devront inclure certaines des variables aléatoires que nous avons utilisées.
{% endhint %}

## Fonctionnalités du champ de saisie (Input)

![](<../.gitbook/assets/image (59).png>)

{% hint style="info" %}
Pour **chacun des input** que nous avons dans la question, nous aurons un onglet **Input** pour configurer ledit champ de saisie.
{% endhint %}

Voyons comment configurer les champs les plus importants :

* **Type d'input :** vous permet de choisir le type d'entrée que nous attendons de l'utilisateur. Documentation détaillée [ici](https://github.com/maths/moodle-qtype\_stack/blob/master/doc/en/Authoring/Inputs.md).

Ceux que nous utiliserons généralement sont :

![](../.gitbook/assets/image.png)

1. Forme algébrique : Prend en charge les expressions algébriques composées de nombres et de variables. Bien qu'on ne s'attende pas à des variables, c'est aussi valable pour les nombres.
2. Numerical : seules les réponses numériques seront valides. Il prend également en charge les opérations sur les nombres dont le résultat est un nombre. Il peut être configuré pour prendre en charge certains types de nombres et des non-opérations. Documentation détaillée [ici](https://github.com/maths/moodle-qtype\_stack/blob/master/doc/en/Authoring/Numerical\_input.md).

* **Modèle de réponse** : nous inclurons ici une éventuelle réponse correcte à la question. C'est la valeur qui est saisie comme bonne réponse en cliquant sur le bouton "Remplir les réponses correctes" depuis l'aperçu de la question. CE N'EST PAS LA VALEUR UTILISÉE POUR DÉCIDER SI LA RÉPONSE DE L'UTILISATEUR EST CORRECTE OU NON.
* **Interdire les nombres à virgule** : si elle est marquée comme Oui, la réponse de l'utilisateur ne pourra pas inclure de nombres à virgule (nombres décimaux) et seules les réponses avec des **nombres fractionnaires** seront valides. TRÈS UTILE EN MATHS ÉLÉMENTAIRES DANS LESQUELS NOUS NE VOULONS PAS DE RÉSULTATS DÉCIMAUX.
* **Imposer des fractions réduites** : force les fractions à être simplifiées. Sinon, il donne un avertissement qu'ils devraient l'être. AU LIEU D'UTILISER CETTE OPTION, IL SERA NORMALEMENT PRÉFÉRABLE D'ÉVALUER LA SIMPLIFICATION LORSQUE NOUS NOTONS LA QUESTION.
* **Vérifier le type de la réponse** : Si activé, affiche un message d'erreur à l'utilisateur au cas où l'expression saisie n'est pas du type attendu et défini dans le type de variable qui est la réponse du modèle.
* **Demander à l'étudiant de vérifier** et **Afficher la validation** : permet de montrer à l'utilisateur sa réponse dans un format commun. Par exemple, les fractions, les puissances et les racines sont affichées de manière standard. NORMALEMENT, LA VALIDATION COMPACTE SERA LA PLUS UTILISÉE CAR ELLE S'AFFICHE SUR LA MÊME LIGNE QUE LA RÉPONSE ET EST BEAUCOUP PLUS SIMPLE.

![Exemple de validation incluant la liste des variables](<../.gitbook/assets/image (63).png>)

![Exemple de validation compacte](<../.gitbook/assets/image (79).png>)

## Arbre des réponses potentielles

La documentation concernant cette partie de la question peut être trouvée [ici](https://github.com/maths/moodle-qtype\_stack/blob/master/doc/en/Authoring/Feedback.md).

![](<../.gitbook/assets/image (40).png>)

{% hint style="info" %}
Ce sera l'endroit où :

* Nous ferons toutes les vérifications que nous souhaitons à la réponse de l'utilisateur.
* Nous attribuerons le score que nous considérons en fonction du résultat de ces contrôles.
* Nous donnerons des commentaires à l'utilisateur en fonction du résultat des vérifications que nous effectuons.
{% endhint %}

Dans notre question, nous vérifions seulement que la réponse de l'utilisateur (Sans, que nous avons appelée dans ce cas ans1) est algébriquement équivalente à la bonne réponse (Tans, que nous avons appelée dans ce cas tans1). Si c'est le cas, 100 % du score (1) est attribuée et sinon, un score de zéro est attribuée. Nous n'offrons pas de commentaires.

Un champ important à configurer est le **PRT Feedback Style**, car il déterminera quelles informations sont proposées à l'utilisateur après la correction. Pour l'instant, nous allons le laisser en Standard. Nous verrons plus tard, dans d'autres questions, quels types de feedback nous pouvons utiliser.

## Résultat de la question

![](<../.gitbook/assets/image (5).png>)

## Déploiement de variantes et de tests

![](<../.gitbook/assets/image (96).png>)

{% hint style="info" %}
Lorsque les questions incluent des variables aléatoires, Moodle offre la possibilité (et recommande fortement) de générer des **variantes**, qui sont chaque version de la question qui sera montrée aux étudiants.
{% endhint %}

Le déploiement de variantes nous permettra de **contrôler le caractère aléatoire** généré dans les questions, puisque nous pourrons éliminer les variantes dont la combinaison de variables aléatoires ne nous convient pas (valeurs répétées, résultats fractionnaires indésirables...) .

![](<../.gitbook/assets/image (57).png>)

Dans notre question, il y a potentiellement 4 types de pièces pour 5 largeurs différentes par 5 longueurs différentes, soit un total de 100 variantes différentes. Nous en déploierons 30.

![](<../.gitbook/assets/image (49).png>)

Ici, nous pouvons éliminer les variantes que nous "n'aimons pas" en cliquant sur la corbeille.

Pour terminer la question, il nous suffit de générer un **cas de test**.

{% hint style="info" %}
Les **cas de test** sont utilisés pour identifier les variantes qui ne fonctionnent pas correctement.
{% endhint %}

Dans ce cas, nous allons générer un cas de test élémentaire dans lequel on vérifie que si la réponse de l'utilisateur (ans1) est égale à la réponse modèle (tans1) un score de 100% de la valeur de la question est attribué.

![](<../.gitbook/assets/image (93).png>)

Avec cela, sur l'écran où vous pouvez voir les variantes déployées, vous pouvez effectuer le test sur toutes les variantes (Run all tests on deployed variants) :

![](<../.gitbook/assets/image (48).png>)
