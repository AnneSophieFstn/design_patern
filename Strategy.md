Comme toujours, nous allons apprendre ce modèle en définissant un problème et en utilisant un modèle de stratégie pour le résoudre. Supposons que nous construisions un jeu "Street Fighter". Pour simplifier, supposons qu'un personnage peut avoir quatre mouvements qui sont le coup de pied, le coup de poing, le roulis et le saut. Chaque personnage a des coups de pied et de poing, mais le roulis et le saut sont facultatifs. Comment modéliseriez-vous vos classes? Supposons initialement que vous utilisiez l'héritage et que vous supprimiez les fonctionnalités communes d'une classe **Fighter** et que vous laissiez d'autres personnages sous- classer la classe **Fighter** .

**La** classe **Fighter** aura l'implémentation par défaut des actions normales. Tout personnage avec un mouvement spécialisé peut remplacer cette action dans sa sous-classe. Le diagramme de classes serait le suivant:

![combattant1](https://media.geeksforgeeks.org/wp-content/uploads/classinh.jpg)

**Quels sont les problèmes avec la conception ci-dessus?**

Et si un personnage n'effectue pas de saut? Il hérite toujours du comportement de saut de la superclasse. Bien que vous puissiez remplacer jump pour ne rien faire dans ce cas, vous devrez peut-être le faire pour de nombreuses classes existantes et vous en occuper également pour les classes futures. Cela rendrait également la maintenance difficile. Nous ne pouvons donc pas utiliser l'héritage ici.

  

  

**Et une interface?**

Jetez un œil à la conception suivante:![combattant2](https://media.geeksforgeeks.org/wp-content/uploads/classas.jpg)

C'est beaucoup plus propre. Nous avons supprimé certaines actions (que certains personnages pourraient ne pas effectuer) de la classe **Fighter** et avons créé des interfaces pour elles. De cette façon, seuls les caractères censés sauter implémenteront le **JumpBehavior.**

**Quels sont les problèmes avec la conception ci-dessus?**

Le principal problème avec la conception ci-dessus est la réutilisation du code. Comme il n'y a pas d'implémentation par défaut du comportement jump and roll, nous pouvons avoir une duplicité de code. Vous devrez peut-être réécrire le même comportement de saut à plusieurs reprises dans de nombreuses sous-classes.

**Comment pouvons-nous éviter cela?**

Et si nous **faisions des** classes **JumpBehavior** et **RollBehavior** au lieu de l'interface? Eh bien, nous devrions utiliser l'héritage multiple qui n'est pas pris en charge dans de nombreuses langues en raison de nombreux problèmes qui lui sont associés.

  

  

_Ici, le modèle de stratégie vient à notre secours. Nous apprendrons quel est le modèle de stratégie et nous l'appliquerons ensuite pour résoudre notre problème._

**Définition:**

Wikipedia définit le modèle de stratégie comme:

_«Dans la programmation informatique, le **modèle de stratégie** (également appelé **modèle de politique** ) est un modèle de conception de logiciel qui permet de sélectionner le comportement d'un algorithme au moment de l'exécution. Le modèle de stratégie_

-   _définit une famille d'algorithmes,_
-   _encapsule chaque algorithme, et_
-   _rend les algorithmes interchangeables au sein de cette famille. »_

**Diagramme de _classe_ :![Sans titre](https://media.geeksforgeeks.org/wp-content/uploads/classss.jpg)**

Ici, nous nous appuyons sur la composition au lieu de l'héritage pour la réutilisation. **Le contexte** est composé d'une **stratégie** . Au lieu d'implémenter un comportement, le **contexte le** délègue à **Strategy** . Le contexte serait la classe qui exigerait des changements de comportement. Nous pouvons changer de comportement de manière dynamique. **La stratégie** est implémentée comme interface afin que nous puissions changer de comportement sans affecter notre contexte.

Nous aurons une meilleure compréhension du modèle de stratégie lorsque nous l'utiliserons pour résoudre notre problème.

**Avantages:**

1.  Une famille d'algorithmes peut être définie comme une hiérarchie de classes et peut être utilisée de manière interchangeable pour modifier le comportement de l'application sans changer son architecture.
2.  En encapsulant l'algorithme séparément, de nouveaux algorithmes conformes à la même interface peuvent être facilement introduits.
3.  L'application peut changer de stratégie au moment de l'exécution.
4.  La stratégie permet aux clients de choisir l'algorithme requis, sans utiliser une instruction «switch» ou une série d'instructions «if-else».
5.  Les structures de données utilisées pour implémenter l'algorithme sont complètement encapsulées dans des classes de stratégie. Par conséquent, l'implémentation d'un algorithme peut être modifiée sans affecter la classe Context.

**Désavantages:**

1.  L'application doit connaître toutes les stratégies pour sélectionner la bonne pour la bonne situation.
2.  Les classes de contexte et de stratégie communiquent normalement via l'interface spécifiée par la classe de base de stratégie abstraite. La classe de base de stratégie doit exposer l'interface pour tous les comportements requis, que certaines classes de stratégie concrètes peuvent ne pas implémenter.
3.  Dans la plupart des cas, l'application configure le contexte avec l'objet Stratégie requis. Par conséquent, l'application doit créer et gérer deux objets à la place d'un.

**_Références:_**

-   [Modèles de conception Head First](http://www.amazon.com/Head-First-Design-Patterns/dp/0596007124)
-   [http://wiki.expertiza.ncsu.edu/index.php/CSC/ECE_517_Fall_2007/wiki1b_8_sa](http://wiki.expertiza.ncsu.edu/index.php/CSC/ECE_517_Fall_2007/wiki1b_8_sa)
-   [https://en.wikipedia.org/wiki/Strategy_pattern](https://en.wikipedia.org/wiki/Strategy_pattern)
