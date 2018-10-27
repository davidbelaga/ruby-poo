# Intro à la Programmation Orientée Objet dans Ruby

## Objectifs pédagogiques
* Expliquer la relation entre `.new()` et `def initialize()`
* Savoir si une donnée serait mieux stockée dans une variable locale, d'instance ou de classe
* Expliquer si l'accessibilité de cette donnée est définie au mieux par `attr_accessor`, `attr_reader`, `attr_writer` ou aucune de ces expressions
* Définir précisément les variables d'instance et de classe
* Proposer deux manières de définir des méthodes de classe

## Les bases: Qu'est-ce que la POO?
Ruby est un langage orienté objet. Cela veut dire que cela a été conçu sur l'idée que le développeur construira son application en passant essentiellement par des objets.

De la même manière que vous l'avez appris avec le JSOO (JavaScript orienté objet), un objet est une collection d'attributs reliés (propriétés) et de méthodes (comportements). Imaginez un objet comme une petite machine avec des écrans affichant un texte et des boutons à pousser.

Lorsqu'on écrit une application orientée objet, on écrit les plans de ces machines, et ensuite on écrit une suite d'événements, qui sera lancée par les utilisateurs, et qui permettra aux machines d'interagir les unes avec les autres.

Une grande partie du code que vous allez voir aujourd'hui est très similaire à ce que vous avez vu la dans le cours de JSOO la semaine dernière. Le concept de classe existe depuis quelques années déjà, mais n'a été introduit dans JavaScript que très récemment (ECMAScript 2016/ES6). Utilisez ces connaissances pour avancer dans le cours d'aujourd'hui!

## A FAIRE: Le Processus POO (10 minutes / 0:10)
Nous avons expliqué sommairement en quoi la POO est un paradigme, mais nous n'avons pas expliqué comment réduire un problème en un ensemble d'objets.

### Exemple: Le Monopoly
> "Le Monopoly est un jeu où les joueurs cherchent à faire fortune à travers les biens immobiliers et l'argent.
* plateau
* joueurs
* jetons
* cartes de propriété
* l'argent
### Exemple: Facebook
> "Facebook est une application où des utilisateurs peuvent poster des statuts et ajouter des amis.

* utilisateurs
* statuts
* amis

Décomposer ses idées te donnera une idée de ce que peuvent être les objets.

Prends 10 minutes avec un partenaire pour trouver au moins trois types d'objets qui pourraient t'aider à créer les exemples d'applications qui suivent. Ajoute tes réponses en commentaire à la fin de ce cours. Nous répondrons aux réponses comme dans un cours.


1. Amazon
2. Une application qui attribue des notes aux devoirs maisons
3. Une application qui note les présences.
3. Lyft
> Une approche utile serait de prendre les "noms" dans la description de l'application et de dire qu'ils sont des noms.

## Notre premier Object (10 minutes / 0:20)
Prenons une voiture? On a tous un modèle mental d'une voiture: elle a quatre roues, de l'essence, un guidon... Le plan de la voiture est comme une classe. Lorsque nous voyons une voiture, c'est comme une instance de classe, un véritable objet devant nous. Chaque objet a son propre plan, et est une instance de ce plan ou classe.

Une classe est un plan à partir duquel les objets sont fabriqués. En JavaScript nous avons utilisé des classes qui fonctionnent de façon très similaire que dans Ruby. Chaque objet fait à partir d'une classe est une instance de cette classe. Chaque instance de classe est un objet.

Définissons une classe Utilisateur. Nous allons utiliser binding.pry pour tester notre code.

> Remarque: pry est une gem Ruby qui nous permet de travailler avec Ruby dans un IRB (Interactive Ruby Shell). C'est comme travailler dans notre console de développeur dans le navigateur.

```
$ touch app.rb
$ gem install pry # faites ceci si vous n'avez pas encore installé pry
require "pry"
```
```ruby
class User

  def set_name_to(some_string)
    @name = un_string
  end

  def get_name
    return @name
  end

  def greet
    puts "Salut! Je m'appelle #{@name}!"
  end

end

binding.pry

puts "fin du fichier"
```

<details>
  <summary><strong>Qu'en est-il de cette classe Ruby qui ressemble à une classe JavaScript.</strong>
  </summary>
Le mot clef `classe`. La classe contient des méthodes.
</details>


Maintenant, générons des instances de cette classe...
```ruby
alice = User.new
alice.set_name_to("alice")
puts alice.get_name

madhatter = User.new
madhatter.set_name_to("Mad Hatter")
puts madhatter.get_name

alice.greet
madhatter.greet
```

#### Quelques questions
Le `User` est-il une...

* classe?
* instance?

`alice` est-elle une...

* classe?
* instance?

`User.greet` retourne une erreur. `alice.greet` marche correctement. Donc nous pouvons déduire que la méthode `greet` ne peut être appelée que sur...

* des instances de la classe User?
* la classe User elle-même?

Ainsi, est-ce que ça aurait un sens de nommer `greet` une..

* "une méthode d'instance"?
* "une méthode de classe"?

`User.new` marche bien. `alice.new` renvoie une erreur. Donc nous pouvons déduire que la nouvelle méthode ne peut qu'être appelée sur...

* des instances de la classe User?
* la classe User elle-même?

Ainsi, est-ce que ça aurait un sens de nommer `new` une..

* "une méthode d'instance"?
* "une méthode de classe"?
  
<details>
  <summary>
`class User` fonctionne. `class user` renvoie une erreur. Quelle est la règle que nous pouvons déduire sur les classes?</summary>
 > Les noms de classe commencent obligatoirement avec une majuscule.
</details>

<details>
  <summary>
 `class UserName` fonctionne. `class User Name` renvoie une erreur. Quelle est la règle que nous pouvons déduire sur les classes?</summary>
 > Les noms de classe n'ont pas d'espaces.
</details>

### Initialiser Users (10 minutes / 0:30)
<details>
  <summary><strong>Quel est le but d'un constructeur de fonctions dans les classes JavaScript?</strong></summary>
  > Initialiser n'importe quelle propriété que nous souhaitons donner à une instance de classe lorsqu'elle est créée.
</details>

Les classes Ruby ont un équivalent aux constructeurs JavaScript: la méthode initialize!

```ruby
require 'pry'

class User

  def initialize
    puts "je suis un nouveau User"
  end

  def set_name_to(some_string)
    @name = un_string
  end

  def get_name
    return @name
  end

  def greet
    puts "Salut! Je m'appelle #{@name}!"
  end

end

binding.pry

puts "end of file"
```
```ruby
alice = User.new
alice.greet

madhatter = User.new
madhatter.greet


puts alice
puts madhatter
```
<details><summary>
Quelles conclusions pouvons-nous tirer de la relation entre `def initialize` et `.new`? (Indice: elle sert le même but que la fonction constructor de JavaScript)</summary>
 >> La méthode `initialize` est lancée à chaque fois `.new`est appelé. - Utilisez `.new` pour créer un nouvel objet. - `initialize` est appelé automatiquement si c'est défini dans une classe.  - `.new` est une méthode de la classe. - `initialize` est une méthode de l'instance. - Il faut appeler `new` en premier; avant d'avoir appelé `new` il n' y a aucune instance sur laquelle on peut appeler `initialize`.
  </details>
  
<details><summary>How is this different from other User instance methods we've seen?</summary>
  >> initialize peut seulement être appelé avec la classe `.new` class (i.e. elle est lancée seulement lorsque  a été créé).
  </details>


### You Can Pass Arguments to initialize
initialize est une méthode spéciale qui est en lien avec `.new`, mais à part ça elle a le même comportement que n'importe quelle autre méthode. Cela signifie qu'on peut lui passer des arguments (à nouveau, tout comme le constructor de JavaScript)...

```ruby
require "pry"

class User

  def initialize(firstname, lastname)
    puts "Je suis un nouveau User et je m'appelle #{firstname} #{lastname}"
  end

end

binding.pry

puts "end of file"
```
```ruby
# pry
harry = User.new("Harry", "Potter")
# Je suis un nouveau User et je m'appelle Harry Potter
# => #<User:0x007f96f312b240>
```
### Variables  d'instance (10 minutes / 0:40)
Créons une méthode qui imprime le nom complet du User.

Dans Ruby, les variables normales sont accessibles seulement à l'intérieur de la méthode où elles ont été créées.

Si vous mettez un @ avant le nom de la variable, elle devient une variable d'instance et elle sera alors accessible à l'intérieur l'intégralité de l'instance  dans laquelle elle a été créée.

```ruby
class User

  def initialize(firstname, lastname)
    @firstname = firstname
    @lastname = lastname
  end

  def full_name
    return "#{@firstname.capitalize} #{@lastname.capitalize}"
  end

end
```
```ruby
# pry
harry = User.new("Harry", "Potter")
# => #<User:0x007faf3903f670 @firstname="Harry", @lastname="Potter">
harry.full_name
# => "Harry Potter"
```

### Récupérer et définir les propriétés
Afin de récupérer le prénom de Harry on ne peut pas simplement faire harry.firstname. Afin de définir le prénom de Harry on ne peut pas simplement taper harry.firstname = "Harry"

Les seules choses disponibles en dehors d'une instance sont ses méthodes. @firstname est une propriété et non une méthode. On ne peut pas accéder des données à l'intérieur d'une instance à moins qu'elle contienne des méthodes qui nous le permettent.

Afin de rendre une méthode "récupérable" ("gettable" en anglais) and "définissable" ("settable" en anglais), nous devons créer des méthodes "getter" et "setter".

```ruby
class User

  def initialize(firstname, lastname)
    @firstname = firstname
    @lastname = lastname
  end

  def full_name
    return "#{@firstname.capitalize} #{@lastname.capitalize}"
  end

  def get_firstname
    return @firstname
  end

  def set_firstname(firstname)
    @firstname = firstname
  end

end
```
```ruby
# pry
harry = User.new("Harry", "Potter")
# => #<User:0x007faf3903f670 @firstname="Harry", @lastname="Potter">
puts harry.get_firstname
# "Harry"
harry.set_firstname("Ginny")
puts harry.get_firstname
# "Ginny"
```
### attr_accessor
Souvenez-vous comment on ne pouvait pas simplement taper Harry.firstname = "un autre prénom" dans l'exemple précédent.

```ruby
class User

  def initialize(firstname, lastname)
    @firstname = firstname
    @lastname = lastname
  end

  def full_name
    return "#{@firstname.capitalize} #{@lastname.capitalize}"
  end

  def get_firstname
    return @firstname
  end

  def set_firstname(firstname)
    @firstname = firstname
  end

end
```
```ruby
harry = User.new("Harry", "Potter")
harry.firstname = "Ginny"
# Ceci envoie une erreur
harry.set_firstname("Ginny")
puts harry.get_firstname
# =>
```
Si seulement il y avait une façon de définir une classe afin de ne pas à avoir à définir une méthode getter et setter pour chaque propriété...

```ruby
class User

  attr_accessor :firstname, :lastname

  def initialize(firstname, lastname)
    @firstname = firstname
    @lastname = lastname
  end

  def full_name
    return "#{@firstname.capitalize} #{@lastname.capitalize}"
  end

end
```
```ruby
nayana = User.new("Nayana", "Davis")
nayana.firstname = "Nayana"
puts nayana.firstname
```
<details><summary>
Maintenant nous pouvons directement accéder les propriétés de l'instance User, donc nous pouvons déduire que `attr_accessor` est un raccourci qui fait quoi ?</summary>
  >> Cela créé des méthodes getter et setter pour la variable d'instance firstname.
  </details>
  
### `attr_accessor` est en fait un raccourci qui combine deux autres raccourcis
#### `attr_accessor` est `attr_reader` combiné avec `attr_writer`.

`attr_reader` rend un `attribut lisible`, `attr_writer rend an attribut écrivable. attr_accessor rend un attribute à la fois lisible ET écrivable.

Afin d'illustrer la différence entre attr_reader et attr_writer, jetons un oeil au code en-dessous.

```ruby
class User
  attr_reader :firstname
  attr_writer :lastname

  def initialize(firstname, lastname)
    @firstname = firstname
    @lastname = lastname
  end

  def full_name
    return "#{@firstname.capitalize} #{@lastname.capitalize}"
  end

end
```
```ruby
hermione = User.new("Hermione", "Granger")
hermione.firstname
# => "Hermione"
hermione.lastname
# => Error!
hermione.firstname = "Ginny"
# => Error!
hermione.lastname = "Weasley"
hermione.full_name
# => "Hermione Weasley"
```

`attr_reader`crée seulement une méthode getter. Si l'on tente hermione.firstname = "Ginny", cela va échouer.

`attr_writer`crée seulement une méthode setter. Si l'on tente puts hermione.lastname, cela va échouer.

`attr_accessor` créé des méthodes getters et setters.

> Vous allez utiliser essentiellement `attr_accessor`

---
### Pause :) (10 minutes / 1:00)
---
### A FAIRE: Monkies! (20 minutes / 1:20)
Pour le prochain exercice, clonez le repo dans le lien suivant : https://github.com/ga-wdi-exercises/oop_monkey
---

Les Attributs/Variables de Classe (5 minutes / 1:25)
Trouvons une façon de sauvegarder le nombre d'utilisateurs qui ont été créés dans leur totalité...

```ruby
class User
  attr_accessor :firstname, :lastname
  @@all = 0

  def count
    return @@all
  end

  def initialize(firstname, lastname)
    @firstname = firstname
    @lastname = lastname
    @@all += 1
  end

  def full_name
    return "#{@firstname.capitalize} #{@lastname.capitalize}"
  end
end
```
```ruby
harry = User.new("Harry", "Potter")
harry.count
# => 1
ron = User.new("Ron", "Weasley")
harry.count
# => 2
ron.count
# => 2
draco = User.new("Draco", "Malfoy")
harry.count
# => 3
ron.count
# => 3
draco.count
# => 3
```
Mais il y a quelque chose de bizarre qui se passe ici: remarquez qu'on n'est pas en train de compter le nombre de Ron, Harry ou Draco. Pensez à ce que .count pourrait retourner. Plus sur ce point prochainement...

Une variable commençant avec @@ est une variable de classe. Chaque instance de classe a la même valeur pour cette variable. Elle ne peut pas être récupérée avec `attr_accessor`. On doit créer une méthode pour y accéder.

### Les attributs et les méthodes de Classe (10 minutes / 1:40)
Un nom de méthode commençant avec le nom de la classe est une méthode de classe. Elle est rattachée à la classe elle-même, plutôt qu'aux instances. Il y a aussi des méthodes qu'on appelle sur `User`. Pour l'instant nous avons vu seulement `.new`. Cela aurait plus de sens si nous faisions `User.count` au lieu de `harry.count` afin de récupérer le nombre total d'utilisateurs.

```ruby
class User
  attr_accessor :firstname, :lastname
  @@all = 0

  def initialize(firstname, lastname)
    @firstname = firstname
    @lastname = lastname
    @@all += 1
  end

  def full_name
    return "#{@firstname.capitalize} #{@lastname.capitalize}"
  end

  # You could also define this as `def self.count`, where self represents the class
  def User.count
    return @@all
  end

end
```
```ruby
ginny = User.new("Ginny", "Weasley")
ginny.count
# => Error!
User.count
# => 1
```
### Self (5 minutes / 1:45)

`self` est une variable spéciale qui contient l'instance en cours d'un objet (comme `this` en JavaScript). C'est ainsi que l'objet fait référence à lui-même.

`self`a aussi un autre contexte : `def self.all`. Ici `self`fait référence à la classe `User`. Qu'est-ce que cela signifie? Cela veut dire que la méthode `.all`est appelée sur la classe `User`, comme `.new` et qu'elle est par conséquent une méthode de classe.

```ruby
class User
  attr_accessor :firstname, :lastname
  @@all = []

  def initialize(firstname, lastname)
    @firstname = firstname
    @lastname = lastname
    # ici, `self` fait référence à l'instance actuelle
    puts "Creating #{self.firstname}"
    @@all.push(self)
  end

  def full_name
    return "#{@firstname.capitalize} #{@lastname.capitalize}"
  end

  # Can also be written as `def User.all`
  # here, `self` refers to the class
  def self.all
    return @@all
  end

end
```
```ruby
draco = User.new("Draco", "Malfoy")
# "Creating Draco"
luna = User.new("Luna", "Lovegood")
# "Creating Luna"
bellatrix = User.new("Bellatrix", "LeStrange")
# "Creating Bellatrix"
User.all
# => [#<User @firstname="Draco">, #<User @firstname="Luna">, #<User @firstname="Bellatrix">]
```

### Pause (10 minutes / 1:55)
### A FAIRE: Un oranger (25 minutes / 2:20)
> Pris dans "Learn to Program - Second Edition" de Chris Pine : p 112, section 13.6

Faites une classe d'oranger qui a...

* une méthode hauteur qui retourne sa hauteur en pieds.
  * Sa valeur initiale devrait être déterminée par une donnée.
  * indice: vous ne devez pas nécessairement définir la méthode.
* une méthode une_annee_passe, qui, lorsqu'elle est appelée, vieillit l'arbre d'un an. Commencez l'âge à 0.
> Testez votre code.

* Chaque année, l'arbre grandit d'un pied
* Au bout de 50 ans l'arbre meurt (sa taille repart à zéro)
> Testez votre code

* Au bout des 5 premières années, l'arbre donne fruit à 20 oranges
* Vous devriez être capables de `compter_oranges`, ce qui retourne le nombre d'oranges sur un arbre
> Testez votre code

* Vous devriez être capables de `cueillir_oranges`, ce qui réduit le nombre d'oranges par 1
* Faites en sorte que votre oranger n'ait pas un nombre négatif d'oranges
* Faites en sorte que votre oranger ait 20 oranges au total après chaque nouvelle année
> Testez votre code

* Le nombre d'oranges produit par l'arbre chaque année est égal à 20 plus l'âge de l'arbre

#### Bonus

Créez une classe VergerOrangers qui gère plusieurs orangers. Elle peut...

* Vieillir tous les arbres d'un an
* Cueillir et compter tous les fruits
* Calculer la moyenne et le produit de tous les orangers

### FIN / Exercices (10 minutes / 2:30)

### Exercices supplémentaires
* Créez une classe Ruby pour un élève, initialisez le avec un nom et un âge
  * Ecrivez un getter pour le nom et l'âge, un setter pour seulement le nom
  * Créez un nouvel élève et faites la démonstration en utilisant toutes les méthodes
* Expliquez la différence entre les variables locales et les variables d'instances

### Glossaire
* **Class**: un plan des objets
* **Instance**: un objet créé avec une classe
* **Variable d'instance**: une propriété exclusive d'un objet
* **Variable de classe**: une propriété accessible par toutes les instances d'une classe
* **Méthode d'instance**: une méthode qui peut être appelée par une instance de classe (e.g., sample_user.reset_password)
* **Méthode de classe**: une méthode qui peut être appelée par une classe (e.g., User.list_user)
* `initialize`: une méthode de classe qui, lorsqu'elle est enclenchée, créé une instance et assigne les propriétés initiales
* `.new`: une méthode de classe qui, lorsqu'elle est enclenchée, lance sa méthode d'initialisation
* `attr_accessor`: un réglage qui permet to directement "get" ou "set" une variable d'instance

### Bonus: Public et privé (5 minutes / 1:50)
### A FAIRE
Dessinez une machine, réelle ou imaginaire qui des entrées (boutons, interrupteurs, claviers...) et des éléments d'affichage (cadrans, lumières, écrans...).
Déterminez ce que chaque élément accomplit.
La plupart des machines ont des jauges internes ou mémoire qui les aident à prendre des décisions: des contrôleurs de température, de voltage, des discs durs etc.
Ces derniers ne sont visibles qu'à l'intérieur de la machine: quiconque utilise la machine ne peut pas les voir. Dessinez deux d'entre eux placez-les sur votre machine. Par défaut toutes les instances et méthodes de classe sont publics, à l'exception de `def initialize`qui est privé. Ceci signifie qu'ils sont visibles pour d'autres objets. Une analogie: ce sont des fonctions qui ont leurs propres boutons à l'extérieur de la machine, comme les clignotants d'une voiture.

Il peut y avoir des méthodes qui ne doivent pas être nécessairement connus des autres objets.

```ruby
class User
  attr_accessor :firstname, :lastname
  @@all = []

  def initialize(firstname, lastname, password)
    @firstname = firstname
    @lastname = lastname
    @password = encrypt(password)
    @@all.push(self)
  end

  def full_name
    return "#{@firstname.capitalize} #{@lastname.capitalize}"
  end

  def User.all
    return @@all
  end

  private
  def encrypt(input)
    return input.reverse
  end

end
```
```ruby
harry = User.new("Harry", "Potter", "Expecto Patronum")
# #<User @firstname="Harry" @password="munortaP otcepxE">
harry.encrypt("Expecto Patronum")
# Error! Private method `encrypt`
```

Si l'on met `private` devant des méthodes signifie qu'ils peuvent être utilisés à l'intérieur de l'objet, mais qu'ils sont inaccessibles depuis l'extérieur. Une analogie: ce sont des fonctions qui n'ont pas leurs boutons à l'extérieur de la machine, comme le filtre à air de la voiture.

`private`est utile surtout pour garder les choses bien organisées. Prenons jQuery: ce langage est déjà bien assez compliqué avec des méthodes comme `.fadeOut`et `.css`. Il y a plein d'autres méthodes cachées à l'intérieur qu'on n'est pas obligé de connaître.

### Résumé: Pourquoi la POO?
#### C'est facile à comprendre
Les objets nous aident à construire des programmes qui reflètent la façon dont on pense à la réalité. Au lieu d'un tas de variables et de fonctions (programmation procédurale), nous pouvons regrouper les données et fonctions pertinentes dans des objets, et les considérer comme des unités individuelles et autonomes. Ce regroupement de propriétés (données) et méthodes est appelé encapsulation.

#### Gérer la complexité
Ceci est d'autant plus important que nos programmes deviennent de plus en plus complexes. On en peut retenir l'intégralité du code (et de ce qu'il fait) simultanément dans notre tête. Nous préférons nous concentrer sur des portions du code.

Les objets nous aident à organiser et penser nos programmes. Si je regarde le code pour un objet équipe, et si je vois que cet objet a des personnes qui y sont associées, et que ces personnes peuvent danser lorsque l'équipe danse, je ne dois pas penser ou voir le code associé à toutes ces personnes qui dansent. Je peux me contenter de placer à un niveau au-dessus : lorsque l'équipe danse, les personnes associées dansent. C'est une forme d'abstraction qui me permet de ne pas me concentrer sur les détails.

#### Garantir une cohérence
Un des effets de l'encapsulation (regrouper les données et méthodes dans des objets) est que ces objets peuvent être en contrôle de leurs données. Ceci signifie une cohérence dans les données.

Prenons l'exemple d'un compte bancaire... Je pourrais définir un compte bancaire afin qu'on ne puisse pas directement modifier le solde. Au lieu, il faut utiliser les méthodes retrait ou dépôt. Ces méthodes sont les interfaces du compte, et ils peuvent renforcer les règles de cohérence, telles que "le solde ne peut être inférieur à zéro."

#### Modularité
Si nos objets sont bien définis, alors ils interagissent de façon bien définie. Ceci nous permet de refactorer (réécrire) n'importe quel objet sans impacter d'autres endroits de notre code.

### Entrainement supplémentaire: Scrabble
Clonez cet exercice et suivez les instructions dans le Readme.

[Scrabble Word Scorer](https://github.com/ga-wdi-exercises/scrabbler)

### Ressources
* [Fiche variables](https://github.com/ga-wdi-lessons/ruby-oop/blob/master/variables.md)
* Autres exercices
  * [Monkeys](https://github.com/ga-wdi-exercises/oop_monkey)
  * [Application Config](https://github.com/ga-wdi-exercises/ruby_application_configuration)
  * [Superheroes](https://github.com/ga-wdi-exercises/superheros)
* Publications sur internet
  * WDI8, Robin
    * [Part 1](https://www.youtube.com/watch?v=-pAFSheGDr0)
    * [Part 2](https://www.youtube.com/watch?v=ZgZCtns27pE)
    * [Part 3](https://www.youtube.com/watch?v=npM249VzB0I&feature=youtu.be)
    * [Part 4](https://www.youtube.com/watch?v=su_XYcj_Cpk&feature=youtu.be)
