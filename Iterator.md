Le modèle d'itérateur est un modèle de conception relativement simple et fréquemment utilisé. Il existe de nombreuses structures / collections de données disponibles dans toutes les langues. Chaque collection doit fournir un itérateur qui lui permet de parcourir ses objets. Cependant, ce faisant, il doit s'assurer qu'il n'expose pas son implémentation.  
Supposons que nous construisions une application qui nous oblige à maintenir une liste de notifications. Finalement, une partie de votre code devra parcourir toutes les notifications. Si nous implémentions votre collection de notifications sous forme de tableau, vous les itéreriez comme suit:

// Si un simple tableau est utilisé pour stocker les notifications pour (int i = 0; i <notificationList.length; i ++) Notification notification = notificationList [i]);

// Si ArrayList est Java est utilisé, alors nous itérerions // sur eux comme: pour (int i = 0; i <notificationList.size (); i ++) Notification notification = (Notification) notificationList.get (i);

Et s'il s'agissait d'une autre collection comme un ensemble, un arbre, etc., la façon d'itérer changerait légèrement. Maintenant, que se passe-t-il si nous construisons un itérateur qui fournit une manière générique d'itérer sur une collection indépendante de son type.

// Créer un itérateur Iterator iterator = notificationList.createIterator ();
 // Peu importe si list est Array ou ArrayList ou // rien d'autre. while (iterator.hasNext ()) { Notification de notification = iterator.next ()); }

Le modèle d'itérateur nous permet de faire exactement cela. Formellement, il est défini comme suit:**  
_Le modèle d'itérateur fournit un moyen d'accéder aux éléments d'un objet agrégé sans exposer sa représentation sous-jacente._**

**_Diagramme de classe:_**  
![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/iteratorpattern1.png)

Ici, nous avons une interface commune Aggregate pour le client car elle la dissocie de l'implémentation de votre collection d'objets. ConcreteAggregate implémente createIterator () qui renvoie l'itérateur pour sa collection. La responsabilité de chaque ConcreteAggregate est d'instancier un ConcreteIterator qui peut itérer sur sa collection d'objets. L'interface de l'itérateur fournit un ensemble de méthodes pour parcourir ou modifier la collection qui s'ajoute à next () / hasNext (), elle peut également fournir des fonctions de recherche, de suppression, etc.  
Comprenons cela à travers un exemple. Supposons que nous créons une barre de notification dans notre application qui affiche toutes les notifications contenues dans une collection de notifications. NotificationCollection fournit un itérateur pour itérer sur ses éléments sans exposer comment il a implémenté la collection (tableau dans ce cas) au client (NotificationBar).  

  

  

Le diagramme de classes serait:

![](https://media.geeksforgeeks.org/wp-content/uploads/20200214144148/NotificationIterator.png)

Vous trouverez ci-dessous l'implémentation Java de la même chose:

_filter_none_

_Éditer_

_play_arrow_

_luminosité_4_

`// A Java program to demonstrate implementation`

`// of iterator pattern with the example of`

`// notifications`

`// A simple Notification class`

`class` `Notification`

`{`

`// To store notification message`

`String notification;`

`public` `Notification(String notification)`

`{`

`this``.notification = notification;`

`}`

`public` `String getNotification()`

`{`

`return` `notification;`

`}`

`}`

`// Collection interface`

`interface` `Collection`

`{`

`public` `Iterator createIterator();`

`}`

`// Collection of notifications`

`class` `NotificationCollection` `implements` `Collection`

`{`

`static` `final` `int` `MAX_ITEMS =` `6``;`

`int` `numberOfItems =` `0``;`

`Notification[] notificationList;`

`public` `NotificationCollection()`

`{`

`notificationList =` `new` `Notification[MAX_ITEMS];`

`// Let us add some dummy notifications`

`addItem(``"Notification 1"``);`

`addItem(``"Notification 2"``);`

`addItem(``"Notification 3"``);`

`}`

`public` `void` `addItem(String str)`

`{`

`Notification notification =` `new` `Notification(str);`

`if` `(numberOfItems >= MAX_ITEMS)`

`System.err.println(``"Full"``);`

`else`

`{`

`notificationList[numberOfItems] = notification;`

`numberOfItems = numberOfItems +` `1``;`

`}`

`}`

`public` `Iterator createIterator()`

`{`

`return` `new` `NotificationIterator(notificationList);`

`}`

`}`

`// We could also use Java.Util.Iterator`

`interface` `Iterator`

`{`

`// indicates whether there are more elements to`

`// iterate over`

`boolean` `hasNext();`

`// returns the next element`

`Object next();`

`}`

`// Notification iterator`

`class` `NotificationIterator` `implements` `Iterator`

`{`

`Notification[] notificationList;`

`// maintains curr pos of iterator over the array`

`int` `pos =` `0``;`

`// Constructor takes the array of notifiactionList are`

`// going to iterate over.`

`public` `NotificationIterator (Notification[] notificationList)`

`{`

`this``.notificationList = notificationList;`

`}`

`public` `Object next()`

`{`

`// return next element in the array and increment pos`

`Notification notification = notificationList[pos];`

`pos +=` `1``;`

`return` `notification;`

`}`

`public` `boolean` `hasNext()`

`{`

`if` `(pos >= notificationList.length ||`

`notificationList[pos] ==` `null``)`

`return` `false``;`

`else`

`return` `true``;`

`}`

`}`

`// Contains collection of notifications as an object of`

`// NotificationCollection`

`class` `NotificationBar`

`{`

`NotificationCollection notifications;`

`public` `NotificationBar(NotificationCollection notifications)`

`{`

`this``.notifications = notifications;`

`}`

`public` `void` `printNotifications()`

`{`

`Iterator iterator = notifications.createIterator();`

`System.out.println(``"-------NOTIFICATION BAR------------"``);`

`while` `(iterator.hasNext())`

`{`

`Notification n = (Notification)iterator.next();`

`System.out.println(n.getNotification());`

`}`

`}`

`}`

`// Driver class`

`class` `Main`

`{`

`public` `static` `void` `main(String args[])`

`{`

`NotificationCollection nc =` `new` `NotificationCollection();`

`NotificationBar nb =` `new` `NotificationBar(nc);`

`nb.printNotifications();`

`}`

`}`

Production:

-------BARRE DE NOTIFICATION------------ Notification 1 Notification 2 Notification 3

Notez que si nous avions utilisé ArrayList au lieu de Array, il n'y aura pas de changement dans le code client (barre de notification) en raison du découplage réalisé par l'utilisation de l'interface de l'itérateur.

**Références:**  
[Modèles de conception Head First](http://www.amazon.com/Head-First-Design-Patterns/dp/0596007124)
