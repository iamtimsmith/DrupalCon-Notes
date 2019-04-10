# OOP: Quest for Pokemon

>  ### Speaker: Fatima - @sugaroverflow
> - Leader Drupal Diversity
> - Rising Star Award
> - Code for Canada Fellow
> - Code & Drons @transoprot canada
> - Hobby Axe Thrower

## The Journey Begins

> ### Pikachu
> - Type: Electric
> - Attack: Thunderbolt
> - It lives in forests

### Classes are blueprints
- with _properties_ - data points 
- and _methods_ - class specific functions

### Creating a pokemon class
```
class Pokemon {
  public $name;
  public $type;
}
```

### The Constructor
- A constructor allows you to initialize your object’s properties when you instantiate an object.
- Each class needs it's own constructor

```
public function __constructor($name, $type) {
  $this-> = $name;
  $this->type = $type
}
```

### Constructing a Pokemon
```
class Pokemon {
  public $name;
  public $type;

  public function __construct($name, $type) {
    $this-> = $name;
    $this->type = $type
  }

  public function attack() {
    /* do something */
    return $attack;
  }
}
```

### Creating a pokemon object
- An object is an _instance_ of a _class_
```
$pikachu = new Pokemon('Pikachu', 'Electric');
```
```
$pikachu = attack();
```

### Classes in Drupal Core

```
class Link {
  public function __construct($text, Url $url) {
    $this->text = $text;
    $this->url = $url;
  }
}
```

### Inheritance is about sharing
- parent classes _provide_ the base properties and functionality
- child classes _can inherit_ and _override_ properties or methods
- PHP is a **single** inheritance language

```
class ElectricPokemon extends Pokemon { ... }
```
In the example above, the Electric Pokemon is inheriting the stuff in the pokemon class.

- Child classes inherit the properties and methods of the parent class but can override the parent class.
- If a class needs a lot of the same functionality and then some because there is a difference, create child class (i.e. Electric pokemon are still pokemon with all of those attributes but they have more abilities too)

### Visibility
Class members can be _public_, _protected_, or _private_
- public: accessed anywhere (any class whether inherited or not)
- private: only the class itself (can't be accessed by child classes)
- protected: only within the class itself and child classes

### Getters and Setters
- Getters and Setters should be used to set or retrieve private properties

```
class Pokemon {
  private $strength;
  private $weakness;

  public function getWeakness() {
    /* do something */
    return $this->weakness;
  }
}
```

```
$pokemon = new Pokemon('Pikachu', 'Electric');
$pokeStr = $pokemon->getStrength();
```

- Statically injecting getters and setters are bad because of performance (multiple service calls, etc). Should use dependency injection instead.
- Using dependency injection also beneficial in unit testing so you know what you'll get during the testing

### Interfaces are like contracts
- all methods are public
- the calss must implement the methods
- cannot be instatiated
- are kind of like shells/templates

```
interface PokemonInterface {
  public function attack();
  public function getStrength();
  public function getWeakness();
}
```

```
class ElectricPokemon implements PokemonInterface {
  public function attack() {
    /* do something */
    return $some_attack;
  }

  public function getStrength() {
    /* do something */
    return $strength;
  }

  public function getWeakness() {
    /* do something */
    return $weakness;
  }
}
```

### Abstract classes are like fillable PDFs
- a class that is only partially implemented
- can contain at least one abstract method
- cannot be instantiated

### Traits are like code snippets
- code reuse
- avoid inheritance
- similar to class, but cannot be instatiated

```
trait PokeEvolutionTrait {
  publlic fucntion evolve() {
    /*do something */
    return new $this-nextStage;
  }
}
```
```
class Pikachu extends ElectricPokemon {
  use PokeEvolutionTrait;
  public $nextStage = 'raichu';
}
```
```
class Raichu extends ElectricPokemon {
  /* do something */
  return 'raichu';
}
```
- To work, raichu class must exist.
- Pikachu can pull what it needs from pokemon, pull some stuff from electric pokemon stuff, and pull what it needs from evolve

### Plugins are like functional lego blocks
- many types of plugins
- different behaviors | common interface
- Unraveling the plugin system in drupal 8 | [drupalize.me](http://drupalize.me)

