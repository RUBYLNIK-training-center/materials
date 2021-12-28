## OOP Ruby basics

OOP has the following benefits:

- It is easy to design programs, as OOP concepts help greatly in the organization of concepts in everyday life.
- It breaks hard problems down into manageable pieces for coding.
- It is easy to test.
- It is easy for others to read and learn how the program works.

By the end of this lecture you will be able to describe:
- the basics of object-oriented programming using Ruby;
- model data with classes; 
- implement instance and class variables in Ruby programs;
- write instance and class methods in application programs;
- evaluate getters and setters in Ruby;
- implement modules within the Ruby object model; 
- add instance methods by including a module into a class; 
- add class methods by extending a class with a module; 
- create a namespace with a module;
- distinguish between prepending modules into classes and including and extending them and use modules to address multiple inheritance in Ruby.

---

## Class

Classes are abstract templates for objects. You can also say that objects are instances of classes. Classes contain the template for a set of behaviors (such as methods) and data (such as variables).

- Class

```rb
class Animal
end

```

- Instance

```rb 
Animal.new
```

- Methods
    - Instance methods

    ```rb
    class Animal
      def name
        'Cat'
      end

      def age
        12
      end
    end

    animal = Animal.new
    p animal.name # 'Cat'
    p animal.age # 12
    ```
    - Class methods

    ```rb
    class Animal
      # - First option
      def self.name
        'Cat'
      end

      # - Second option 
      class << self
        def name
          'Cat'
        end
      end
    end

    p Animal.name
    ```

    - Initialize (constructor)

    The initialize method is a special method in Ruby that is placed inside the class definition. In other languages, the initialize method is known as the "constructor."

    ```rb
    class Animal
      def initialize
        @name = 'Cat'
      end

      def name
        @name
      end
    end

    animal = Animal.new
    p animal.name
    ```

- Getters and Setters 
    - attr_reader (defines the getter)

    ```rb
    class Animal
      attr_reader :name

      def initialize
        @name = 'Cat'
      end
    end

    animal = Animal.new
    p animal.name
    ```
    
    - attr_writer (defines the setter)
    
    ```rb
    class Animal
      attr_writer :name
      attr_reader :name
    end

    animal = Animal.new
    animal.name = 'Cat'
    p animal.name
    ```

    - attr_accessor ( defines both the getter and the setter )

    ```rb
    class Animal
      attr_accessor :name
    end

    animal = Animal.new
    animal.name = 'Cat'
    p animal.name
    ```

- Inheritance
    - Is a 
    ```rb 
    class Animal
      def name
        'Animal'
      end
    end

    class Cat < Animal
    end

    p Cat.new.name # 'Animal'
    ```
    - Kind of
    
    ```rb
    module MusicPlayer
      def play
        p 'Music ...'
      end
    end

    class Car
      include MusicPlayer
    end

    Car.new.play # 'Music ..."
    ```
    - super
    - ancestors/superclass

- Method access control
    - public (default)
    ```rb 
    class Animal
      public

      def name
        'Animal'
      end
    end
    p Animal.new.name # 'Animal'
    ```
    - private
    
    ```rb
    class Animal
      def get_name
        name
      end

      private

      def name
        'Animal'
      end
    end
    p Animal.new.get_name # 'Animal'
    p Animal.new.name # 'raises NoMethodError'
    ```
    - protected

    ```rb
    # The same as private but we can call these methods on other instances of this class
    class Animal
      def get_name(animal)
        animal.name
      end

      protected

      def name
        'Animal'
      end
    end
    animal1 = Animal.new
    p Animal.new.get_name(animal1) # 'Animal'
    p Animal.new.name # 'raises NoMethodError'
    ```

---

## Module

Modules, in their simplest definition, are a way to wrap code into a bundle so the code can be reused within other code without needing to be duplicated.


- Inheritance 
    - include
    ```rb
    module Engine
      def check
        puts 'Check engine ...'
      end
    end

    class Car
      include Engine
    end

    Car.new.check
    ```
    - extend
    ```rb
    module Engine
      def check
        puts 'Check engine ...'
      end
    end

    class Car
      extend Engine
    end

    Car.check
    ```
    - prepend
    ```rb
    module Engine
      def check
        p 'Check engine ...'
      end
    end

    class Car
      prepend Engine

      def check
        p 'Do not override...'
      end
    end

    Car.new.check # 'Check engine ...'
    ```
- Namespace

```rb
module Extensions
  class Engine
  end
end

Extensions::Engine.new
```

---

### Links

- https://tadhao.medium.com/private-vs-protected-in-ruby-3ae230cc9f37

---

### Books

- https://www.amazon.com/Head-First-Ruby-Brain-Friendly-Guide/dp/1449372651
- https://www.amazon.com/Ruby-Workshop-Interactive-Approach-Learning/dp/1838642366
- https://www.rubyguides.com/ruby-book/

P.S. All books are available on the Google Drive Disk. Ask the link in your Telegram chat. 

### Interview questions
