## OOP Design Patterns

Design patterns are typical solutions to commonly occurring problems in software design. They are like pre-made blueprints that you can customize to solve a recurring design problem in your code.

All patterns can be categorized by their intent, or purpose.
- **Creational patterns**
- **Structural patterns**
- **Behavioral patterns**

In this lecture, you'll learn the following design patterns:

- Singleton
- Decorator
- Adapter
- Template
- Strategy
- Observer
- Proxy 
- Factory

By the end of this lecture, you'll have a better understanding of the Design Patterns in Ruby.

---

### Singleton

Singleton is a creational design pattern, which ensures that only one object of its kind exists and provides a single point of access to it for any other code.

```rb
class Singleton
  def self.new
    @singleton ||= super
  end
end

p Singleton.new
p Singleton.new
p Singleton.new

p Singleton.new.object_id
p Singleton.new.object_id
p Singleton.new.object_id

```

---

### Decorator

The Decorator pattern allows us to add behavior to a given object without having to add that behavior to the class of the object.

```rb
class Cat
  attr_reader :name, :age

  def initialize(name, age)
    @name = name
    @age = age
  end
end

cat = Cat.new('Baffy', 10)
p cat.name

class CatDecorator
  attr_reader :cat

  def initialize(cat)
    @cat = cat
  end

  def full_name
    "!!! #{cat.name} #{cat.age}!!!"
  end
end

p CatDecorator.new(cat).full_name

```

---

### Adapter

Adapter is a structural design pattern, which allows incompatible objects to collaborate.

```rb
class Cat
  def meow
    p 'Meow'
  end
end

class Dog 
  def bark
    p 'Bark'
  end
end

cat = Cat.new 
dog = Dog.new

class CatAdapter
  def initialize(cat)
    @cat = cat
  end

  def say_something
    @cat.meow
  end
end

class DogAdapter
  def initialize(dog)
    @dog = dog
  end

  def say_something
    @dog.bark
  end
end

dog = DogAdapter.new(dog)
cat = CatAdapter.new(cat)

dog.say_something
cat.say_something

```

---

### Template

Template Method is a behavioral design pattern that allows you to defines a skeleton of an algorithm in a base class and let subclasses override the steps without changing the overall algorithm’s structure.

```rb
class AnimalTempate

  def run
    create_animal
    create_passport
    find_owner
    sell_animal
  end

  def create_animal
  end

  def create_passport
  end

  def find_owner
  end

  def sell_animal
  end

end

class Cat < AnimalTempate
  def create_animal
    p 'Cat was created'
  end

  def create_passport
    p "Cat's passport was created"
  end

  def find_owner
  end

  def sell_animal
  end
end

class Dog < AnimalTempate
  def create_animal
    p 'Dog was created'
  end

  def create_passport
    p "Dog's passport was created"
  end

  def find_owner
  end

  def sell_animal
  end
end

Dog.new.run
Cat.new.run

```

--- 

### Strategy

Strategy is a behavioral design pattern that turns a set of behaviors into objects and makes them interchangeable inside original context object.

```rb
# first example

def hello
  p '!!!!'
  yield
  p '!!!!'
end

hello { p 'AAA' }
hello { p 'BBB' }

# second example

# What we have at the beginning

class AnimalOrchestra
  def play_music
    p 'Start playing'
    if cat?
      p "Meow"
    elsif dog?
      p "Bark"
    end
    p 'Finish playing'
  end
end

# What we want to achieve

class AnimalOrchestra
  def initialize(strategy)
    @strategy = strategy
  end

  def play_music
    p 'Start playing'
    @strategy.animal_sound
    p 'Finish playing'
  end
end

class CatStrategy
  def animal_sound
    p "Meow"
  end
end

class DogStrategy
  def animal_sound
    p "Bark"
  end
end

cat = CatStrategy.new
dog = DogStrategy.new

AnimalOrchestra.new(dog).play_music
```

---

### Observer

“Define a one-to-many dependency between objects so that when one object changes state, all of its dependents are notified and updated automatically.”

```rb
# first example

puts 'A'
notify

# second example 

# OBSERVER

class CatFactory

  def initialize
    @potential_owners = []
  end

  def born
    # some_logic
    notify_potential_owners
  end

  def notify_potential_owners
    @potential_owners.each do |owner|
      owner.notify
    end
  end

  def add_potential_owner(owner)
    @potential_owners << owner
  end

end

class PotentionOwner
  def initialize(name)
    @name = name
  end

  def notify
    p "Dear, #{@name}, a new cat was born"
  end
end

nik = PotentionOwner.new('Nik')
alex = PotentionOwner.new('Alex')

cat_factory = CatFactory.new
cat_factory.add_potential_owner(nik)
cat_factory.add_potential_owner(alex)
cat_factory.born

```

---

## Proxy

Proxy is a structural design pattern that provides a placeholder for another object to control access to it.

```rb

class Cat
  def meow 
    p 'meow'
  end
end

class CatProxy
  def initialize(cat)
    @cat = cat
  end

  def meow
    @cat.meow if access?
  end

  def access?
    true
  end
end

CatProxy.new(Cat.new).meow

```

---

## Factory

Factory method is a creational design pattern which solves the problem of creating product objects without specifying their concrete classes.

```rb
class CarFactory
  def create(name)
    case name
    when 'BMW'
      BMW.new
    when 'KIA'
      KIA.new
    when 'LADA'
      LADA.new
    end
  end
end

class BMW
  def build
    p 'BMW was built'
  end
end

class KIA
  def build
    p 'KIA was built'
  end
end

class LADA
  def build
    p 'LADA was built'
  end
end 

# BMW.new.build
CarFactory.new.create('LADA')

```

---

### Links

- https://refactoring.guru/ru/design-patterns/ruby

---

### Books

- https://www.amazon.com/Head-First-Design-Patterns-Brain-Friendly/dp/0596007124
- https://refactoring.guru/ru/design-patterns/book
- https://www.amazon.com/Design-Patterns-Ruby-Russ-Olsen/dp/0321490452

P.S. All books are available on the Google Drive Disk. Ask the link in your Telegram chat. 

### Questions
