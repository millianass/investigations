# Code Legacy & Refactoring

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



## Code legacy (1/2)

- Quest-ce que le code legacy
  - Définition de Michael Feathers

> Le code legacy est un code sans test

- Il est difficile à modifier
- L'impact d'une modification n'est ni évidente, ni maitrisée

Notes :



## Code legacy (2/2)

- Le cercle vicieux
  - Pas de harnais de test.
  - Code difficile à modifier par manque de confiance.
  - Ajout de nouveau code non testé.
  - Code plus complexe.
  - Code plus difficile à modifier.
  - Moins de temps disponible.
  - Plus difficile de rajouter des tests et de refactorer le code.
  - ...

Notes :



## Refactoring

- Définition
  - Toute action qui modifie la structure d'un programme sans modifier son comportement extérieur.

- Le dilemme du refactoring

> Quand nous refactorons,
  nous avons besoin de tests
  et pour mettre des tests en place,
  nous avons souvent besoin de refactorer.

Notes :



## Pourquoi aurais-je besoin de refactorer ?

- Pour améliorer la conception du logiciel.
- Pour rendre la maintenance plus simple et aisée.
- Pour faciliter les changements.
- Pour être plus flexible.
- Pour accroître la réutilisabilité.
- Pour aider à trouver plus rapidement des bugs.

Notes :



## Quand refactorer ?

- S'il y a
  - de la duplication de code.
  - de longues méthodes.
  - une longue liste de paramètres.
  - des nommages incorrects.
  - de la désinformation.
  - du code inutile.

Notes :



## TDD & Legacy code : Comment ?

- Identifier les points de modification.
- Identifier ce que vous devez tester.
- Casser les dépendances.
- Ecrire les tests.
- Faire les modifications et refactorer.

Notes :



## Quand doit-on casser les dépendances ?

- Quand une méthode ne peut pas être éxécutée dans le harnais de tests.
- Quand une classe ne peut pas être instanciée facilement dans le harnais de tests.
- Quelques techniques
  - Extraire une interface.
  - Sous-classer et surcharger.
  - Transformer une méthode en classe.
  - ...

Notes :
 - extraire interface : créer une interface permettant d'avoir une version plus simple et plus facile implémentée (cf exercice legacy-code-extract-interface)
 - sous-classer et surcharger : dans les tests on crée une nouvelle classe étendant la classe à tester
 et on surcharge les méthodes qui nous arrange (cf exercice legacy-code-sous-classer)
 - Transformer une méthode en classe (Break out method object) : quand nous avons une méthode très compliquée
 on crée une classe avec le contenu de la méthode. Le constructeur prend exactement les arguments de la méthode,
 on change la méthode par la classe et en compile et on modifie les erreurs (cf exercice legacy-code-break-out-method-object)



## Si je ne peux pas mettre de harnais de tests

- Le pattern "Sprout class / method"
  - quand le comportement que j'ai à coder est réalisé dans une méthode ou une classe à part que je peux développer en TDD.
- Le pattern "Wrap class / method"
  - quand le comportement à ajouter est placé avant ou après une méthode. Cette dernière est développée en TDD.

- Pour aller plus loin voir "Working effectively with legacy code" de Michael Feathers.

Notes :
- Sprout method : dans la méthode legacy non testable, j'ajoute l'appel à une méthode (cf exercice legacy-code-sprout-method)
- Wrap class : quand j'ai besoin d'ajouter un comportement avant ou après une méthode non testable je crée une classe
qui étend la 1ère et ajoute ma méthode qui utilise la méthode legacy et ajoute avant ou après mon comportement (cf exercice legacy-code-wrap-method)



<!-- .slide: class="page-questions" -->
