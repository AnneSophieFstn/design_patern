Le modèle de poids mouche est l'un des [modèles de conception structurelle](https://www.geeksforgeeks.org/design-patterns-set-1-introduction/) car ce modèle fournit des moyens de réduire le nombre d'objets, améliorant ainsi la structure des objets requis par l'application. Le modèle de poids mouche est utilisé lorsque nous devons créer un grand nombre d'objets similaires (disons 10 5 ). Une caractéristique importante des objets poids mouche est qu'ils sont **immuables** . Cela signifie qu'ils ne peuvent pas être modifiés une fois qu'ils ont été construits.

**Pourquoi prenons-nous soin du nombre d'objets dans notre programme?**

-   Moins de nombre d'objets réduit l'utilisation de la mémoire et parvient à nous éloigner des erreurs liées à la mémoire comme [java.lang.OutOfMemoryError.](https://docs.oracle.com/javase/7/docs/api/java/lang/OutOfMemoryError.html)
-   Bien que la création d'un objet en Java soit très rapide, nous pouvons toujours réduire le temps d'exécution de notre programme en partageant des objets.
    

Dans le modèle Flyweight, nous utilisons un [HashMap](https://www.geeksforgeeks.org/hashmap-treemap-java/) qui stocke la référence à l'objet qui a déjà été créé, chaque objet est associé à une clé. Désormais, lorsqu'un client veut créer un objet, il lui suffit de passer une clé qui lui est associée et si l'objet a déjà été créé, nous obtenons simplement la référence à cet objet, sinon il crée un nouvel objet et le renvoie ensuite au client .

**États intrinsèques et extrinsèques**

  

  

Pour comprendre l'état intrinsèque et extrinsèque, considérons un exemple.

Supposons que dans un éditeur de texte, lorsque nous saisissons un caractère, un objet de la classe Character est créé, les attributs de la classe Character sont {name, font, size}. Nous n'avons pas besoin de créer un objet chaque fois que le client entre un caractère car la lettre «B» n'est pas différente d'un autre «B». Si le client tape à nouveau un 'B', nous renvoyons simplement l'objet que nous avons déjà créé auparavant. Maintenant, tous ces états sont intrinsèques (nom, police, taille), car ils peuvent être partagés entre les différents objets car ils sont similaires les uns aux autres.

Maintenant, nous ajoutons plus d'attributs à la classe Character, ils sont ligne et colonne. Ils spécifient la position d'un caractère dans le document. Désormais, ces attributs ne seront pas similaires même pour les mêmes caractères, car deux caractères n'auront pas la même position dans un document, ces états sont appelés états extrinsèques et ne peuvent pas être partagés entre les objets.

**Mise en œuvre:** Nous mettons en œuvre la création de terroristes et de contre-terroristes dans le jeu de [Counter Strike](https://en.wikipedia.org/wiki/Counter-Strike) . Nous avons donc 2 classes une pour **T** errorist ( **T** ) et l'autre pour **C** ounter **T** errorist ( **CT** ). Chaque fois qu'un joueur demande une arme, nous lui attribuons l'arme demandée. Dans la mission, la tâche du terroriste est de poser une bombe tandis que les contre-terroristes doivent diffuser la bombe.

**Pourquoi utiliser Flyweight Design Pattern dans cet exemple?** Ici, nous utilisons le modèle de conception Fly Weight, car ici nous devons réduire le nombre d'objets pour les joueurs. Maintenant, nous avons n nombre de joueurs jouant CS 1.6, si nous ne suivons pas le modèle de conception de poids de mouche, nous devrons créer n nombre d'objets, un pour chaque joueur. Mais maintenant, nous n'aurons plus qu'à créer 2 objets, l'un pour les terroristes et l'autre pour les contre-terroristes, nous les réutiliserons encore et encore chaque fois que nécessaire.

**État intrinsèque:** Ici, «tâche» est un état intrinsèque pour les deux types de joueurs, car c'est toujours le même pour les T / CT. Nous pouvons avoir d'autres États comme leur couleur ou toute autre propriété qui est similaire pour tous les terroristes / contre-terroristes dans leur classe respective de terroristes / contre-terroristes.

**État extrinsèque: L'** arme est un état extrinsèque puisque chaque joueur peut porter n'importe quelle arme de son choix. L'arme doit être passée en paramètre par le client lui-même.

Diagramme de classe:[![FwCd](https://media.geeksforgeeks.org/wp-content/uploads/flyweight.jpg)](https://media.geeksforgeeks.org/wp-content/uploads/flyweight.jpg)

_filter_none_

_Éditer_

_play_arrow_

_luminosité_4_

`// A Java program to demonstrate working of`

`// FlyWeight Pattern with example of Counter`

`// Strike Game`

`import` `java.util.Random;`

`import` `java.util.HashMap;`

`// A common interface for all players`

`interface` `Player`

`{`

`public` `void` `assignWeapon(String weapon);`

`public` `void` `mission();`

`}`

`// Terrorist must have weapon and mission`

`class` `Terrorist` `implements` `Player`

`{`

`// Intrinsic Attribute`

`private` `final` `String TASK;`

`// Extrinsic Attribute`

`private` `String weapon;`

`public` `Terrorist()`

`{`

`TASK =` `"PLANT A BOMB"``;`

`}`

`public` `void` `assignWeapon(String weapon)`

`{`

`// Assign a weapon`

`this``.weapon = weapon;`

`}`

`public` `void` `mission()`

`{`

`//Work on the Mission`

`System.out.println(``"Terrorist with weapon "`

`+ weapon +` `"|"` `+` `" Task is "` `+ TASK);`

`}`

`}`

`// CounterTerrorist must have weapon and mission`

`class` `CounterTerrorist` `implements` `Player`

`{`

`// Intrinsic Attribute`

`private` `final` `String TASK;`

`// Extrinsic Attribute`

`private` `String weapon;`

`public` `CounterTerrorist()`

`{`

`TASK =` `"DIFFUSE BOMB"``;`

`}`

`public` `void` `assignWeapon(String weapon)`

`{`

`this``.weapon = weapon;`

`}`

`public` `void` `mission()`

`{`

`System.out.println(``"Counter Terrorist with weapon "`

`+ weapon +` `"|"` `+` `" Task is "` `+ TASK);`

`}`

`}`

`// Class used to get a player using HashMap (Returns`

`// an existing player if a player of given type exists.`

`// Else creates a new player and returns it.`

`class` `PlayerFactory`

`{`

`/* HashMap stores the reference to the object`

`of Terrorist(TS) or CounterTerrorist(CT). */`

`private` `static` `HashMap <String, Player> hm =`

`new` `HashMap<String, Player>();`

`// Method to get a player`

`public` `static` `Player getPlayer(String type)`

`{`

`Player p =` `null``;`

`/* If an object for TS or CT has already been`

`created simply return its reference */`

`if` `(hm.containsKey(type))`

`p = hm.get(type);`

`else`

`{`

`/* create an object of TS/CT */`

`switch``(type)`

`{`

`case` `"Terrorist"``:`

`System.out.println(``"Terrorist Created"``);`

`p =` `new` `Terrorist();`

`break``;`

`case` `"CounterTerrorist"``:`

`System.out.println(``"Counter Terrorist Created"``);`

`p =` `new` `CounterTerrorist();`

`break``;`

`default` `:`

`System.out.println(``"Unreachable code!"``);`

`}`

`// Once created insert it into the HashMap`

`hm.put(type, p);`

`}`

`return` `p;`

`}`

`}`

`// Driver class`

`public` `class` `CounterStrike`

`{`

`// All player types and weapon (used by getRandPlayerType()`

`// and getRandWeapon()`

`private` `static` `String[] playerType =`

`{``"Terrorist"``,` `"CounterTerrorist"``};`

`private` `static` `String[] weapons =`

`{``"AK-47"``,` `"Maverick"``,` `"Gut Knife"``,` `"Desert Eagle"``};`

`// Driver code`

`public` `static` `void` `main(String args[])`

`{`

`/* Assume that we have a total of 10 players`

`in the game. */`

`for` `(``int` `i =` `0``; i <` `10``; i++)`

`{`

`/* getPlayer() is called simply using the class`

`name since the method is a static one */`

`Player p = PlayerFactory.getPlayer(getRandPlayerType());`

`/* Assign a weapon chosen randomly uniformly`

`from the weapon array */`

`p.assignWeapon(getRandWeapon());`

`// Send this player on a mission`

`p.mission();`

`}`

`}`

`// Utility methods to get a random player type and`

`// weapon`

`public` `static` `String getRandPlayerType()`

`{`

`Random r =` `new` `Random();`

`// Will return an integer between [0,2)`

`int` `randInt = r.nextInt(playerType.length);`

`// return the player stored at index 'randInt'`

`return` `playerType[randInt];`

`}`

`public` `static` `String getRandWeapon()`

`{`

`Random r =` `new` `Random();`

`// Will return an integer between [0,5)`

`int` `randInt = r.nextInt(weapons.length);`

`// Return the weapon stored at index 'randInt'`

`return` `weapons[randInt];`

`}`

`}`

**Production:**

Contre-terrorisme créé Contre le terrorisme avec arme Gut Knife | La tâche est DIFFUSE BOMB Contre le terrorisme avec arme Desert Eagle | La tâche est DIFFUSE BOMB Terroriste créé Terroriste avec arme AK-47 | La tâche est PLANTER UNE BOMBE Terroriste avec arme Gut Knife | La tâche est PLANTER UNE BOMBE Terroriste avec arme Gut Knife | La tâche est PLANTER UNE BOMBE Terroriste avec arme Desert Eagle | La tâche est PLANTER UNE BOMBE Terroriste avec arme AK-47 | La tâche est PLANTER UNE BOMBE Contre le terrorisme avec arme Desert Eagle | La tâche est DIFFUSE BOMB Contre le terrorisme avec arme Gut Knife | La tâche est DIFFUSE BOMB Contre le terrorisme avec arme Desert Eagle | La tâche est DIFFUSE BOMB

**Références:**

-   Éléments d'un logiciel orienté objet réutilisable (par groupe de quatre)
-   [https://en.wikipedia.org/wiki/Flyweight_pattern](https://en.wikipedia.org/wiki/Flyweight_pattern)
