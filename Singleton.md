La méthode Factory est un [modèle de conception créative](https://www.geeksforgeeks.org/design-patterns-set-1-introduction/) , c'est-à-dire lié à la création d'objets. Dans le modèle Factory, nous créons un objet sans exposer la logique de création au client et le client utilise la même interface commune pour créer un nouveau type d'objet.  
L'idée est d'utiliser une fonction membre statique (méthode de fabrique statique) qui crée et retourne des instances, cachant les détails des modules de classe à l'utilisateur.

Un modèle d'usine est l'un des principes de conception de base pour créer un objet, permettant aux clients de créer des objets d'une bibliothèque (expliqué ci-dessous) d'une manière telle qu'il ne soit pas étroitement lié à la hiérarchie de classes de la bibliothèque.

_**Que veut dire quand on parle de bibliothèque et de clients?**_  
Une bibliothèque est quelque chose qui est fourni par un tiers qui expose certaines API publiques et les clients font des appels à ces API publiques pour accomplir sa tâche. Un exemple très simple peut être différents types de vues fournies par Android OS.

  

  

_**Pourquoi un modèle d'usine?**_  
Comprenons-le avec un exemple:

_filter_none_

_Éditer_

_play_arrow_

_luminosité_4_

`// A design without factory pattern`

`#include <iostream>`

`using` `namespace` `std;`

`// Library classes`

`class` `Vehicle {`

`public``:`

`virtual` `void` `printVehicle() = 0;`

`};`

`class` `TwoWheeler :` `public` `Vehicle {`

`public``:`

`void` `printVehicle() {`

`cout <<` `"I am two wheeler"` `<< endl;`

`}`

`};`

`class` `FourWheeler :` `public` `Vehicle {`

`public``:`

`void` `printVehicle() {`

`cout <<` `"I am four wheeler"` `<< endl;`

`}`

`};`

`// Client (or user) class`

`class` `Client {`

`public``:`

`Client(``int` `type) {`

`// Client explicitly creates classes according to type`

`if` `(type == 1)`

`pVehicle =` `new` `TwoWheeler();`

`else` `if` `(type == 2)`

`pVehicle =` `new` `FourWheeler();`

`else`

`pVehicle = NULL;`

`}`

`~Client() {`

`if` `(pVehicle)`

`{`

`delete``[] pVehicle;`

`pVehicle = NULL;`

`}`

`}`

`Vehicle* getVehicle() {`

`return` `pVehicle;`

`}`

`private``:`

`Vehicle *pVehicle;`

`};`

`// Driver program`

`int` `main() {`

`Client *pClient =` `new` `Client(1);`

`Vehicle * pVehicle = pClient->getVehicle();`

`pVehicle->printVehicle();`

`return` `0;`

`}`

Production:

Je suis deux roues

_**Quels sont les problèmes avec la conception ci-dessus?**_  
Comme vous devez l'avoir observé dans l'exemple ci-dessus, le client crée des objets de TwoWheeler ou FourWheeler en fonction d'une entrée lors de la construction de son objet.  
Dites, la bibliothèque présente une nouvelle classe ThreeWheeler pour incorporer également des véhicules à trois roues. Ce qui se passerait? Le client finira par enchaîner un nouveau else si dans l'échelle conditionnelle pour créer des objets de ThreeWheeler. Ce qui à son tour nécessitera que le client soit recompilé. Ainsi, chaque fois qu'une nouvelle modification est apportée du côté de la bibliothèque, le client devra apporter des modifications correspondantes à sa fin et recompiler le code. Semble mauvais? C'est une très mauvaise pratique du design.

**Comment éviter le problème?**  
La réponse est, créez une méthode statique (ou d'usine). Voyons ci-dessous le code.

_filter_none_

_Éditer_

_play_arrow_

_luminosité_4_

`// C++ program to demonstrate factory method design pattern`

`#include <iostream>`

`using` `namespace` `std;`

`enum` `VehicleType {`

`VT_TwoWheeler, VT_ThreeWheeler, VT_FourWheeler`

`};`

`// Library classes`

`class` `Vehicle {`

`public``:`

`virtual` `void` `printVehicle() = 0;`

`static` `Vehicle* Create(VehicleType type);`

`};`

`class` `TwoWheeler :` `public` `Vehicle {`

`public``:`

`void` `printVehicle() {`

`cout <<` `"I am two wheeler"` `<< endl;`

`}`

`};`

`class` `ThreeWheeler :` `public` `Vehicle {`

`public``:`

`void` `printVehicle() {`

`cout <<` `"I am three wheeler"` `<< endl;`

`}`

`};`

`class` `FourWheeler :` `public` `Vehicle {`

`public``:`

`void` `printVehicle() {`

`cout <<` `"I am four wheeler"` `<< endl;`

`}`

`};`

`// Factory method to create objects of different types.`

`// Change is required only in this function to create a new object type`

`Vehicle* Vehicle::Create(VehicleType type) {`

`if` `(type == VT_TwoWheeler)`

`return` `new` `TwoWheeler();`

`else` `if` `(type == VT_ThreeWheeler)`

`return` `new` `ThreeWheeler();`

`else` `if` `(type == VT_FourWheeler)`

`return` `new` `FourWheeler();`

`else` `return` `NULL;`

`}`

`// Client class`

`class` `Client {`

`public``:`

`// Client doesn't explicitly create objects`

`// but passes type to factory method "Create()"`

`Client()`

`{`

`VehicleType type = VT_ThreeWheeler;`

`pVehicle = Vehicle::Create(type);`

`}`

`~Client() {`

`if` `(pVehicle) {`

`delete``[] pVehicle;`

`pVehicle = NULL;`

`}`

`}`

`Vehicle* getVehicle() {`

`return` `pVehicle;`

`}`

`private``:`

`Vehicle *pVehicle;`

`};`

`// Driver program`

`int` `main() {`

`Client *pClient =` `new` `Client();`

`Vehicle * pVehicle = pClient->getVehicle();`

`pVehicle->printVehicle();`

`return` `0;`

`}`

Production:

Je suis à trois roues

Dans l'exemple ci-dessus, nous avons totalement découplé la sélection du type pour la création d'objet depuis Client. La bibliothèque est désormais responsable du choix du type d'objet à créer en fonction d'une entrée. Le client a juste besoin d'appeler la méthode Create Factory de la bibliothèque et de transmettre le type qu'il veut sans se soucier de l'implémentation réelle de la création d'objets.
