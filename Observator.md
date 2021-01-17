Considérons d'abord le scénario suivant pour comprendre le modèle d'observateur.

**Scénario** :

Supposons que nous construisions une application de cricket qui notifie aux téléspectateurs des informations telles que le score actuel, le taux d'exécution, etc. Supposons que nous ayons créé deux éléments d'affichage CurrentScoreDisplay et AverageScoreDisplay. CricketData a toutes les données (courses, bols, etc.) et chaque fois que les données changent, les éléments d'affichage sont notifiés avec de nouvelles données et ils affichent les dernières données en conséquence.[![o1](https://media.geeksforgeeks.org/wp-content/uploads/ObserverPatternSet-1.png)](https://media.geeksforgeeks.org/wp-content/uploads/ObserverPatternSet-1.png)

Vous trouverez ci-dessous l'implémentation java de cette conception.

_filter_none_

_Éditer_

_play_arrow_

_luminosité_4_

`// Java implementation of above design for Cricket App. The`

`// problems with this design are discussed below.`

`// A class that gets information from stadium and notifies`

`// display elements, CurrentScoreDisplay & AverageScoreDisplay`

`class` `CricketData`

`{`

`int` `runs, wickets;`

`float` `overs;`

`CurrentScoreDisplay currentScoreDisplay;`

`AverageScoreDisplay averageScoreDisplay;`

`// Constructor`

`public` `CricketData(CurrentScoreDisplay currentScoreDisplay,`

`AverageScoreDisplay averageScoreDisplay)`

`{`

`this``.currentScoreDisplay = currentScoreDisplay;`

`this``.averageScoreDisplay = averageScoreDisplay;`

`}`

`// Get latest runs from stadium`

`private` `int` `getLatestRuns()`

`{`

`// return 90 for simplicity`

`return` `90``;`

`}`

`// Get latest wickets from stadium`

`private` `int` `getLatestWickets()`

`{`

`// return 2 for simplicity`

`return` `2``;`

`}`

`// Get latest overs from stadium`

`private` `float` `getLatestOvers()`

`{`

`// return 10.2 for simplicity`

`return` `(``float``)``10.2``;`

`}`

`// This method is used update displays when data changes`

`public` `void` `dataChanged()`

`{`

`// get latest data`

`runs = getLatestRuns();`

`wickets = getLatestWickets();`

`overs = getLatestOvers();`

`currentScoreDisplay.update(runs,wickets,overs);`

`averageScoreDisplay.update(runs,wickets,overs);`

`}`

`}`

`// A class to display average score. Data of this class is`

`// updated by CricketData`

`class` `AverageScoreDisplay`

`{`

`private` `float` `runRate;`

`private` `int` `predictedScore;`

`public` `void` `update(``int` `runs,` `int` `wickets,` `float` `overs)`

`{`

`this``.runRate = (``float``)runs/overs;`

`this``.predictedScore = (``int``) (``this``.runRate *` `50``);`

`display();`

`}`

`public` `void` `display()`

`{`

`System.out.println(``"\nAverage Score Display:\n"` `+`

`"Run Rate: "` `+ runRate +`

`"\nPredictedScore: "` `+ predictedScore);`

`}`

`}`

`// A class to display score. Data of this class is`

`// updated by CricketData`

`class` `CurrentScoreDisplay`

`{`

`private` `int` `runs, wickets;`

`private` `float` `overs;`

`public` `void` `update(``int` `runs,``int` `wickets,``float` `overs)`

`{`

`this``.runs = runs;`

`this``.wickets = wickets;`

`this``.overs = overs;`

`display();`

`}`

`public` `void` `display()`

`{`

`System.out.println(``"\nCurrent Score Display: \n"` `+`

`"Runs: "` `+ runs +``"\nWickets:"`

`+ wickets +` `"\nOvers: "` `+ overs );`

`}`

`}`

`// Driver class`

`class` `Main`

`{`

`public` `static` `void` `main(String args[])`

`{`

`// Create objects for testing`

`AverageScoreDisplay averageScoreDisplay =`

`new` `AverageScoreDisplay();`

`CurrentScoreDisplay currentScoreDisplay =`

`new` `CurrentScoreDisplay();`

`// Pass the displays to Cricket data`

`CricketData cricketData =` `new` `CricketData(currentScoreDisplay,`

`averageScoreDisplay);`

`// In real app you would have some logic to call this`

`// function when data changes`

`cricketData.dataChanged();`

`}`

`}`

**Production:**

  

  

Affichage du score actuel:  Nombre de pistes: 90 Guichets: 2 Plus: 10.2
 Affichage du score moyen: Taux d'exécution: 8,823529 PredictedScore: 441

**Problèmes avec la conception ci-dessus** **:**

-   CricketData contient des références à des objets d'éléments d'affichage concrets même s'il n'a besoin d'appeler que la méthode de mise à jour de ces objets. Il a accès à trop d'informations supplémentaires qu'il n'en a besoin.
-   Cette déclaration "currentScoreDisplay.update (exécute, guichets, overs);" viole l’un des principes de conception les plus importants: «Programmez les interfaces, pas les implémentations». car nous utilisons des objets concrets pour partager des données plutôt que des interfaces abstraites.
-   CricketData et les éléments d'affichage sont étroitement liés.
-   Si à l'avenir une autre exigence entre en jeu et que nous avons besoin d'ajouter un autre élément d'affichage, nous devons apporter des modifications à la partie non variable de notre code (CricketData). Ce n'est certainement pas une bonne pratique de conception et l'application peut ne pas être en mesure de gérer les modifications et pas facile à maintenir.

**Comment éviter ces problèmes?**  
Utiliser le modèle d'observateur

**Modèle d'observateur**

Pour comprendre le modèle d'observateur, vous devez d'abord comprendre le sujet et les objets observateurs.

La relation entre le sujet et l'observateur peut facilement être comprise comme une analogie avec l'abonnement à un magazine.

-   Un éditeur de magazine (sujet) est dans l'entreprise et publie des magazines (données).
-   Si vous (utilisateur de données / observateur) êtes intéressé par le magazine auquel vous vous abonnez (inscrivez-vous), et si une nouvelle édition est publiée, elle vous est livrée.
-   Si vous vous désinscrivez (désinscription), vous ne recevez plus de nouvelles éditions.
-   L'éditeur ne sait pas qui vous êtes et comment vous utilisez le magazine, il vous le livre simplement parce que vous êtes abonné (couplage lâche).

**Définition:**

Le modèle d'observateur définit une dépendance un à plusieurs entre les objets de sorte qu'un objet change d'état, tous ses dépendants sont notifiés et mis à jour automatiquement.

**Explication:**

  

  

-   Une dépendance à plusieurs se situe entre le sujet (un) et l'observateur (plusieurs).
-   Il existe une dépendance car les observateurs eux-mêmes n'ont pas accès aux données. Ils dépendent du sujet pour leur fournir des données.

**Diagramme de classe:![o2](https://media.geeksforgeeks.org/wp-content/cdn-uploads/o2.png)**

Source de l'image: [Wikipedia](https://en.wikipedia.org/wiki/Observer_pattern)

-   Ici, l'observateur et le sujet sont des interfaces (peut être n'importe quel super type abstrait pas nécessairement une interface Java).
-   Tous les observateurs qui ont besoin des données doivent implémenter une interface d'observateur.
-   La méthode notify () dans l'interface d'observateur définit l'action à entreprendre lorsque le sujet lui fournit des données.
-   Le sujet maintient un observateurCollection qui est simplement la liste des observateurs actuellement enregistrés (abonnés).
-   registerObserver (observer) et unregisterObserver (observer) sont des méthodes pour ajouter et supprimer respectivement des observateurs.
-   notifyObservers () est appelé lorsque les données sont modifiées et que les observateurs doivent recevoir de nouvelles données.

**Avantages:**  
fournit une conception faiblement couplée entre les objets qui interagissent. Les objets faiblement couplés sont flexibles avec des exigences changeantes. Ici, un couplage lâche signifie que les objets en interaction devraient avoir moins d'informations les uns sur les autres.

Le modèle d'observateur fournit ce couplage lâche comme:

-   Le sujet sait seulement que l'observateur implémente l'interface Observer. Rien de plus.
-   Il n'est pas nécessaire de modifier le sujet pour ajouter ou supprimer des observateurs.
-   Nous pouvons réutiliser les classes sujet et observateur indépendamment les unes des autres.

**Désavantages:**

-   Fuites de mémoire causées par [un problème d'écoute Lapsed en](https://en.wikipedia.org/wiki/Lapsed_listener_problem) raison d'un registre explicite et de la désinscription des observateurs.

**Quand utiliser ce modèle?**  
Vous devez envisager d'utiliser ce modèle dans votre application lorsque plusieurs objets dépendent de l'état d'un objet, car il fournit une conception soignée et bien testée pour celui-ci.

**La vraie vie utilise:**

-   Il est largement utilisé dans les boîtes à outils d'interface graphique et dans l'écouteur d'événements. En java, le bouton (sujet) et onClickListener (observateur) sont modélisés avec un modèle d'observateur.
-   Réseaux sociaux, flux RSS, abonnement par e-mail dans lequel vous avez la possibilité de suivre ou de vous abonner et de recevoir la dernière notification.
-   Tous les utilisateurs d'une application sur le Play Store sont avertis en cas de mise à jour.
