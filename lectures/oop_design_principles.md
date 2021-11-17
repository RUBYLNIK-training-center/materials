## OOP Design Principles

In this lecture, you'll learn the following design principles:

- DRY
- KISS
- YAGNI
- SOLID

By the end of this lecture, you'll have a better understanding of the principles of Ruby class design and how to apply some important object-oriented design principles.

---

### DRY

DRY (don’t repeat yourself) means don’t write duplicate code, instead use Abstraction to abstract common things in one place.

```rb
p 'hello'  # any complex logic 
p 'hello'  # any complex logic 
p 'hello'  # any complex logic 
p 'hello'  # any complex logic 
p 'hello'  # any complex logic 
p 'hello'  # any complex logic 
p 'hello'  # any complex logic 

def hello # complex logic encapsulation
  p 'hello'
end

hello

# AFTER =>

hello
hello
hello
hello

```

---

### KISS

Keep it simple, stupid (KISS) is a design principle which states that designs and/or systems should be as simple as possible.

---

### YAGNI

YAGNI stands for You aren't gonna need it. This principle means you should implement only required functionalities.

---

## SOLID

SOLID is an acronym for five separate object-oriented design principles:

- The single-responsibility principle
- The open-closed principle
- The Liskov substitution principle
- The interface segregation principle
- The dependency inversion principle


---

###  The single-responsibility principle

The basic idea of the single-responsibility principle is that a class should basically serve one purpose. On the face of it, this is a good general rule, as classes built to serve a single purpose are fine and easy to use.

```rb
def hello
  calculation = 1 + 1 + 3 # any complex logic 

  puts calculation # any complex output 
end

hello

# =>

def calculation # complex logic encapsulated
  1 + 1 + 3 
end

def print_calculation # complex output encapsulated
  puts calculation
end

```

---

### The open-closed principle

The open-closed principle stipulates that a class should be open for extension, but closed for modification. An extension in Ruby's case would be adding instance variables and methods, and modification would be modifying or removing existing instance variables or methods.

```rb
class Animal
  def hello
    p 'Hello'
  end
end

class AnimalExtension < Animal
  def hello
    p 'Hello World!'
  end
end

AnimalExtension.new.hello

```

---

### The Liskov substitution principle

The Liskov substitution principle states that any place in the code where you can use an object of type T, you can also use an object of a subtype of T. In terms of Ruby, this means that any place in your code where you are using an instance of a class, you can also use an instance of a subclass without anything breaking.

```rb

class Animal
  def hello
    p 'Hello'
  end 
end

class Cat < Animal
  def hello
    # we can remove this `p` to break this principle
    p 'Hello from Cat'
  end
end

animal = Animal.new
animal.hello 

cat = Cat.new
cat.hello

# animal.hello  => cat.hello
```

---

### The interface segregation principle

The interface segregation principle states that clients should not be forced to depend on methods they do not use.

```rb
module Extension
  def task1_helper
    p 'helper'
  end 

  def task2_helper
    p 'helper 2'
  end
end

class Task1
  include Extension
end

class Task2
  include Extension
end

Task2.new.task2_helper

# AFTER => 

module Task1Extension
  def task1_helper
    p 'helper'
  end 
end

module Task2Extension
  def task2_helper
    p 'helper 2'
  end
end

```

---

### DEPENDENCY INVERSION

The dependency inversion principle states that high-level modules should not depend on low-level modules, and both high-level and low-level modules should depend on abstractions. It also states that abstractions should not depend on concrete implementations, but that concrete implementations should depend on abstractions.

```rb
class Animal
  def hello
    p 'Hello'
    # puts 'Hello'
    # print 'Hello'
    # we want .show('Hello')
  end
end

Animal.new.hello

# AFTER => 

class Puts
  def show(text)
    puts text
  end
end

Puts.new.show('puts')

class Print
  def show(text)
    print text
  end
end

Print.new.show('print')

class Animal
  attr_reader :printer

  def initialize(printer)
    @printer = printer
  end

  def hello
    printer.show('Hello')
  end
end

Animal.new(Puts.new).hello
```

----

#### Links

-

----

#### Questions

- 


