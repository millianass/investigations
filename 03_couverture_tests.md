# Couverture de tests

## Principes

- Métrique qui mesure le code testé et celui qui ne l'est pas
  - Pourcentage de code couvert.
  - Métrique calculée pour chaque méthodes, fonctions, fichiers, classes, ...
- Besoin d'outils d'analyse.


--------


## Analyse des résultats

- Un pourcentage de couverture de code ne décrit pas la qualité des tests
  - Une couverture de code de 100% peut masquer de gros manques dans les tests    
  et la couverture réelle.
  - Au contraire une couverture de code trop faible indique clairement que le code     
  n'est pas assez testé.
  - La couverture indique uniquement le pourcentage de code exécuté lors des tests.


--------


## Analyse des résultats

- Avoir une cible définie peut être contre productif
  - Tester tous les assesseurs va faire gonfler artificiellement la     
  couverture de code sans aucune utilité.
  - Tester des cas impossibles avant de tester des comportements métiers.
- La métrique permet d'améliorer la **qualité** des tests
  - Met en évidence les zones de codes pas ou peu testées.
  - Met en évidence les tests qui ne testent rien (_Tests Liar_)


--------


## Conclusion

- Métrique très utile mais attention à l'analyse
  - Permet de repérer des zones de codes mal ou pas du tout testées.
  - Une couverture de code trop basse est un signal d'alerte.
  - 100 % de couverture de code ne veux pas dire 100% du code testé.
- Il ne faut pas viser une cible absolue
  - La qualité des tests est plus importante que leur nombre.


--------


## Mutation Testing

- Le *Mutation Testing* consiste à faire un ensemble de modifications du     
code afin de vérifier que les tests couvrent correctement le code.

- Les mutations :
  - remplacer un opérateur par un autre
  - supprimer d'une instruction
  - ...

- Si une modification du code ne met pas en echec les tests on peut     
remettre en question la couverture du code.


--------


## Mutation Testing (Génération des mutants)

- La génération des mutants :
  - Tente d'appliquer toutes des mutations possibles au code testé     
  afin de générer des mutants.
  - Si la mutation compile alors le mutant est généré.


--------


## Mutation Testing (Elimination des mutants)

-  Élimination des mutants :
  - Les tests sont alors exécutés sur les mutants.
  - Pour chaque mutant :
    - Si les tests sont tous rouges
      - les tests couvrent les modifications du code de la mutation,     
      le mutant est éliminé.
    - Si un ou plusieurs tests restent verts
      - les tests ne traitent pas la mutation, donc ils ne couvrent     
      pas correctement le code.


--------


## Mutation Testing - Conclusion

- Permet de renforcer la métrique donnée par la couverture de code.
- Très consommateur de ressources à cause des multiples mutants générés et testés.
- Potentiellement très lent.
- Impossible à faire manuellement, nécessite un outil dédié.
- S'applique uniquement sur les tests unitaires.
