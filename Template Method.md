Le modèle de conception de méthode de modèle consiste à définir un algorithme comme un squelette d'opérations et à laisser les détails à implémenter par les classes enfants. La structure globale et la séquence de l'algorithme sont conservées par la classe parente.  
Modèle signifie un format prédéfini comme les modèles HTML qui ont un format prédéfini fixe. De même, dans le modèle de méthode de modèle, nous avons une méthode de structure prédéfinie appelée méthode de modèle qui se compose d'étapes. Ces étapes peuvent être une méthode abstraite qui sera implémentée par ses sous-classes.

Ce modèle de conception comportementale est l'un des plus faciles à comprendre et à implémenter. Ce modèle de conception est couramment utilisé dans le développement de framework. Cela permet également d'éviter la duplication de code.

[![](https://media.geeksforgeeks.org/wp-content/uploads/claasDia.jpg)](https://media.geeksforgeeks.org/wp-content/uploads/claasDia.jpg)  
_Source:_ [Wikipédia](https://en.wikipedia.org/wiki/Template_method_pattern)

-   **AbstractClass** contient le templateMethod () qui doit être rendu final afin qu'il ne puisse pas être remplacé. Cette méthode de modèle utilise d'autres opérations disponibles afin d'exécuter l'algorithme mais est découplée pour l'implémentation réelle de ces méthodes. Toutes les opérations utilisées par cette méthode de modèle sont rendues abstraites, leur implémentation est donc reportée aux sous-classes.
-   **ConcreteClass** implémente toutes les opérations requises par le templateMethod qui ont été définies comme abstraites dans la classe parent. Il peut y avoir de nombreuses ConcreteClasses différentes.

**Voyons un exemple du modèle de méthode de modèle.**

_filter_none_

_Éditer_

_play_arrow_

_luminosité_4_

`abstract` `class` `OrderProcessTemplate`

`{`

`public` `boolean` `isGift;`

`public` `abstract` `void` `doSelect();`

`public` `abstract` `void` `doPayment();`

`public` `final` `void` `giftWrap()`

`{`

`try`

`{`

`System.out.println(``"Gift wrap successful"``);`

`}`

`catch` `(Exception e)`

`{`

`System.out.println(``"Gift wrap unsuccessful"``);`

`}`

`}`

`public` `abstract` `void` `doDelivery();`

`public` `final` `void` `processOrder(``boolean` `isGift)`

`{`

`doSelect();`

`doPayment();`

`if` `(isGift) {`

`giftWrap();`

`}`

`doDelivery();`

`}`

`}`

`class` `NetOrder` `extends` `OrderProcessTemplate`

`{`

`@Override`

`public` `void` `doSelect()`

`{`

`System.out.println(``"Item added to online shopping cart"``);`

`System.out.println(``"Get gift wrap preference"``);`

`System.out.println(``"Get delivery address."``);`

`}`

`@Override`

`public` `void` `doPayment()`

`{`

`System.out.println`

`(``"Online Payment through Netbanking, card or Paytm"``);`

`}`

`@Override`

`public` `void` `doDelivery()`

`{`

`System.out.println`

`(``"Ship the item through post to delivery address"``);`

`}`

`}`

`class` `StoreOrder` `extends` `OrderProcessTemplate`

`{`

`@Override`

`public` `void` `doSelect()`

`{`

`System.out.println(``"Customer chooses the item from shelf."``);`

`}`

`@Override`

`public` `void` `doPayment()`

`{`

`System.out.println(``"Pays at counter through cash/POS"``);`

`}`

`@Override`

`public` `void` `doDelivery()`

`{`

`System.out.println(``"Item delivered to in delivery counter."``);`

`}`

`}`

`class` `TemplateMethodPatternClient`

`{`

`public` `static` `void` `main(String[] args)`

`{`

`OrderProcessTemplate netOrder =` `new` `NetOrder();`

`netOrder.processOrder(``true``);`

`System.out.println();`

`OrderProcessTemplate storeOrder =` `new` `StoreOrder();`

`storeOrder.processOrder(``true``);`

`}`

`}`

Production :

  

  

Article ajouté au panier d'achat en ligne Obtenez la préférence d'emballage cadeau Obtenez l'adresse de livraison. Paiement en ligne via Netbanking, carte ou Paytm Emballage cadeau réussi Expédier l'article par la poste à l'adresse de livraison
 Le client choisit l'article dans l'étagère. Paye au comptoir en espèces / POS Emballage cadeau réussi Article livré au comptoir de livraison.

L'exemple ci-dessus traite du flux de traitement des commandes. La classe OrderProcessTemplate est une classe abstraite contenant le squelette de l'algorithme. Comme indiqué sur la note, processOrder () est la méthode qui contient les étapes du processus. Nous avons deux sous-classes NetOrder et StoreOrder qui ont les mêmes étapes de traitement des commandes.

Ainsi, l'algorithme global utilisé pour traiter une commande est défini dans la classe de base et utilisé par les sous-classes. Mais la manière dont les opérations individuelles sont effectuées varie en fonction de la sous-classe.

**Quand utiliser la méthode de modèle**

La méthode de modèle est utilisée dans les frameworks, où chacun implémente les parties invariantes de l'architecture d'un domaine, laissant des «espaces réservés» pour les options de personnalisation.

La méthode du modèle est utilisée pour les raisons suivantes:

-   Laisser les sous-classes implémenter un comportement variable (via le remplacement de méthode)
-   Évitez la duplication dans le code, la structure générale du flux de travail est implémentée une fois dans l'algorithme de la classe abstraite et les variations nécessaires sont implémentées dans les sous-classes.
-   Contrôle à quels points le sous-classement est autorisé. Contrairement à un simple remplacement polymorphe, où la méthode de base serait entièrement réécrite, permettant une modification radicale du flux de travail, seuls les détails spécifiques du flux de travail sont autorisés à changer.

**Référence:**  
[Wikipedia](https://en.wikipedia.org/wiki/Template_method_pattern)
