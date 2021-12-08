## Ruby metaprogramming

Metaprogramming is a technique which allows you to write code that generates code during runtime. This mean you can even create classes, methods and so on during
the time of program's execution. It's biggest advantage is making your code much more DRYer but you have to use it with caution.

In this lecture you will learn when and how to use the metaprogramming.

### Use case 

- lots of repetative code
- necessity to prevent defafult behaviour (not raising errors, handling the method_missing etc)
- class evaluation "on the fly"

... and so on.

---

### Examples

Let's say we are going to start a new project and hiring a team. Here's the ruby code that allows us to do so:
```rb
class MyTeam
  def frontend_dev
    puts 'hired a FE developer!'
  end

  def backend_dev
    puts 'hired a BE developer!'
  end

  def project_manager
    puts 'hired a project manager!'
  end
end

MyTeam.new.frontend_dev
MyTeam.new.backend_dev
MyTeam.new.project_manager
```
This works! But what happens if we will have to hire a really big team? We'll have to run code like ```rb MyTeam.new.frontend_dev ``` as much times as the number
of people we want to hire. What if I told you that you solve this problem using metaprogramming?

```rb
class MyTeam
  def initialize(positions_to_hire)
    @positions_to_hire = positions_to_hire
  end

  def hire_a_team
    @positions_to_hire.each { |position| send(position) }
  end

  private

  def frontend_dev
    puts 'hired a FE developer!'
  end

  def backend_dev
    puts 'hired a BE developer!'
  end

  def project_manager
    puts 'hired a project manager!!'
  end
end

team_to_hire = ["frontend_dev", "backend_dev", "backend_dev", "project_manager"]
MyTeam.new(team_to_hire).hire_a_team
```
Using this technique we simply provide an array of specialist we want to hire and call methods for every object in array
using ```rb send``` (Ruby's default tool for calling methods by name).

This code already looks better. But what if we will try to hire let's say devops? Our program will crash beecause we don't have such method:
```rb undefined method `devops' for #<MyTeam:0x00007fd4f2129228> (NoMethodError) ```

Metaprogramming can help us here as well:

```rb
class MyTeam
  def initialize(positions_to_hire)
    @positions_to_hire = positions_to_hire
  end

  def hire_a_team
    @positions_to_hire.each { |position| send(position) }
  end

  def method_missing(method, *args, &block)
    puts "there is no such specialist to hire"
  end

  private

  def frontend_dev
    puts 'hired a FE developer!'
  end

  def backend_dev
    puts 'hired a BE developer!'
  end

  def project_manager
    puts 'hired a project manager!!'
  end
end

team_to_hire = ["frontend_dev", "backend_dev", "backend_dev", "project_manager", "devops"]
MyTeam.new(team_to_hire).hire_a_team
```
We simply reassigned ```rb method_missing``` for MyTeam class. This is very handy but has lot's of drawback as well and here's the biggest issue with metaprogramming:
- We can accidentally prevent program from default behaviour
- Metaprogramming code is not that easy to debug and it's not very explicit

That's why you have to use it carefully.

### Usefull links:
-----------------------------------

- https://www.toptal.com/ruby/ruby-metaprogramming-cooler-than-it-sounds
- https://github.com/dazhizhang/ruby-rails/blob/master/Metaprogramming%20Ruby%2C%202nd%20Edition.pdf

