Le modèle de constructeur vise à «séparer la construction d'un objet complexe de sa représentation afin que le même processus de construction puisse créer différentes représentations.» Il est utilisé pour construire un objet complexe étape par étape et l'étape finale retournera l'objet. Le processus de construction d'un objet doit être générique afin de pouvoir être utilisé pour créer différentes représentations du même objet.

**Diagramme UML du modèle de conception du générateur**

![](https://media.geeksforgeeks.org/wp-content/uploads/uml-of-builedr.jpg)  
Source: [Wikipédia](https://en.wikipedia.org/wiki/Builder_pattern)

-   **Produit -** La classe de produit définit le type de l'objet complexe qui doit être généré par le modèle de générateur.
-   **Builder -** Cette classe de base abstraite définit toutes les étapes à suivre pour créer correctement un produit. Chaque étape est généralement abstraite car la fonctionnalité réelle du constructeur est réalisée dans les sous-classes concrètes. La méthode GetProduct est utilisée pour renvoyer le produit final. La classe constructeur est souvent remplacée par une interface simple.
-   **ConcreteBuilder -** Il peut y avoir n'importe quel nombre de classes de générateur concret héritant de Builder. Ces classes contiennent la fonctionnalité permettant de créer un produit complexe particulier.
-   **Director -** La classe Director contrôle l'algorithme qui génère l'objet produit final. Un objet directeur est instancié et sa méthode Construct est appelée. La méthode comprend un paramètre pour capturer l'objet de construction concret spécifique qui doit être utilisé pour générer le produit. Le directeur appelle ensuite les méthodes du constructeur de béton dans le bon ordre pour générer l'objet produit. À la fin du processus, la méthode GetProduct de l'objet générateur peut être utilisée pour renvoyer le produit.

**Voyons un exemple de modèle de conception de constructeur:**

Prenons la construction d'une maison. La maison est le produit final (objet) qui doit être retourné en tant que résultat du processus de construction. Il comportera de nombreuses étapes comme la construction du sous-sol, la construction des murs, etc. Enfin, tout l'objet home est renvoyé. Ici, en utilisant le même processus, vous pouvez construire des maisons avec des propriétés différentes.

  

  

_filter_none_

_Éditer_

_play_arrow_

_luminosité_4_

`interface` `HousePlan`

`{`

`public` `void` `setBasement(String basement);`

`public` `void` `setStructure(String structure);`

`public` `void` `setRoof(String roof);`

`public` `void` `setInterior(String interior);`

`}`

`class` `House` `implements` `HousePlan`

`{`

`private` `String basement;`

`private` `String structure;`

`private` `String roof;`

`private` `String interior;`

`public` `void` `setBasement(String basement)`

`{`

`this``.basement = basement;`

`}`

`public` `void` `setStructure(String structure)`

`{`

`this``.structure = structure;`

`}`

`public` `void` `setRoof(String roof)`

`{`

`this``.roof = roof;`

`}`

`public` `void` `setInterior(String interior)`

`{`

`this``.interior = interior;`

`}`

`}`

`interface` `HouseBuilder`

`{`

`public` `void` `buildBasement();`

`public` `void` `buildStructure();`

`public` `void` `bulidRoof();`

`public` `void` `buildInterior();`

`public` `House getHouse();`

`}`

`class` `IglooHouseBuilder` `implements` `HouseBuilder`

`{`

`private` `House house;`

`public` `IglooHouseBuilder()`

`{`

`this``.house =` `new` `House();`

`}`

`public` `void` `buildBasement()`

`{`

`house.setBasement(``"Ice Bars"``);`

`}`

`public` `void` `buildStructure()`

`{`

`house.setStructure(``"Ice Blocks"``);`

`}`

`public` `void` `buildInterior()`

`{`

`house.setInterior(``"Ice Carvings"``);`

`}`

`public` `void` `bulidRoof()`

`{`

`house.setRoof(``"Ice Dome"``);`

`}`

`public` `House getHouse()`

`{`

`return` `this``.house;`

`}`

`}`

`class` `TipiHouseBuilder` `implements` `HouseBuilder`

`{`

`private` `House house;`

`public` `TipiHouseBuilder()`

`{`

`this``.house =` `new` `House();`

`}`

`public` `void` `buildBasement()`

`{`

`house.setBasement(``"Wooden Poles"``);`

`}`

`public` `void` `buildStructure()`

`{`

`house.setStructure(``"Wood and Ice"``);`

`}`

`public` `void` `buildInterior()`

`{`

`house.setInterior(``"Fire Wood"``);`

`}`

`public` `void` `bulidRoof()`

`{`

`house.setRoof(``"Wood, caribou and seal skins"``);`

`}`

`public` `House getHouse()`

`{`

`return` `this``.house;`

`}`

`}`

`class` `CivilEngineer`

`{`

`private` `HouseBuilder houseBuilder;`

`public` `CivilEngineer(HouseBuilder houseBuilder)`

`{`

`this``.houseBuilder = houseBuilder;`

`}`

`public` `House getHouse()`

`{`

`return` `this``.houseBuilder.getHouse();`

`}`

`public` `void` `constructHouse()`

`{`

`this``.houseBuilder.buildBasement();`

`this``.houseBuilder.buildStructure();`

`this``.houseBuilder.bulidRoof();`

`this``.houseBuilder.buildInterior();`

`}`

`}`

`class` `Builder`

`{`

`public` `static` `void` `main(String[] args)`

`{`

`HouseBuilder iglooBuilder =` `new` `IglooHouseBuilder();`

`CivilEngineer engineer =` `new` `CivilEngineer(iglooBuilder);`

`engineer.constructHouse();`

`House house = engineer.getHouse();`

`System.out.println(``"Builder constructed: "``+ house);`

`}`

`}`

Production :

Constructeur construit: House @ 6d06d69c 

**Avantages du modèle de conception de constructeur**

-   Les paramètres du constructeur sont réduits et sont fournis dans des appels de méthode hautement lisibles.
-   Le modèle de conception du générateur aide également à minimiser le nombre de paramètres dans le constructeur et il n'est donc pas nécessaire de transmettre null pour les paramètres facultatifs au constructeur.
-   L'objet est toujours instancié dans un état complet
-   Les objets immuables peuvent être construits sans beaucoup de logique complexe dans le processus de création d'objets.

**Inconvénients du modèle de conception de constructeur**

-   Le nombre de lignes de code augmente au moins pour doubler dans le modèle du constructeur, mais l'effort est payant en termes de flexibilité de conception et de code beaucoup plus lisible.
-   Nécessite la création d'un ConcreteBuilder distinct pour chaque type de produit différent.
