# Principes SOLID dans un cadre TDD

<!-- .slide: class="page-title" -->



## Plan

<!-- .slide: class="toc" -->

- [Types de tests](#/1)
- [Doublures](#/2)
- [Couverture de tests](#/3)
- [Principes TDD](#/4)
- [Ecrire des tests maintenables](#/5)
- [Principes SOLID dans un cadre TDD](#/6)
- [Code Legacy & Refactoring](#/7)
- [Aller plus loin](#/8)
- [Annexes](#/9)

Notes :



## Présentation principes SOLID

- 5 principes qu'un code doit respecter pour être :
    - plus fiable.
    - plus robuste.
    - plus extensible.

- Principes énoncés par "Uncle" Bob Martin au début des années 2000.
- Acronyme créé par Michael Feathers.

Notes :



## S : Single Responsibility Principle (SRP)

- Une classe ou une méthode ne doit faire qu'une seule chose.
- Par extension, elle ne doit avoir qu'une seule raison de changer.
- Dans le cadre TDD :
  - Tests beaucoup plus simples.
    - Partie __given__ succincte.
    - Une seule raison d'échouer.
    - Facile à comprendre.

Notes :



## O : Open/Close Principle (OCP) (1/2)

- __Open for extension, closed to modification__.
- Il doit être possible d'étendre les fonctionnalités d'un logiciel, sans en modifier le contenu.
    - Encapsulation des champs et méthodes privés.
    - Ecriture de code générique.
    - Injection des composants spécifiques, manipulés à travers des interfaces génériques.

- Meilleur exemple : les plugins.

Notes :



## O : Open/Close Principle (OCP) (2/2)

- Dans le cadre TDD :
  - Le système devient extrêmement testable.
    - Les interfaces peuvent être mockées.
    - Moins de tests nécessaires pour avoir une bonne couverture de test.

Notes :
Les plugins sont le meilleur exemple possible d'OCP car on va ajouter des fonctionnalités sans modifier le code du logiciel (firefox, chrome, eclipse, etc.)
En OOP, le polymorphisme est idéal pour ce principe (pas de if, elseif)



## L : Liskov Substitution Principle (LSP)

- Un objet de l'application peut être remplacé par n'importe quel autre objet qui en hérite.
    - Le code ne doit pas savoir quelle est l'implémentation réelle qu'il manipule.
    - Lié au concept de _programmation par contrat_.

- Dans le cadre TDD :
  - Un objet peut être remplacé par un mock sans altérer le comportement du système.

Notes :



## L : Liskov Substitution Principle (LSP) - Exemple

- `Carré` hérite de `Rectangle`
    - La hauteur et la largeur d'un rectangle peuvent être modifiées indépendamment.
    - La hauteur et la largeur d'un carré sont toujours égales.
- Dans la sous-classe `Carré`, on modifie automatiquement la largeur lorsque la hauteur est modifiée
    - Violation du LSP.
    - Le contrat du Rectange n'est pas respecté si on souhaite modifier les deux indépendamment.

Notes :



## I : Interface Segregation Principle (ISP) (1/2)

- Un client ne devrait pas dépendre de méthodes qu'il n'utilise pas.
- Les interfaces "fourre-tout" doivent être divisées en plus petites interfaces :
  - Plus spécifiques.
  - Plus cohérentes.
  - Plus claires dans le rôle qu'elles tiennent.
- Le système devient plus découplé et facile à maintenir.

Notes :



## I : Interface Segregation Principle (ISP) (2/2)

- Dans le cadre TDD :
  - Les petites interfaces sont plus simples à mocker.
  - Les tests sont plus concis, moins complexes et plus faciles à comprendre.

Notes :



## D : Dependency Inversion Principle (DIP)

- Le code doit dépendre d'abstractions, pas d'implémentations concrètes.
- Les détails dépendent de l'abstraction et non l'inverse
  - Les dépendances sont inversées.
  - Le code est découplé.
- Dans le cadre TDD :
  - Chaque composant peut être testé en isolation.
  - Les détails d'implémentation sont testés indépendamment du code appelant.

Notes :



## D : Dependency Inversion Principle (DIP) - Exemple

- Exemple : Communication avec une base de données
  - Le système dépend d'une interface.
  - L'interface est implémentée différemment selon le type de base de données.

Notes :



## SOLID - Conclusion

- Faire du TDD aide à écrire du code SOLID
  - Cela force à écrire du code découplé pour être testable en isolation (DIP).
  - Les tests ne doivent pas tous changer à chaque nouvelle fonctionnalité (SRP).
  - Les tests doivent être simples à comprendre et rapide à écrire (SRP, ISP).
- Du code non SOLID sera plus dur à tester
  - Un système difficile à tester n'est sans doute pas SOLID.

Notes :




<!-- .slide: class="page-questions" -->
