# Ecrire des tests maintenables


## Objectifs

- Le code de test est considéré comme du code de production
  - Il doit être soigné, refactorisé régulièrement et **relu**.
  - Il doit être simple, compréhensible et **maintenable**.
- Des tests non maintenables
  - Ne sont pas maintenus.
  - Tombent en erreur de plus en plus souvent (changement du code, des fonctionnalités).
  - Ne sont plus pertinents.
  - Ne sont plus lancés.


-----


## Given / When / Then

- Pattern de base des tests unitaires
  - **Given** : Préparation des mocks, des jeux de tests.
  - **When** : Exécution de la méthode à tester.
  - **Then** : Assertions pour vérifier le résultat.
- Peut être explicite (avec des sections bien distinctement identifiées) ou implicite
  - Quoi qu'il en soit, doit être visible.


-----


## Configuration

- La configuration des tests doit être la plus simple possible
  - Si la configuration est trop complexe, cela signifie que la classe à tester est trop grosse et doit être refactorisée.
  - Utiliser des fixtures.
  - Mocker seulement ce qui est nécessaire (bonne utilisation des différents types de doublures).
- Eviter de partager les jeux de données
  - Couplage fort entre les tests.
- Utiliser des frameworks uniquement si cela simplifie le code.

Notes :
Si on créer un objet dans le setup qui servira de jeu de données dans tous les tests, une modification de cet objet pour un test va impacter tous les autres.
Il faut le limiter aux objets très bien définis (utilisateur authentifié, etc.)


-----


## Tests fixtures - Problématique

- Créer un jeu de test peut être verbeux et répétitif
  - Objets créés dans chaque test.
  - La valeur des propriétés d'un objet est parfois peu importante (elle doit juste exister).
  - L'ajout d'une propriété dans un objet oblige à réécrire tous les tests.
- La création des jeux de test rend le test moins compréhensible
  - Le code qui exécute le test est noyé dans le code de préparation.
  - L'objectif du test est moins clair.


-----


## Tests fixtures - Méthodes

- Méthode qui va instancier un objet avec des valeurs par défaut.
- Très utile quand on a besoin d'un objet et que son contenu importe peu.
- Éventuellement passer un ou deux paramètres pour rendre l'objet paramétrable
  - Si trop de paramètres, la méthode a peu d'intérêt (autant utiliser un constructeur ou un builder).


-----


## Tests fixtures - Méthodes (exemple)

```java
@Test
public void should_increment_basket_price() {
  Product product = aProduct(12.0);
  Basket basket = new Basket();

  basket.add(product);

  assertThat(basket.totalPrice(), is(12.0));
}

private Product aProduct(double price) {
  Product product = new Product();
  product.setId(1L);
  product.setName("Banana");
  product.setPrice(price);
  return product;
}
```


-----


## Tests fixtures - Builder

- Pattern *Builder* pour instancier un objet.
- Très utile quand on souhaite un haut niveau de personnalisation
  - Présence de valeurs par défaut si on ne souhaite pas personnaliser un champ.

<br>
```java
@Test
public void should_increment_basket_price() {
  // Utilisation du Builder de Product
  Product product = aProduct().named("Lemon").thatCosts(12.0).build();

  Basket basket = new Basket();
  basket.add(product);

  assertThat(basket.totalPrice(), is(12.0));
}
```


-----


## Tests fixtures - Builder (exemple)

```java
public class ProductBuilder {
  private Long id = 1L;
  private double price = 0.0;
  private String name = "Banana";

  public static ProductBuilder aProduct() {
    return new ProductBuilder();
  }
  public Product build() {
    Product product = new Product();
    product.setId(id);
    product.setName(name);
    product.setPrice(price);
    return product;
  }
  public ProductBuilder named(String name) {
    this.name = name;
    return this;
  }
  [...]
}
```


-----


## Tester l'aléatoire

- Une méthode qui manipule des dates et des nombres aléatoires est difficile à tester
  - Le résultat n'est pas prévisible.
  - Impossible d'avoir des tests constants (__Flaky test__).
- Solution : externaliser l'aléatoire
  - Possibilité de mocker les dépendances et de "fixer" l'aléatoire.
  - Les tests deviennent prédictibles.


-----


## Cacher les détails d'implémentation

- Le test doit tester des comportements, pas des implémentations.
- Il ne doit pas savoir comment la méthode est implémentée
  - Ne pas tester les méthodes privées.
  - Ne pas vérifier *tous* les appels aux dépendances (seulement ceux qui font partie de la fonctionnalité).
- Risque de casser tous les tests à chaque modification de l'implémentation
  - Beaucoup de temps passé à maintenir les tests.
  - Perte de motivation.
  - Tests ignorés.


-----


## Echouer pour une seule raison

- Chaque test doit ne pouvoir échouer que pour une seule raison
  - Quelques assertions tout au plus par test.
  - Une seule action par test.
- Quand il échoue, on sait pourquoi et on peut le corriger
  - Augmente la clarté.
  - Accélère le debug.


-----


## Nommage des classes

- Il est pratique de pouvoir identifier le type d'une classe à son nom.
- Pas de solution unique
  - Il existe de nombreuses possibilités.
  - Le plus important : la cohérence et le respect de la convention.
- Exemple (Configuration par défaut Surefire/Failsafe)
  - `Foo` l'interface d'un Service.
  - `FooImpl` son implémentation.
  - `FooImplTest` son test unitaire associé.
  - [`FooImplIT` son test d'intégration associé.]

Notes :
Sandro utilise "Should" à la fin de ses classes pour être plus clair (pas besoin de le mettre en début de méthodes)
-> Force à configurer Surefire pour exécuter les tests sur des classes qui se terminent par Should
http://codurance.com/2014/12/13/naming-test-classes-and-methods/


-----


## Nommage des méthodes

- Le nom de la méthode doit décrire ce qu'elle va tester.
- Elle doit décrire le test, pas la classe testée
  - Permet de savoir ce qu'il doit tester quand il est en échec.
  - Sert de documentation sous forme de code.
  - Le nommage en soit importe peu
    - Question de cohérence et de clarté.
    - Pas de "meilleur" choix.
  - Exemple : `should_increment_basket` au lieu de `testBasket`.
- Selon l'outil, on peut même ajouter une description textuelle au test.

Notes :
Utilisation de camel case, underscores, mix des deux : peu importe


-----


## Structure

- Si une classe a beaucoup de méthodes, la classe de test peut être très grosse
  - Signe que la classe fait trop de chose.
  - Peut être signe qu'il faut refactoriser.
- Ne pas hésiter à découper la classe de test en plusieurs classes
  - Séparation par fonctionnalité.
  - Trouver un moyen pour les nommer correctement.
  - Exemple : `ProductServiceImpl_BasketTest`.


-----


## Conclusion

- Le code de test est très important
  - Il sert de documentation.
  - Il sert d'exemple.
  - Il est très souvent modifié.
- Les tests doivent donc être écrits avec autant de soin que le code de production
  - Design, revue, patterns, maintenabilité.
  - En Java : http://www.petrikainulainen.net/writing-clean-tests/
