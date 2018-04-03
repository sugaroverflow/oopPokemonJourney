title: My Presentation
class: animation-fade
layout: true

---
class: impact

.contain[![ooptitle](assets/ooptitle.png)]
.responsive[![journeytitle](assets/journeytitle.png)]

---
class: concept

# Hi I'm Fatima

.col-6[
## @sugaroverflow
- Digital Echidna
- Drupal Diversity & Inclusion

.logo[![DE logo](assets/de_logo.png)]
.logo[![DD&I logo](assets/ddi_logo.png)]
]

.col-6[
.contain.rounded-profile[![photo of fatima](assets/fatima.jpeg)]
]
---

# OOP is a way of organizing our code.
## modular
## reusable
## flexible

???

- Instead of writing code for each trainer to be able to have a starter pokemon, do battle, and collect badges, we can create a 'trainer' class.

- The trainer class can contain methods for doing battle, collecting badges, and catching pokemon. These are things that all trainers can do. The properties of a trainer might be their name and which city they came from - but each trainer can have a different name a different origin city.

- In this OOP way, we can write one chunk of code to hanlde all the aspects of a trainer - without writing specific code for each trainer to be able to catch pokemon, do battle, etc.

- Being able to create this container of a generic Pokemon trainer and extend it into specific cases is OOP. Instead of creating 3 separate pokemon trainers and building the functionality for having pokemon or badges three times, we can create one trainer and use it to share these traits.

---
class: center, story

# The Journey Begins

.contain[![journey](assets/journey.png)]

???
- Visit Prof Oak
- Choose our starter pokemon - Pikachu!
- Let's take a look at our Pikachu to learn more about it.

---
# Our first Pokemon!
## Pikachu
### type: electric
### attack: thunderbolt

???
- electric pokemon
- electric shock attack

(T) Now we want to model this data in code
OOP gives us a way of doing that called classes!
---

# Classes are like blueprints
## Properties
### data points

## Methods
### class-specific functions


???


(T) Lets create a Pokemon class!

----

# Creating a Pokemon Class

```php
class Pokemon {
  public $name;
  public $type;

  public function attack() {
    /* do something */
    return $attack;
  }
}
```

???
(T) In order to create a pokemon and give it a name and type, we need to use something special - a constructor - a PHP magic method.
---

# Constructing a Pokemon
### PHP provides magic method: `__construct()`

```php
class Pokemon {
  public $name;
  public $type;

  public function __construct($name, $type)
  {
      $this->name = $name;
      $this->type = $type;
  }
}
```

???
(T) So now we have our class, how do we create an actual Pokemon object?

---
# Creating a Pokemon Object

```php
$pikachu = new Pokemon('Pikachu', 'Electric');
```

```php
$pikachu->attack();
```


???

(T) Lets take a look at an example of a class in Drupal core.
---
# Classes & Objects in Drupal

```php
class TranslatableMarkup extends FormattableMarkup { ... }

```

```php

class Translation extends AnnotationBase {

  protected $translation;

  public function __construct() {
    $this->translation = new TranslatableMarkup($string, $arguments, $options);
  }

}

```

???


(T) Back to our story…
We’ve been travelling for a while now… a wild Pokemon appears!

---
class: center, story
# A Wild Pokemon Appears!

.center.contain[![wildpokemon](assets/wildpokemon.jpg)]

???
- Pokemon battle
- capture!
(T) Lets analyze our Pokemon to understand them better

---
## Pikachu
### Electric
### Thunderbolt

## Oddish
### Grass
### Poison Fire

???

- Lets map what we know
- It looks like we might modify our Pokemon class to account for the different types and how they'll change in the future.
- There's an OOP concept that makes this much easier for us - Inheritance!

(T) Lets look at inheritance!
---

# Inheritance is about sharing

## parent class
- base class

## child classes
- override methods or properties


???
- Inheritance is…
-

(T) Let's look at some Pokemon Inheritance!


---
# Parent Pokemon Class

```php

class Pokemon {
  public function attack() {
    return $attack;
  }
}
```

---

# Extending the Pokemon Class

```php

class ElectricPokemon extends Pokemon {
  public function attack() {
    return $electric_attack;
  }
}

```

---
# Extending the ElectricPokemon class

```php
class Pikachu extends ElectricPokemon {
  public function attack() {
    return 'Thunderbolt!';
  }
}
```

???
- to change the behaviour of an existing method or property.


---


# Inheritance in Drupal

```php
interface WidgetInterface extends WidgetBaseInterface {
   public function formElement(...);
}
```

```php
abstract class WidgetBase implements WidgetInterface { }
```

```php
class RangeWidget extends WidgetBase {
  public function formElement(FieldItemListInterface...) {

    $element['from'] = [ ... ]
    $element['to'] = [ ... ]
  }
}
```



???

- Here formElement() actually comes from WidgetBaseInterface

---
class: story, center

# Gym Battle!

.contain[![battle](assets/battle.png)]

???
- lose the battle
- lack of strategy
- need to learn more about the strengths and weakness of our pokemons
  - add a weakness and strength property

---
# Comparing our Pokemon
## Pikachu
### Water (str)
### Ground (wkn)

## Oddish
### Water (str)
### Fire (wkn)

???
- Mapping what we know
- Different pokemon have different str and wkn
- If we want to add this to our pokemon class - we need to be able to retrieve this information quickly and easily.

(T) PHP provides more magic methods for this!

---

# Getting data from our Pokemon
## PHP magic methods:
-  `__get()`
-  `__set()`

```php

class Pokemon {

  public function getWeakness() {
    /* do something */
    return $weakness;
  }

  public function setStrength($strength) {
    /* do something */
    $this->strength = $strength;
  }

}
```

---
# Getters and Setters in child classes:

```php
class ElectricPokemon extends Pokemon {

  $str = 'grass';
  $wkn = 'water';

  // (constructor with name and type)

  public function getStrength() {
    return $this->str;
  }
  public function getWeakness() {
    return $this->wkn;
  }
}
```

---
# Getters/Setters in Drupal

```php

class RouteMatch implements RouteMatchInterface {
  public function getParameters() {
    return $this->parameters;
  }
}
```

```php
$params = \Drupal::routeMatch()->getParameters();
```

???
An example that I've been using recently.

(T) Now that we can get and set our strength, let's see how we use with our pokemon objects.

---

# Using a Pokemon object

```php
$pokemon = new Pokemon('Pikachu', 'Electric');
$pokestr = $pokemon->getStrength();
```

```php
$pikachu = new ElectricPokemon('Pikachu');
$pikachuStrength = $pikachu->getStrength();
```

???

- but hey we don’t want to just create “Pokemon” anymore - since we have the ability to create specific types.
- -generic pokemon can't be created, but specific pokemon types can be.


(T) How do we create a class that can't be instantiated (or created an object of) --- OOP gives us this with Interfaces!

---

# Interfaces are like contracts
## - all methods are public
## - the class must implement the methods

???

- create code that specifies what classes must implement
- but without defining those methods
- same way as a class
- all methods must be public (just a rule)

- generic pokemon can't be created, but specific pokemon types can be.


---
class: concept
title: Pokemon | Interface

# Creating a Pokemon Interface

```php
interface PokemonInterface {

  public function setPokemonName($name);
  public function setPokemonType($type);

  public function getPokemonName();
  public function getPokemonType();

  public function attack();
  public function getStrength();
  public function getWeakness();

}

```

---
# Implementing a Pokemon Interface

```php
class ElectricPokemon implements PokemonInterface
```

--

```php
class Pikachu extends ElectricPokemon
```

???
- to change the behavior of existing property or method in the new class
- just overwrite in the new class with what you need

- extends keyword
- interface keyword
- empty method bodies
- pokemon - electric pokemon - pikachu.

(T) Let's look a little more closely at our ElectricPokemon class implementing PokemonInterface

---

# Implementing a Pokemon Interface

```php
class ElectricPokemon implements PokemonInterface {

  public function getStrength() {
    /* do something */
    return 'Water';
  }

  public function getWeakness() {
    /* do something */
    return 'Grass';
  }
}
```

???

- Yay, we have a PokemonInterface now.
- On we go.

---
# Interfaces in Drupal

```php
interface FormInterface {
  public function getFormId();
}
```

```php
abstract class FormBase implements FormInterface { }
```

```php
class UserLoginForm extends FormBase {
  public function getFormId() {
    return 'user_login_form';
  }
}
```



---
class: story, center

# Your Pokemon is evolving!

.contain[![evolve](assets/evolve.jpg)]

???
- suddenly, your Poliwhirl is evolving -> Poliwrath - awesome!
- but how can we add this ability to our Pokemon classes?
- Not all Pokemon can evolve so we can't add to the interface.
- some evolve in different ways - stone, battle, etc and this depends on the exact Pokemon - not the type.
- how can we model this ability to evolve without putting it in our base class.

(T) PHP gives us this awesome ability to use snippets of code with Traits!

---

# Traits are like code snippets
## - code reuse
## - avoid inheritance
## - cannot be instantiated

???
- code copy pasta
- PHP method of code reuse
- for single inheritance libraries
- reduces limitations of single inheritance
- similar to a class
- can't create a trait on it's own

---
# Creating a Pokemon Evolution Trait

```php
trait PokemonEvolutionTrait {

  public function evolvesTo() {
    return $nextPokemonStage;
  }
}
```

--

```php
class Poliwhirl extends WaterPokemon {
  use EvolutionTrait;

  public function evolve() {
    // to figure out the next evolution stage
    $nextStage = $this->evolvesTo();
  }
}
```

---

# Traits in Drupal

```php

trait StringTranslationTrait {
  protected function t(...) {
    return new TranslatableMarkup($string, $args,
     $options, $this->getStringTranslation());
  }
}
```

```php
abstract class PluginBase extends ComponentPluginBase {
  use StringTranslationTrait;
}
```


---
class: story, center

# You won your first badge!

![won badge](assets/badge.jpg)

???



---


# plugins are like functional lego blocks

## many types of plugins
## different behaviors | common interface


???

Plugins implement different behaviors via a common interface.

- annotated, yaml (menus, routes, and services), hook, discovery, static

There are many types of plugins - we're going to focus on the "annotated type" for things like blocks, views, rules.



(T) Lets take a look at what a Pokemon plugin for managing badges would look like

---

# Pokemon | Plugins

```php

abstract class PokeBadgePluginBase extends PluginBase
 implements PokePluginInterface {
    abstract public function isBadgeEarned();
}

```

--

```php

class DrupalBadge extends PokeBadgePluginBase {
  public function isBadgeEarned(){
    // do stuff
    return TRUE;
  }
}

```

???
In order to make a custom plugin, we'd have to do a couple of things, but to save some time we're going to assume there exists a PokeBadgePluginBase which provides the functionality which means the interface and the base are also provided (this is making an assumption)

- to create a custom plugin:
Annotation Plugin Definition
Plugin Manager Service
Plugin Interface
Plugin Base
Example Implementation
Controller (optional)

(T) Lets look at an example in Drupal
---

# Plugins in Drupal

```php
abstract class BlockBase {
    public function build() {
      // does basic stuff
      return $build;
    }
}
```

```php
class CustomBlock extends BlockBase {
  public function build() {
    // custom stuff
    return $build;
  }
}
```

???

annotated plugin - most common

drupal provides a lot of plugin bases.
Most plugins will contain a fair amount of boiler plate code that is the same for almost all plugins of that type,

(T) Back to story!
---
class: story, center

# To be the very best
.contain[![league](assets/trainercard_card.png)]

???

???
Now that you've won a lot of battles and some fame, you've been invited to compete!


Before you can join the competition, you need to submit your pokemon trainer profile with all of your pokemon's stats.

Let's say we've been saving those stats into a database somewhere - and now, we want to retrieve them.

(T) OOP provides us a functionality for "retreiving things" in a pluggable way.

---
class: concept
title: OOP | Services

# services are like swappable operations

## - same function | swappable code
## - globally available
## - usually an interface defining methods

???
Services provide the same functionality, and are interchangeable, differing only in their internal implementation.

package reusable functionality in one place to perform an operation like sending an email or database query.
- the operation always stays the same

 ideally, there should also be an interface that defines the methods that may be called.

"service" (such as accessing the database, sending email, or translating user interface text)

(T) Lets look at our Pokemon Service!
---
# Creating a Pokemon Service

```php

class PokeDataService implements PokeDataInterface {

  public function getYearlyStats(PokemonInterface $pokemon, int $year) {
    // does query stuff
    return $array_of_data;
  }
}
```

???
- creating a pokemon service that retrieves data about our pokemon for us - their wins, losses, strengths, and weaknesses.

we are going to make the assumption that there exists a "PokeDataInterface" which defines an interface for generating data from the pokedatabase for pokemons.

Lets say we want to scope out some data on our opponents.

Our service then implements this interface and provides the functionality.

(T) How do we call our service?

---
# Calling our Pokemon Service

```php
$pikachu = new Pokemon('Pikachu', 'Electric');

```

--

```php
$pokeDataHelper= \Drupal::service('pokemon.pokedataservice');
```

--

```php
$data = $pokeDataHelper->getYearlyStats($pikachu, '2018');
```


---

# Services in Drupal

## Drupal core provides a lot of services

### `core.services.yml`


```php
  current_user:
    class: Drupal\Core\Session\AccountProxy
```

```php
$user = \Drupal\user\Entity\User::load(\Drupal::currentUser();
```

---

# Services in Drupal are swappable

```php
  email.validator:
    class: Egulias\EmailValidator\EmailValidator
```

```php
class ContactFormEditForm extends EntityForm {

  if ($this->emailValidator->isValid($recipient)) {
      //do stuff
  }

}
```

---

# When possible, inject your services

## - pass as arguments to a constructor
## - or use setter methods


???
- preferred method for accessing and using services in Drupal 8 and should be used whenever possible.
- Rather than calling out to the global services container, services are instead passed as arguments to a constructor or injected via setter methods.
- Many of the controller and plugin classes provided by modules in core make use of this pattern and serve as a good resource for seeing it in action.

- dependency injection
- using services.

(T) So how do we inject our Pokemon Service?
---
# Pokemon Dependency Injection

```php
use Drupal\pokemon\PokeDataService;

class ElectricPokemon extends Pokemon {

  protected $PokeDataService;

  public function __construct(PokeDataInterface $PokeDataService) {
    $this->$PokeDataService = $PokeDataService;
  }

  public static function create(ContainerInterface $container) {
    return new static(
      $container->get('pokemon.pokedataservice')
    );
  }
}
```

---

# Injecting services in Drupal

```php
class myCustomForm extends FormBase {

  protected $account;

  public function __construct(AccountInterface $account) {
    $this->account = $account;
  }

  public static function create(ContainerInterface $container) {
    return new static(
      $container->get('current_user')
    );
  }
}
```

---
class: story, center
# The Adventure Continues

.contain[![adventure continues](assets/topdown.png)]

???
- There's a lot out there in OOP and as you do more backend work, you'll discover new and interesting things! and the OOP adventure will continue.

- I hope this session helps to provide a foundation for the basics and from there you can build as you learn.

---
# Thank you!
## @sugaroverflow
### bit.ly/oop-midcamp-2018
