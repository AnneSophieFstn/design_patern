Le modèle composite est un modèle de conception de partitionnement et décrit un groupe d'objets qui est traité de la même manière qu'une seule instance du même type d'objet. L'intention d'un composite est de «composer» des objets dans des structures arborescentes pour représenter des hiérarchies partie-tout. Il vous permet d'avoir une structure arborescente et de demander à chaque nœud de l'arborescence d'effectuer une tâche.

-   Comme décrit par Gof, «Composez des objets dans une structure arborescente pour représenter **des hiérarchies partie-tout** . Composite permet au client de traiter des objets individuels et des compositions d'objets de manière uniforme ».
-   Lorsqu'ils traitent des données structurées en arborescence, les programmeurs doivent souvent faire la distinction entre un nœud feuille et une branche. Cela rend le code plus complexe et donc sujet aux erreurs. La solution est une **interface** qui permet de traiter les objets complexes et primitifs de manière uniforme.
-   Dans la programmation orientée objet, un composite est un objet conçu comme une composition d'un ou plusieurs objets similaires, tous présentant des fonctionnalités similaires. C'est ce qu'on appelle **une** relation **«has-a»** entre les objets.

Le concept clé est que vous pouvez manipuler une seule instance de l'objet comme vous le feriez pour un groupe d'entre eux. Les opérations que vous pouvez effectuer sur tous les objets composites ont souvent une relation de moindre dénominateur commun.  
**Le modèle composite compte quatre participants:**

1.  **Composant - Le** composant déclare l'interface pour les objets de la composition et pour accéder et gérer ses composants enfants. Il implémente également le comportement par défaut de l'interface commune à toutes les classes, le cas échéant.
2.  **Feuille - La** feuille définit le comportement des objets primitifs dans la composition. Il représente des objets feuilles dans la composition.
3.  **Composite -** Composite stocke les composants enfants et implémente les opérations liées aux enfants dans l'interface du composant.
4.  **Client - Le** client manipule les objets de la composition via l'interface du composant.

Le client utilise l'interface de classe de composant pour interagir avec les objets dans la structure de composition. Si le destinataire est une feuille, la demande est traitée directement. Si le destinataire est un composite, il transmet généralement la demande à ses composants enfants, réalisant éventuellement des opérations supplémentaires avant et après le transfert.

**Exemple de la vraie vie**

Dans une organisation, il y a des directeurs généraux et sous des directeurs généraux, il peut y avoir des directeurs et sous des directeurs il peut y avoir des développeurs. Vous pouvez maintenant définir une structure arborescente et demander à chaque nœud d'effectuer une opération courante comme getSalary ().  
Le modèle de conception composite traite chaque nœud de deux manières:  
1) **Composite** - Composite signifie qu'il peut avoir d'autres objets en dessous.  
2) **feuille** - feuille signifie qu'il n'y a aucun objet en dessous.

  

  

**Structure arborescente:**

![Arbre](https://media.geeksforgeeks.org/wp-content/uploads/Composite-Design-Pattern-Diagram.png)  
La figure ci-dessus montre une structure d'objet composite typique. Comme vous pouvez le voir, il peut y avoir beaucoup d'enfants pour un seul parent, c'est-à-dire composite, mais un seul parent par enfant.

**Interface Component.java**

_filter_none_

_luminosité_4_

`public` `interface` `Employee`

`{`

`public` `void` `showEmployeeDetails();`

`}`

**Leaf.java**

_filter_none_

_luminosité_4_

`public` `class` `Developer` `implements` `Employee`

`{`

`private` `String name;`

`private` `long` `empId;`

`private` `String position;`

`public` `Developer(``long` `empId, String name, String position)`

`{`

`this``.empId = empId;`

`this``.name = name;`

`this``.position = position;`

`}`

`@Override`

`public` `void` `showEmployeeDetails()`

`{`

`System.out.println(empId+``" "` `+name+);`

`}`

`}`

**Leaf.java**

_filter_none_

_luminosité_4_

`public` `class` `Manager` `implements` `Employee`

`{`

`private` `String name;`

`private` `long` `empId;`

`private` `String position;`

`public` `Manager(``long` `empId, String name, String position)`

`{`

`this``.empId = empId;`

`this``.name = name;`

`this``.position = position;`

`}`

`@Override`

`public` `void` `showEmployeeDetails()`

`{`

`System.out.println(empId+``" "` `+name);`

`}`

`}`

**Composite.java**

_filter_none_

_luminosité_4_

`import` `java.util.ArrayList;`

`import` `java.util.List;`

`public` `class` `CompanyDirectory` `implements` `Employee`

`{`

`private` `List<Employee> employeeList =` `new` `ArrayList<Employee>();`

`@Override`

`public` `void` `showEmployeeDetails()`

`{`

`for``(Employee emp:employeeList)`

`{`

`emp.showEmployeeDetails();`

`}`

`}`

`public` `void` `addEmployee(Employee emp)`

`{`

`employeeList.add(emp);`

`}`

`public` `void` `removeEmployee(Employee emp)`

`{`

`employeeList.remove(emp);`

`}`

`}`

**Client.java**

_filter_none_

_luminosité_4_

`public` `class` `Company`

`{`

`public` `static` `void` `main (String[] args)`

`{`

`Developer dev1 =` `new` `Developer(``100``,` `"Lokesh Sharma"``,` `"Pro Developer"``);`

`Developer dev2 =` `new` `Developer(``101``,` `"Vinay Sharma"``,` `"Developer"``);`

`CompanyDirectory engDirectory =` `new` `CompanyDirectory();`

`engDirectory.addEmployee(dev1);`

`engDirectory.addEmployee(dev2);`

`Manager man1 =` `new` `Manager(``200``,` `"Kushagra Garg"``,` `"SEO Manager"``);`

`Manager man2 =` `new` `Manager(``201``,` `"Vikram Sharma "``,` `"Kushagra's Manager"``);`

`CompanyDirectory accDirectory =` `new` `CompanyDirectory();`

`accDirectory.addEmployee(man1);`

`accDirectory.addEmployee(man2);`

`CompanyDirectory directory =` `new` `CompanyDirectory();`

`directory.addEmployee(engDirectory);`

`directory.addEmployee(accDirectory);`

`directory.showEmployeeDetails();`

`}`

`}`

**Diagramme UML pour le modèle de conception composite:**

  

  

![Conception composite-UML](https://media.geeksforgeeks.org/wp-content/uploads/Composite-Design-Pattern-Diagram-1.png)

**Code de fonctionnement complet pour l'exemple ci-dessus:**

_filter_none_

_Éditer_

_play_arrow_

_luminosité_4_

`// A Java program to demonstrate working of`

`// Composite Design Pattern with example`

`// of a company with different`

`// employee details`

`import` `java.util.ArrayList;`

`import` `java.util.List;`

`// A common interface for all employee`

`interface` `Employee`

`{`

`public` `void` `showEmployeeDetails();`

`}`

`class` `Developer` `implements` `Employee`

`{`

`private` `String name;`

`private` `long` `empId;`

`private` `String position;`

`public` `Developer(``long` `empId, String name, String position)`

`{`

`// Assign the Employee id,`

`// name and the position`

`this``.empId = empId;`

`this``.name = name;`

`this``.position = position;`

`}`

`@Override`

`public` `void` `showEmployeeDetails()`

`{`

`System.out.println(empId+``" "` `+name+` `" "` `+ position );`

`}`

`}`

`class` `Manager` `implements` `Employee`

`{`

`private` `String name;`

`private` `long` `empId;`

`private` `String position;`

`public` `Manager(``long` `empId, String name, String position)`

`{`

`this``.empId = empId;`

`this``.name = name;`

`this``.position = position;`

`}`

`@Override`

`public` `void` `showEmployeeDetails()`

`{`

`System.out.println(empId+``" "` `+name+` `" "` `+ position );`

`}`

`}`

`// Class used to get Employee List`

`// and do the opertions like`

`// add or remove Employee`

`class` `CompanyDirectory` `implements` `Employee`

`{`

`private` `List<Employee> employeeList =` `new` `ArrayList<Employee>();`

`@Override`

`public` `void` `showEmployeeDetails()`

`{`

`for``(Employee emp:employeeList)`

`{`

`emp.showEmployeeDetails();`

`}`

`}`

`public` `void` `addEmployee(Employee emp)`

`{`

`employeeList.add(emp);`

`}`

`public` `void` `removeEmployee(Employee emp)`

`{`

`employeeList.remove(emp);`

`}`

`}`

`// Driver class`

`public` `class` `Company`

`{`

`public` `static` `void` `main (String[] args)`

`{`

`Developer dev1 =` `new` `Developer(``100``,` `"Lokesh Sharma"``,` `"Pro Developer"``);`

`Developer dev2 =` `new` `Developer(``101``,` `"Vinay Sharma"``,` `"Developer"``);`

`CompanyDirectory engDirectory =` `new` `CompanyDirectory();`

`engDirectory.addEmployee(dev1);`

`engDirectory.addEmployee(dev2);`

`Manager man1 =` `new` `Manager(``200``,` `"Kushagra Garg"``,` `"SEO Manager"``);`

`Manager man2 =` `new` `Manager(``201``,` `"Vikram Sharma "``,` `"Kushagra's Manager"``);`

`CompanyDirectory accDirectory =` `new` `CompanyDirectory();`

`accDirectory.addEmployee(man1);`

`accDirectory.addEmployee(man2);`

`CompanyDirectory directory =` `new` `CompanyDirectory();`

`directory.addEmployee(engDirectory);`

`directory.addEmployee(accDirectory);`

`directory.showEmployeeDetails();`

`}`

`}`

Production :

100 Développeur Lokesh Sharma Pro 101 Développeur Vinay Sharma 200 Gestionnaire de référencement Kushagra Garg 201 Le manager de Vikram Sharma Kushagra

**Quand utiliser Composite Design Pattern?**

Le modèle composite doit être utilisé lorsque les clients doivent ignorer la différence entre les compositions d'objets et d'objets individuels. Si les programmeurs constatent qu'ils utilisent plusieurs objets de la même manière, et ont souvent un code presque identique pour gérer chacun d'eux, alors le composite est un bon choix, il est moins complexe dans cette situation de traiter les primitifs et les composites comme homogènes.

1.  Moins de nombre d'objets réduit l'utilisation de la mémoire et parvient à nous éloigner des erreurs liées à la mémoire comme [java.lang.OutOfMemoryError](https://www.geeksforgeeks.org/understanding-outofmemoryerror-exception-java/) .
2.  Bien que la création d'un objet en Java soit très rapide, nous pouvons toujours réduire le temps d'exécution de notre programme en partageant des objets.

**Quand ne pas utiliser Composite Design Pattern?**

1.  Le modèle de conception composite rend plus difficile la restriction du type de composants d'un composite. Il ne doit donc pas être utilisé lorsque vous ne souhaitez pas représenter une hiérarchie d'objets complète ou partielle.
2.  Le modèle de conception composite peut rendre la conception trop générale. Il est plus difficile de restreindre les composants d'un composite. Parfois, vous voulez qu'un composite n'ait que certains composants. Avec Composite, vous ne pouvez pas compter sur le système de types pour appliquer ces contraintes à votre place. Au lieu de cela, vous devrez utiliser des contrôles d'exécution.
