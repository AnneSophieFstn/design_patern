Pour comprendre le motif décorateur, considérons un scénario inspiré du livre «Head First Design Pattern». Supposons que nous construisions une application pour une pizzeria et que nous devions modéliser leurs classes de pizza. Supposons qu'ils offrent quatre types de pizzas à savoir Peppy Paneer, Farmhouse, Margherita et Chicken Fiesta. Au départ, nous utilisons simplement l'héritage et résumons les fonctionnalités communes d'une classe **Pizza** .

[![pizza1](https://media.geeksforgeeks.org/wp-content/uploads/decorePattern-1.png)](https://media.geeksforgeeks.org/wp-content/uploads/decorePattern-1.png)

Chaque pizza a un coût différent. Nous avons remplacé getCost () dans les sous-classes pour trouver le coût approprié. Supposons maintenant une nouvelle exigence, en plus d'une pizza, le client peut également demander plusieurs garnitures telles que la tomate fraîche, le paneer, le jalapeno, le Capsicum, le barbecue, etc. afin que le client puisse choisir la pizza avec garnitures et nous obtenons le coût total de la pizza et des garnitures que le client choisit.

Examinons différentes options.

**Option 1**  
Créez une nouvelle sous-classe pour chaque garniture avec une pizza. Le diagramme de classes ressemblerait à ceci:[![pizza2](https://media.geeksforgeeks.org/wp-content/uploads/decorePattern.png)](https://media.geeksforgeeks.org/wp-content/uploads/decorePattern.png)

  

  

Cela semble très complexe. Il y a beaucoup trop de cours et c'est un cauchemar d'entretien. Aussi, si nous voulons ajouter une nouvelle garniture ou une nouvelle pizza, nous devons ajouter autant de classes. C'est évidemment une très mauvaise conception.

**Option 2:**  
ajoutons des variables d'instance à la classe de base de pizza pour indiquer si chaque pizza a ou non une garniture. Le diagramme de classes ressemblerait à ceci:![pizza3](https://media.geeksforgeeks.org/wp-content/uploads/decorePattern-2.png)

Le getCost () de la superclasse calcule les coûts de toutes les garnitures tandis que celui de la sous-classe ajoute le coût de cette pizza spécifique.

// Exemple de getCost () dans la super classe public int getCost () { int totalToppingsCost = 0; si (hasJalapeno ()) totalToppingsCost + = jalapenoCost; si (hasCapsicum ()) totalToppingsCost + = capsicumCost;
 // de même pour les autres garnitures return totalToppingsCost; }

// Exemple de getCost () dans la sous-classe public int getCost () { // 100 pour Margherita et super.getCost () // pour les garnitures. retourne super.getCost () + 100; }

Cette conception semble bonne au début, mais examinons les problèmes qui y sont associés.

-   Les changements de prix dans les garnitures entraîneront une modification du code existant.
-   De nouvelles garnitures nous obligeront à ajouter de nouvelles méthodes et à modifier la méthode getCost () dans la superclasse.
-   Pour certaines pizzas, certaines garnitures peuvent ne pas convenir, mais la sous-classe en hérite.
-   Que faire si le client veut du double capsicum ou du double cheeseburst?

En bref, notre conception viole l'un des principes de conception les plus populaires - le principe [**ouvert-fermé**](https://en.wikipedia.org/wiki/Open/closed_principle) qui stipule que les classes doivent être ouvertes pour extension et fermées pour modification.
