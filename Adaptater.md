Ce modèle est facile à comprendre car le monde réel regorge d'adaptateurs. Par exemple, considérez un adaptateur USB vers Ethernet. Nous en avons besoin lorsque nous avons une interface Ethernet à une extrémité et USB à l'autre. Puisqu'ils sont incompatibles les uns avec les autres. nous utilisons un adaptateur qui convertit l'un en l'autre. Cet exemple est assez analogue aux adaptateurs orientés objet. Dans la conception, les adaptateurs sont utilisés lorsque nous avons une classe (Client) qui attend un certain type d'objet et que nous avons un objet (Adaptee) offrant les mêmes fonctionnalités mais exposant une interface différente.

Pour utiliser un adaptateur:

1.  Le client envoie une demande à l'adaptateur en appelant une méthode sur celui-ci à l'aide de l'interface cible.
2.  L'adaptateur traduit cette demande sur l'adaptee en utilisant l'interface adaptee.
3.  Le client reçoit les résultats de l'appel et n'est pas au courant de la présence de l'adaptateur.

**_Définition:_**

Le modèle d'adaptateur convertit l'interface d'une classe en une autre interface attendue par les clients. L'adaptateur permet aux classes de travailler ensemble qui ne pourraient pas autrement en raison d'interfaces incompatibles.

**Diagramme de classe:**  
![ad3](https://media.geeksforgeeks.org/wp-content/uploads/classDiagram.jpg)

  

  

Le client ne voit que l'interface cible et non l'adaptateur. L'adaptateur implémente l'interface cible. L'adaptateur délègue toutes les demandes à Adaptee.

**Exemple:**

Supposons que vous ayez une classe Bird avec les méthodes fly () et makeSound (). Et aussi une classe ToyDuck avec la méthode squeak (). Supposons que vous manquiez d'objets ToyDuck et que vous souhaitiez utiliser des objets Bird à leur place. Les oiseaux ont des fonctionnalités similaires mais implémentent une interface différente, nous ne pouvons donc pas les utiliser directement. Nous allons donc utiliser un modèle d'adaptateur. Ici, notre client serait ToyDuck et l'adapté serait Bird.

Voici l'implémentation Java de celui-ci.

_filter_none_

_Éditer_

_play_arrow_

_luminosité_4_

`// Java implementation of Adapter pattern`

`interface` `Bird`

`{`

`// birds implement Bird interface that allows`

`// them to fly and make sounds adaptee interface`

`public` `void` `fly();`

`public` `void` `makeSound();`

`}`

`class` `Sparrow` `implements` `Bird`

`{`

`// a concrete implementation of bird`

`public` `void` `fly()`

`{`

`System.out.println(``"Flying"``);`

`}`

`public` `void` `makeSound()`

`{`

`System.out.println(``"Chirp Chirp"``);`

`}`

`}`

`interface` `ToyDuck`

`{`

`// target interface`

`// toyducks dont fly they just make`

`// squeaking sound`

`public` `void` `squeak();`

`}`

`class` `PlasticToyDuck` `implements` `ToyDuck`

`{`

`public` `void` `squeak()`

`{`

`System.out.println(``"Squeak"``);`

`}`

`}`

`class` `BirdAdapter` `implements` `ToyDuck`

`{`

`// You need to implement the interface your`

`// client expects to use.`

`Bird bird;`

`public` `BirdAdapter(Bird bird)`

`{`

`// we need reference to the object we`

`// are adapting`

`this``.bird = bird;`

`}`

`public` `void` `squeak()`

`{`

`// translate the methods appropriately`

`bird.makeSound();`

`}`

`}`

`class` `Main`

`{`

`public` `static` `void` `main(String args[])`

`{`

`Sparrow sparrow =` `new` `Sparrow();`

`ToyDuck toyDuck =` `new` `PlasticToyDuck();`

`// Wrap a bird in a birdAdapter so that it`

`// behaves like toy duck`

`ToyDuck birdAdapter =` `new` `BirdAdapter(sparrow);`

`System.out.println(``"Sparrow..."``);`

`sparrow.fly();`

`sparrow.makeSound();`

`System.out.println(``"ToyDuck..."``);`

`toyDuck.squeak();`

`// toy duck behaving like a bird`

`System.out.println(``"BirdAdapter..."``);`

`birdAdapter.squeak();`

`}`

`}`

Production:

Moineau... En volant Chirp Chirp ToyDuck ... Grincer BirdAdapter ... Chirp Chirp

**Explication:**  
Supposons que nous ayons un oiseau qui peut faire Sound (), et que nous ayons un canard jouet en plastique qui peut grincer (). Supposons maintenant que notre client modifie l'exigence et qu'il souhaite que le toyDuck produise un son que?  
La solution simple est que nous allons simplement changer la classe d'implémentation en la nouvelle classe d'adaptateur et dire au client de transmettre l'instance de l'oiseau (qui veut squeak ()) à cette classe.  
**Avant:** ToyDuck toyDuck = nouveau PlasticToyDuck ();  
**Après:** ToyDuck toyDuck = new BirdAdapter (moineau);  
Vous pouvez voir qu'en changeant une seule ligne, le toyDuck peut maintenant faire Chirp Chirp !!

**Object Adapter Vs Class Adapter**  
Le modèle d'adaptateur que nous avons implémenté ci-dessus est appelé Object Adapter Pattern car l'adaptateur contient une instance d'adaptee. Il existe également un autre type appelé Modèle d'adaptateur de classe qui utilise l'héritage au lieu de la composition, mais vous avez besoin d'un héritage multiple pour l'implémenter.  
Diagramme de classe du modèle d'adaptateur de classe:

![motif4](https://media.geeksforgeeks.org/wp-content/uploads/classDiagram33.jpg)

  

  

Ici, au lieu d'avoir un objet adapté à l'intérieur de l'adaptateur (composition) pour utiliser sa fonctionnalité, l'adaptateur hérite de l'adaptee.

Étant donné que l'héritage multiple n'est pas pris en charge par de nombreux langages, y compris java, et est associé à de nombreux problèmes, nous n'avons pas montré l'implémentation à l'aide du modèle d'adaptateur de classe.

**Avantages:**

-   Aide à atteindre la réutilisabilité et la flexibilité.
-   La classe client n'est pas compliquée par le fait d'avoir à utiliser une interface différente et peut utiliser le polymorphisme pour permuter entre différentes implémentations d'adaptateurs.

**Désavantages:**

-   Toutes les demandes sont transmises, il y a donc une légère augmentation des frais généraux.
-   Parfois, de nombreuses adaptations sont nécessaires le long d'une chaîne d'adaptateur pour atteindre le type requis.

**Références:**  
Head First Design Patterns (Book)
