Comme [les](https://www.geeksforgeeks.org/category/design/) articles [précédents](https://www.geeksforgeeks.org/category/design/) , abordons un problème de conception pour comprendre le modèle de commande. Supposons que vous construisez un système domotique. Il y a une télécommande programmable qui peut être utilisée pour allumer et éteindre divers éléments de votre maison comme les lumières, la chaîne stéréo, le courant alternatif, etc. Cela ressemble à quelque chose comme ça.

Vous pouvez le faire avec de simples instructions if-else comme

if (buttonPressed == button1) lumières allumées()

Mais nous devons garder à l'esprit que la mise sous tension de certains appareils comme la stéréo comprend de nombreuses étapes comme le réglage du cd, du volume, etc. Nous pouvons également réaffecter un bouton pour faire autre chose. En utilisant un simple if-else, nous codons sur l'implémentation plutôt que sur l'interface. Il existe également un couplage serré.

Donc, ce que nous voulons obtenir, c'est une conception qui fournit un couplage lâche et la télécommande ne devrait pas avoir beaucoup d'informations sur un appareil particulier. Le modèle de commande nous aide à le faire.

  

  

**Définition:** Le **modèle de commande** encapsule une demande en tant qu'objet, ce qui nous permet de paramétrer d'autres objets avec différentes demandes, demandes de file d'attente ou de journal, et prend en charge les opérations annulables.

La définition est un peu déroutante au début, mais passons en revue. Par analogie avec notre problème ci-dessus, la télécommande est le client et la stéréo, les lumières, etc. sont les récepteurs. Dans le modèle de commande, il existe un objet Command qui _encapsule une demande_ en liant ensemble un ensemble d'actions sur un récepteur spécifique. Il le fait en exposant une seule méthode execute () qui provoque l'appel de certaines actions sur le récepteur.

_Paramétrer d'autres objets avec des demandes différentes_ dans notre analogie signifie que le bouton utilisé pour allumer les lumières peut plus tard être utilisé pour allumer la stéréo ou peut-être ouvrir la porte du garage.

_les demandes de file d'attente ou de journalisation et la prise en charge des opérations annulables_ signifie que l'opération d'exécution de la commande peut stocker l'état pour inverser ses effets dans la commande elle-même. La commande peut avoir une opération unExecute ajoutée qui annule les effets d'un appel précédent à exécuter. Elle peut également prendre en charge les modifications de journalisation afin qu'elles puissent être réappliquées en cas de panne du système.

Vous trouverez ci-dessous l'implémentation Java de l'exemple de contrôle à distance mentionné ci-dessus:

_filter_none_

_Éditer_

_play_arrow_

_luminosité_4_

`// A simple Java program to demonstrate`

`// implementation of Command Pattern using`

`// a remote control example.`

`// An interface for command`

`interface` `Command`

`{`

`public` `void` `execute();`

`}`

`// Light class and its corresponding command`

`// classes`

`class` `Light`

`{`

`public` `void` `on()`

`{`

`System.out.println(``"Light is on"``);`

`}`

`public` `void` `off()`

`{`

`System.out.println(``"Light is off"``);`

`}`

`}`

`class` `LightOnCommand` `implements` `Command`

`{`

`Light light;`

`// The constructor is passed the light it`

`// is going to control.`

`public` `LightOnCommand(Light light)`

`{`

`this``.light = light;`

`}`

`public` `void` `execute()`

`{`

`light.on();`

`}`

`}`

`class` `LightOffCommand` `implements` `Command`

`{`

`Light light;`

`public` `LightOffCommand(Light light)`

`{`

`this``.light = light;`

`}`

`public` `void` `execute()`

`{`

`light.off();`

`}`

`}`

`// Stereo and its command classes`

`class` `Stereo`

`{`

`public` `void` `on()`

`{`

`System.out.println(``"Stereo is on"``);`

`}`

`public` `void` `off()`

`{`

`System.out.println(``"Stereo is off"``);`

`}`

`public` `void` `setCD()`

`{`

`System.out.println(``"Stereo is set "` `+`

`"for CD input"``);`

`}`

`public` `void` `setDVD()`

`{`

`System.out.println(``"Stereo is set"``+`

`" for DVD input"``);`

`}`

`public` `void` `setRadio()`

`{`

`System.out.println(``"Stereo is set"` `+`

`" for Radio"``);`

`}`

`public` `void` `setVolume(``int` `volume)`

`{`

`// code to set the volume`

`System.out.println(``"Stereo volume set"`

`+` `" to "` `+ volume);`

`}`

`}`

`class` `StereoOffCommand` `implements` `Command`

`{`

`Stereo stereo;`

`public` `StereoOffCommand(Stereo stereo)`

`{`

`this``.stereo = stereo;`

`}`

`public` `void` `execute()`

`{`

`stereo.off();`

`}`

`}`

`class` `StereoOnWithCDCommand` `implements` `Command`

`{`

`Stereo stereo;`

`public` `StereoOnWithCDCommand(Stereo stereo)`

`{`

`this``.stereo = stereo;`

`}`

`public` `void` `execute()`

`{`

`stereo.on();`

`stereo.setCD();`

`stereo.setVolume(``11``);`

`}`

`}`

`// A Simple remote control with one button`

`class` `SimpleRemoteControl`

`{`

`Command slot;` `// only one button`

`public` `SimpleRemoteControl()`

`{`

`}`

`public` `void` `setCommand(Command command)`

`{`

`// set the command the remote will`

`// execute`

`slot = command;`

`}`

`public` `void` `buttonWasPressed()`

`{`

`slot.execute();`

`}`

`}`

`// Driver class`

`class` `RemoteControlTest`

`{`

`public` `static` `void` `main(String[] args)`

`{`

`SimpleRemoteControl remote =`

`new` `SimpleRemoteControl();`

`Light light =` `new` `Light();`

`Stereo stereo =` `new` `Stereo();`

`// we can change command dynamically`

`remote.setCommand(``new`

`LightOnCommand(light));`

`remote.buttonWasPressed();`

`remote.setCommand(``new`

`StereoOnWithCDCommand(stereo));`

`remote.buttonWasPressed();`

`remote.setCommand(``new`

`StereoOffCommand(stereo));`

`remote.buttonWasPressed();`

`}`

`}`

**Production:**

La lumière est allumée La stéréo est activée La stéréo est réglée pour l'entrée CD Volume stéréo réglé sur 11 La stéréo est désactivée

Notez que la télécommande ne sait rien de l'activation de la chaîne stéréo. Ces informations sont contenues dans un objet de commande distinct. Cela réduit le couplage entre eux.

**Avantages:**

-   Rend notre code extensible car nous pouvons ajouter de nouvelles commandes sans changer le code existant.
-   Réduit le couplage de l'invocateur et du récepteur d'une commande.

**Désavantages:**

-   Augmentation du nombre de classes pour chaque commande individuelle

**_Références:_**

-   Head First Design Patterns (livre)
-   [https://github.com/bethrobson/Head-First-Design-Patterns/tree/master/src/headfirst/designpatterns/command](https://github.com/bethrobson/Head-First-Design-Patterns/tree/master/src/headfirst/designpatterns/command)
