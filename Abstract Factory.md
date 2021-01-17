Le modèle de conception de l'usine abstraite est l'un des modèles de création. Le motif de l'usine abstraite est presque similaire au [modèle d'usine](https://www.geeksforgeeks.org/design-patterns-set-2-factory-method/) est considéré comme une autre couche d'abstraction par rapport au modèle d'usine. Les modèles d'usine abstraite fonctionnent autour d'une super-usine qui crée d'autres usines.

L'implémentation de modèle de fabrique abstraite nous fournit un cadre qui nous permet de créer des objets qui suivent un modèle général. Ainsi, au moment de l'exécution, la fabrique abstraite est couplée à toute usine concrète souhaitée qui peut créer des objets du type souhaité.

**Voyons la représentation GOF de Abstract Factory Pattern:**  
![](https://media.geeksforgeeks.org/wp-content/uploads/AbstractFactoryPattern-2.png)  
_exemple de diagramme de classes UML pour le Abstract Factory Design Pattern._

-   **AbstractFactory** : déclare une interface pour les opérations qui créent des objets produits abstraits.
-   **ConcreteFactory** : implémente les opérations déclarées dans AbstractFactory pour créer des objets produit concrets.
-   **Produit** : définit un objet produit à créer par la fabrique de béton correspondante et implémente l'interface AbstractProduct.
-   **Client** : utilise uniquement les interfaces déclarées par les classes AbstractFactory et AbstractProduct.

Abstract Factory fournit des interfaces pour créer des familles d'objets liés ou dépendants sans spécifier leurs classes concrètes.

  

  

Le logiciel client crée une implémentation concrète de la fabrique abstraite et utilise ensuite les interfaces génériques pour créer les objets concrets qui font partie de la famille d'objets.  
Le client ne sait pas ou ne se soucie pas des objets concrets qu'il obtient de chacune de ces usines concrètes puisqu'il n'utilise que les interfaces génériques de ses produits.

Donc, avec cette idée de modèle Abstract Factory, nous allons maintenant essayer de créer un design qui facilitera la création d'objets associés.

**la mise en oeuvre**

Prenons un exemple, supposons que nous voulions construire une usine automobile mondiale. S'il s'agissait [d'un modèle de conception d'usine](https://www.geeksforgeeks.org/design-patterns-set-2-factory-method/) , il convenait à un seul emplacement. Mais pour ce modèle, nous avons besoin de plusieurs emplacements et de quelques modifications de conception critiques.

Nous avons besoin d'usines automobiles dans chaque endroit comme IndiaCarFactory, USACarFactory et DefaultCarFactory. Maintenant, notre application devrait être suffisamment intelligente pour identifier l'emplacement où elle est utilisée, nous devrions donc être en mesure d'utiliser l'usine automobile appropriée sans même savoir quelle implémentation d'usine automobile sera utilisée en interne. Cela nous évite également que quelqu'un appelle une mauvaise usine pour un emplacement particulier.

Ici, nous avons besoin d'une autre couche d'abstraction qui identifiera l'emplacement et utilisera en interne la mise en œuvre correcte de l'usine automobile sans même donner un seul indice à l'utilisateur. C'est exactement le problème, quel motif de fabrique abstraite est utilisé pour résoudre.

_filter_none_

_Éditer_

_play_arrow_

_luminosité_4_

`// Java Program to demonstrate the`

`// working of Abstract Factory Pattern`

`enum` `CarType`

`{`

`MICRO, MINI, LUXURY`

`}`

`abstract` `class` `Car`

`{`

`Car(CarType model, Location location)`

`{`

`this``.model = model;`

`this``.location = location;`

`}`

`abstract` `void` `construct();`

`CarType model =` `null``;`

`Location location =` `null``;`

`CarType getModel()`

`{`

`return` `model;`

`}`

`void` `setModel(CarType model)`

`{`

`this``.model = model;`

`}`

`Location getLocation()`

`{`

`return` `location;`

`}`

`void` `setLocation(Location location)`

`{`

`this``.location = location;`

`}`

`@Override`

`public` `String toString()`

`{`

`return` `"CarModel - "``+model +` `" located in "``+location;`

`}`

`}`

`class` `LuxuryCar` `extends` `Car`

`{`

`LuxuryCar(Location location)`

`{`

`super``(CarType.LUXURY, location);`

`construct();`

`}`

`@Override`

`protected` `void` `construct()`

`{`

`System.out.println(``"Connecting to luxury car"``);`

`}`

`}`

`class` `MicroCar` `extends` `Car`

`{`

`MicroCar(Location location)`

`{`

`super``(CarType.MICRO, location);`

`construct();`

`}`

`@Override`

`protected` `void` `construct()`

`{`

`System.out.println(``"Connecting to Micro Car "``);`

`}`

`}`

`class` `MiniCar` `extends` `Car`

`{`

`MiniCar(Location location)`

`{`

`super``(CarType.MINI,location );`

`construct();`

`}`

`@Override`

`void` `construct()`

`{`

`System.out.println(``"Connecting to Mini car"``);`

`}`

`}`

`enum` `Location`

`{`

`DEFAULT, USA, INDIA`

`}`

`class` `INDIACarFactory`

`{`

`static` `Car buildCar(CarType model)`

`{`

`Car car =` `null``;`

`switch` `(model)`

`{`

`case` `MICRO:`

`car =` `new` `MicroCar(Location.INDIA);`

`break``;`

`case` `MINI:`

`car =` `new` `MiniCar(Location.INDIA);`

`break``;`

`case` `LUXURY:`

`car =` `new` `LuxuryCar(Location.INDIA);`

`break``;`

`default``:`

`break``;`

`}`

`return` `car;`

`}`

`}`

`class` `DefaultCarFactory`

`{`

`public` `static` `Car buildCar(CarType model)`

`{`

`Car car =` `null``;`

`switch` `(model)`

`{`

`case` `MICRO:`

`car =` `new` `MicroCar(Location.DEFAULT);`

`break``;`

`case` `MINI:`

`car =` `new` `MiniCar(Location.DEFAULT);`

`break``;`

`case` `LUXURY:`

`car =` `new` `LuxuryCar(Location.DEFAULT);`

`break``;`

`default``:`

`break``;`

`}`

`return` `car;`

`}`

`}`

`class` `USACarFactory`

`{`

`public` `static` `Car buildCar(CarType model)`

`{`

`Car car =` `null``;`

`switch` `(model)`

`{`

`case` `MICRO:`

`car =` `new` `MicroCar(Location.USA);`

`break``;`

`case` `MINI:`

`car =` `new` `MiniCar(Location.USA);`

`break``;`

`case` `LUXURY:`

`car =` `new` `LuxuryCar(Location.USA);`

`break``;`

`default``:`

`break``;`

`}`

`return` `car;`

`}`

`}`

`class` `CarFactory`

`{`

`private` `CarFactory()`

`{`

`}`

`public` `static` `Car buildCar(CarType type)`

`{`

`Car car =` `null``;`

`// We can add any GPS Function here which`

`// read location property somewhere from configuration`

`// and use location specific car factory`

`// Currently I'm just using INDIA as Location`

`Location location = Location.INDIA;`

`switch``(location)`

`{`

`case` `USA:`

`car = USACarFactory.buildCar(type);`

`break``;`

`case` `INDIA:`

`car = INDIACarFactory.buildCar(type);`

`break``;`

`default``:`

`car = DefaultCarFactory.buildCar(type);`

`}`

`return` `car;`

`}`

`}`

`class` `AbstractDesign`

`{`

`public` `static` `void` `main(String[] args)`

`{`

`System.out.println(CarFactory.buildCar(CarType.MICRO));`

`System.out.println(CarFactory.buildCar(CarType.MINI));`

`System.out.println(CarFactory.buildCar(CarType.LUXURY));`

`}`

`}`

Production :

Connexion à Micro Car  CarModel - MICRO situé en INDE Connexion à une mini voiture CarModel - MINI situé en INDE Connexion à une voiture de luxe CarModel - LUXE situé en INDE

**Différence**

  

  

-   La principale différence entre une «méthode de fabrique» et une «fabrique abstraite» est que la méthode de fabrique est une méthode unique et une fabrique abstraite est un objet.
-   La méthode de fabrique n'est qu'une méthode, elle peut être remplacée dans une sous-classe, alors que la fabrique abstraite est un objet qui a plusieurs méthodes de fabrique dessus.
-   Le modèle de méthode d'usine utilise l'héritage et s'appuie sur une sous-classe pour gérer l'instanciation d'objet souhaitée.

**Avantages**

Ce modèle est particulièrement utile lorsque le client ne sait pas exactement quel type créer.

-   **Isolation des classes concrètes:** le modèle Abstract Factory vous aide à contrôler les classes d'objets qu'une application crée. Étant donné qu'une fabrique encapsule la responsabilité et le processus de création d'objets produit, elle isole les clients des classes d'implémentation. Les clients manipulent les instances via leurs interfaces abstraites. Les noms de classes de produits sont isolés dans la mise en œuvre de l'usine de béton; ils n'apparaissent pas dans le code client.
-   **Échange facile des familles de produits:** la classe d'une fabrique concrète n'apparaît qu'une seule fois dans une application, c'est là qu'elle est instanciée. Cela facilite la modification de l'usine de béton utilisée par une application. Il peut utiliser diverses configurations de produits simplement en changeant l'usine de béton. Parce qu'une usine abstraite crée une famille complète de produits, toute la famille de produits change en même temps.
-   **Promotion de la cohérence entre les produits:** lorsque les objets produit d'une famille sont conçus pour fonctionner ensemble, il est important qu'une application utilise des objets d'une seule famille à la fois. AbstractFactory rend cela facile à appliquer.n.

**Désavantages**

-   **Difficile de prendre en charge de nouveaux types de produits: l'** extension d'usines abstraites pour produire de nouveaux types de produits n'est pas facile. C'est parce que l'interface AbstractFactory corrige l'ensemble des produits qui peuvent être créés. La prise en charge de nouveaux types de produits nécessite d'étendre l'interface d'usine, ce qui implique de modifier la classe AbstractFactory et toutes ses sous-classes.

**REMARQUE: un**  
peu l'exemple ci-dessus est également basé sur le fonctionnement des cabines comme uber et ola à grande échelle.
