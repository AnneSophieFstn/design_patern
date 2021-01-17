### Intention

-   Contrôler l'accès en écriture aux attributs de classe
-   Séparez les données des méthodes qui les utilisent
-   Encapsuler l'initialisation des données de classe
-   Fournir un nouveau type de `final`- _final après constructeur_

### Problème

Une classe peut exposer ses attributs (variables de classe) à la manipulation lorsque la manipulation n'est plus souhaitable, par exemple après la construction. L'utilisation du modèle de conception de données de classe privée empêche cette manipulation indésirable.

Une classe peut avoir des attributs mutables uniques qui ne peuvent pas être déclarés finaux. L'utilisation de ce modèle de conception permet la définition unique de ces attributs de classe.

La motivation de ce modèle de conception vient de l'objectif de conception de protéger l'état de classe en minimisant la visibilité de ses attributs (données).

### Discussion

Le modèle de conception de données de classe privée cherche à réduire l'exposition des attributs en limitant leur visibilité.

Il réduit le nombre d'attributs de classe en les encapsulant dans un seul objet Data. Il permet au concepteur de classe de supprimer le privilège d'écriture des attributs destinés à être définis uniquement pendant la construction, même à partir des méthodes de la classe cible.

### Structure

Le modèle de conception de données de classe privée résout les problèmes ci-dessus en extrayant une classe de données pour la classe cible et en donnant à l'instance de classe cible une instance de la classe de données extraite.

![Schéma des données de classe privée](https://sourcemaking.com/files/v2/content/patterns/Private_Data_class1.png)

### Liste de contrôle

1.  Créez une classe de données. Déplacez vers la classe de données tous les attributs qui doivent être masqués.
2.  Créer dans l'instance de classe principale de la classe de données.
3.  La classe principale doit initialiser la classe de données via le constructeur de la classe de données.
4.  Exposez chaque attribut (variable ou propriété) de la classe de données via un getter.
5.  Exposez chaque attribut qui changera ultérieurement via un setter.

### Source
https://sourcemaking.com/design_patterns/private_class_data
