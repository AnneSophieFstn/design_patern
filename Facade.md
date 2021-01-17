La façade fait partie du modèle de conception Gang of Four et est classée sous Modèles de conception structurelle. Avant de creuser dans les détails, discutons de quelques exemples qui seront résolus par ce Pattern particulier.

Donc, comme son nom l'indique, cela signifie la face du bâtiment. Les passants ne peuvent voir que cette face vitrée du bâtiment. Ils n'en savent rien, le câblage, les tuyaux et autres complexités. Il cache toutes les complexités du bâtiment et affiche un visage amical.

**Plus d'exemples**

En Java, l'interface JDBC peut être qualifiée de façade car, en tant qu'utilisateurs ou clients, nous créons une connexion à l'aide de l'interface «java.sql.Connection», dont l'implémentation ne nous préoccupe pas. La mise en œuvre est laissée au vendeur du pilote.

Un autre bon exemple peut être le démarrage d'un ordinateur. Lorsqu'un ordinateur démarre, cela implique le travail du processeur, de la mémoire, du disque dur, etc. Pour le rendre facile à utiliser pour les utilisateurs, nous pouvons ajouter une façade qui enveloppe la complexité de la tâche, et fournir une interface simple à la place.  
Il en va de même pour le **modèle de conception de façade** . Il masque les complexités du système et fournit une interface au client à partir de laquelle le client peut accéder au système.

  

  

[![](https://media.geeksforgeeks.org/wp-content/uploads/facadeA.png)](https://media.geeksforgeeks.org/wp-content/uploads/facadeA.png)

**Diagramme de modèle de conception de façade**

Essayons maintenant de mieux comprendre le modèle de façade en utilisant un exemple simple. Prenons un hôtel. Cet hôtel a un hôtelier. Il y a beaucoup de restaurants à l'intérieur de l'hôtel, par exemple les restaurants Veg, les restaurants non-Veg et les restaurants Veg / Non Both.  
Vous, en tant que client, souhaitez accéder à différents menus de différents restaurants. Vous ne savez pas quels sont les différents menus dont ils disposent. Vous avez juste accès à un hôtelier qui connaît bien son hôtel. Quel que soit le menu que vous voulez, vous le dites à l'hôtelier et il le sort des restaurants respectifs et vous le remet. Ici, l'hôtelier fait office de **façade** , car il cache les complexités du système hôtelier.  
Voyons voir comment ça fonctionne :

**Interface de l'hôtel**

_filter_none_

_luminosité_4_

`package` `structural.facade;`

`public` `interface` `Hotel`

`{`

`public` `Menus getMenus();`

`}`

L'interface de l'hôtel ne renvoie que les menus.  
De même, le Restaurant est de trois types et peut implémenter l'interface hôtelière. Jetons un coup d'œil au code de l'un des restaurants.

**NonVegRestaurant.java**

_filter_none_

_luminosité_4_

`package` `structural.facade;`

`public` `class` `NonVegRestaurant` `implements` `Hotel`

`{`

`public` `Menus getMenus()`

`{`

`NonVegMenu nv =` `new` `NonVegMenu();`

`return` `nv;`

`}`

`}`

**VegRestaurant.java**

_filter_none_

_luminosité_4_

`package` `structural.facade;`

`public` `class` `VegRestaurant` `implements` `Hotel`

`{`

`public` `Menus getMenus()`

`{`

`VegMenu v =` `new` `VegMenu();`

`return` `v;`

`}`

`}`

**VegNonBothRestaurant.java**

  

  

_filter_none_

_luminosité_4_

`package` `structural.facade;`

`public` `class` `VegNonBothRestaurant` `implements` `Hotel`

`{`

`public` `Menus getMenus()`

`{`

`Both b =` `new` `Both();`

`return` `b;`

`}`

`}`

Considérons maintenant la façade,

**HotelKeeper.java**

_filter_none_

_luminosité_4_

`package` `structural.facade;`

`public` `class` `HotelKeeper`

`{`

`public` `VegMenu getVegMenu()`

`{`

`VegRestaurant v =` `new` `VegRestaurant();`

`VegMenu vegMenu = (VegMenu)v.getMenus();`

`return` `vegMenu;`

`}`

`public` `NonVegMenu getNonVegMenu()`

`{`

`NonVegRestaurant v =` `new` `NonVegRestaurant();`

`NonVegMenu NonvegMenu = (NonVegMenu)v.getMenus();`

`return` `NonvegMenu;`

`}`

`public` `Both getVegNonMenu()`

`{`

`VegNonBothRestaurant v =` `new` `VegNonBothRestaurant();`

`Both bothMenu = (Both)v.getMenus();`

`return` `bothMenu;`

`}`

`}`

De là, il est clair que la mise en œuvre complexe sera effectuée par HotelKeeper lui-même. Le client accédera simplement à l'HotelKeeper et demandera le menu du restaurant Veg, NonVeg ou VegNon Both.

**Comment le programme client accédera-t-il à cette façade?**

_filter_none_

_luminosité_4_

`package` `structural.facade;`

`public` `class` `Client`

`{`

`public` `static` `void` `main (String[] args)`

`{`

`HotelKeeper keeper =` `new` `HotelKeeper();`

`VegMenu v = keeper.getVegMenu();`

`NonVegMenu nv = keeper.getNonVegMenu();`

`Both = keeper.getVegNonMenu();`

`}`

`}`

De cette manière, la mise en œuvre est envoyée à la façade. Le client n'a qu'une seule interface et ne peut accéder qu'à cela. Cela cache toutes les complexités.

**Quand ce modèle doit-il être utilisé?**

Le modèle de façade convient lorsque vous avez un **système complexe** que vous souhaitez exposer aux clients de manière simplifiée ou que vous souhaitez créer une couche de communication externe sur un système existant incompatible avec le système. La façade traite des interfaces, pas de la mise en œuvre. Son but est de cacher la complexité interne derrière une interface unique qui paraît simple à l'extérieur.
