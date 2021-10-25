# Course structure

[**Introduction**](https://github.com/RUBYLNIK-training-center/materials/blob/main/lectures/intro.md)


About Course structure

----------

**Ruby basics**
<details>
<summary>Information</summary>

Ruby basics
=====================
In Ruby, just like in real life, our world is filled with objects. Everything is an object - ```integers```, ```characters```, ```text```, ```arrays``` - everything.

To make things happen using Ruby, one always puts oneself in the place of an object and then has conversations with other objects, telling them to do stuff.

The Ideals of Ruby’s Creator
Ruby is a language of careful balance. Its creator, ```Yukihiro “Matz” Matsumoto```, blended parts of his favorite languages (Perl, Smalltalk, Eiffel, Ada, and Lisp) to form a new language that balanced functional programming with imperative programming.
He has often said that he is “trying to make Ruby natural, not simple,” in a way that mirrors life.
Building on this, he adds:

> Ruby is simple in appearance, but is very complex inside, just like our human body.

In computer programming, one of the many ways that programming languages are colloquially classified is whether the language's type system makes it strongly typed or weakly typed (loosely typed). However, there is no precise technical definition of what the terms mean and different authors disagree about the implied meaning of the terms and the relative rankings of the "strength" of the type systems of mainstream programming languages.

Dynamic Vs Static
-----------------------------------

First step to avoid confusion : Don’t mix Dynamic/Static typing with Strong/Weak typing. Ruby, for example, is dynamically and strongly typed at the same time (more on that later).
Example of a language statically typed :

```ruby
int x;
x = 3;
x = "hello"; //ERROR!
```

Example of a language dynamically typed :
```ruby
x = 3
x = "Transformers seems to be a boring movie"
x = :why_are_we_here
x = [‘Sasuke, ‘Naruto’]
x = "enough already... I think we understand"
```
When we talk about dynamic typing, we talk about a mechanism where the type of a variable can change and be resolved on the fly at the exact moment it gets parsed by the interpreter.
When we talk about static typing, we talk about a mechanism where the type of a variable is resolved in advance by the interpreter/compiler. With statically typed languages, you cannot say that x is a string and, a few lines after, that it is an integer. That’s all there is to say about it.
As you already know, Ruby is dynamically typed. Javascript falls in the same category as well.

Strong Vs Weak
-----------------------------------
```Question```: Why Ruby is a strongly typed language?
```Answer```: Because once it knows the type of an object, it expects you to do something that makes sense with it.
In ruby, you CAN do :
```ruby
x = "3"
y = x + "ho!" #result : "3ho!"
```
but you CANNOT do :
```ruby
x = "3"
y = x + 3 #Wooo! Ruby won't like that
```

Check deference between Ruby 2 and Ruby 3
https://scoutapm.com/blog/ruby-3-features

Variables
-----------------------------------
One of the most basic concepts in computer programming is the variable. You can think of a variable as a word or name that grasps a single value. For example, let’s say you needed the number 30, but you’re not going to use it right away. You can set a variable, say my_number, to grasp the value 30 and hang onto it for later use, like this:
my_number = 30

Declaring variables in Ruby is easy: you just write out a name like my_number, use = to assign it a value, and you’re done! If you need to change a variable, no sweat: just type it again and hit ```=``` to assign it a new value.

```Quize ( TODO )```

Data Types: Numbers, Strings, Booleans, Symbols,  Hashes & Arrays
=====================
Numeric 
-----------------------------------
Integers and floating point numbers come in the category of numbers.
Integers are held internally in binary form. Integer numbers are numbers without a fraction. According to their size, there are two types of integers. One is Bignum and other is Fixnum.

In a calculation if integers are used, then only integers will be returned back.
```ruby
1 + 5 # => 6
```
In a calculation if float type is used, then only float will be returned back.
```ruby
2 + 4.0 # => 6.0
```
In case of dvision, following output will appear.
```ruby
11.0 / 2 # => 5.5
11 / 2 # => 5
```

You can familiarize yourself with the methods of the Numeric class in the documentation
https://ruby-doc.org/core-3.0.2/Numeric.html

Boolean 
-----------------------------------
Can be true or false. Ruby uses the == operator for comparing two objects.
```ruby
name = “Ruby”
name == "Ruby" # => true
```
The other usual operators like greater than ```>```, less than ```<```, greater than or equal to ```>=``` etc. are supported.
```ruby
35 > 25 # => true
25 > 56 # => false
```
Boolean expressions like the above always return either the true or false objects.

Combining Expressions using the ```&&``` and ```||``` operators

You can use the keywords ```||``` (read as 'or'), ```&&``` (read as 'and') to combine expressions. 
```ruby
age = 25
name = ‘Ruby’
age >= 25 && name == ‘Ruby’ # => true
age == 25 && name == ‘Java’ # => false
age == 33 || name == ‘Ruby’ # => true (because one of our check return true )
```
### Negating expressions
Ruby lets you negate expressions using the ```!``` operator (read as 'not'). For instance, ```! (name == ‘Ruby’)``` will return false if the name is Ruby and true for any other name.

You can familiarize yourself with the methods of the TrueClass/FalseClass  in the documentation
https://ruby-doc.org/core-2.5.1/TrueClass.html
https://ruby-doc.org/core-2.6.5/FalseClass.html

String 
-----------------------------------
Words or phrases like "I like Ruby Lab!". 
A string is a group of letters that represent a sentence or a word. Strings are defined by enclosing a text within single ```'``` or double ```"``` quote.
```ruby
'Ruby' + 'Lab' # => "RybuLab"
"Ruby" + "Lab" # => "RybuLab"
```
The single quoted and double quoted approaches have some differences, which we will look into later. For most purposes they are equivalent.
All Strings are instances of the Ruby String class which provides a number of methods to manipulate the string. Now that you have successfully mastered creating strings let's take a look at some of the most commonly used methods.

### String Interpolation
It is essential to be able to replace placeholders within a string with values they represent. In the programming paradigm, this is called "string interpolation". In Ruby, string interpolation is extremely easy.
```ruby
a = 1
b = 4
puts "The number #{a} is less than #{b}" # => "The number 1 is less than 2"
```
Do remember that placeholders aren't just variables. Any valid block of Ruby code you place inside ```#{}``` will be evaluated and inserted at that location
We've been using double quotes in all our string interpolation examples. A String literal created with single quotes does not support interpolation.
```ruby
num = 5
"String with double quotes where number = #{num}. \n" # => "String with double quotes where number = 5"
# (new line = \n)
```
The essential difference between using single or double quotes is that double quotes allow for escape sequences while single quotes do not. What you saw above is one such example. ```"\n"``` is interpreted as a new line and appears as a new line when rendered to the user, whereas ```'\n'``` displays the actual escape sequence to the user.

### String case change
Ruby provides us with a convenient tool-set to take care of proper and consistent casing within strings. Let's start with converting a string in lower case to upper case.
```ruby
puts 'i am in lowercase'.upcase # => 'I AM IN LOWERCASE'
```
### Splitting Strings
Splitting strings on a particular word, escape character or white space to get an array of sub-strings, is an oft-used technique. The method the Ruby String API provides for this is ```String#split```. Let us begin by splitting the string below on space ```' '``` to get a collection of words in the string.
```ruby
'Fear is the path to the dark side'.split(' ') # =>	["Fear", "is", "the", "path", "to", "the", "dark", "side"]
```
### Concatenating Strings
You can create a new string by adding two strings together in Ruby, just like most other languages.
```ruby
'Ruby' + 'Lab' => ‘RubyLab’
```
OR
Ruby often provides more than one way to do the same thing. The literal and expressive method for String concatenation is String#concat.
```ruby
"Ruby".concat("Lab") # =>‘RubyLab’
```
### Replacing a substring
The Ruby String API provides strong support for searching and replacing within strings. We can search for sub-strings or use Regex. Let us first try our hands at something simple. This is how we would replace ```I``` with ```We``` in a given string:
```ruby
"I should look into your problem when I get time".sub('I','We') # => ‘We should look into your problem when I get time’
```
You can familiarize yourself with the methods of the Sting class in the documentation
https://ruby-doc.org/core-3.0.2/String.html

Symbols  
-----------------------------------
Symbols are like strings. A symbol is preceded by a colon ```:```.
For example:
```ruby
:g
```
They do not contain spaces. Symbols containing multiple words are written with (_). One difference between string and symbol is that, if text is a data then it is a string but if it is a code it is a symbol.
Symbols are unique identifiers and represent static values, while string represent values that change.
```ruby
'string'.object_id # => 534
'string'.object_id # => 875
:symbol.object_id # => 123
:symbol.object_id # => 123
```
In the above example, two different object_id is created for string but for symbol same object_id is created.

Arrays 
-----------------------------------
Arrays are ordered, integer-indexed collections of any object
Array indexing starts at 0, as in C or Java. A negative index is assumed to be relative to the end of the array - that is, an index of -1 indicates the last element of the array, -2 is the next to last element in the array, and so on.

An array stroes data or list of data. It can contain all types of data. Data in an array are separated by comma in between them and are enclosed by square bracket. For example,
A new array can be created by using the literal constructor ```[]```. Arrays can contain different types of objects. For example, the array below contains an Integer,  a String and a Float:
```ruby
array = [1, "two", 3.0] # => [1, "two", 3.0]
```
### Growing arrays
In Ruby, the size of an array is not fixed. Also, any object of any type can be added to an array, not just numbers. How about appending the String "woot" to an array? Try using <<
``` ruby
array = [1, "two", 3.0] 
array << ‘tre’
# array = [1, "two", 3.0, 'tre']
```
Unlike many other languages, you will always find multiple ways to perform the same action in Ruby. To append a new element to a given array, you can also use push method on an array.
``` ruby
array = [1, "two", 3.0] 
array.push('new')
```

### Transforming arrays
Now on to more interesting things, but with a little tip from me first. Try running this:
```ruby
[1, 2, 3, 4, 5].map { |i| i + 1 } # =>	[2, 3, 4, 5, 6]
```
You'll notice that the output, [2, 3, 4, 5, 6] is the result of applying the code inside the curly brace to every single element in the array. The result is an entirely new array containing the results. In Ruby, the method map is used to transform the contents of an array according to a specified set of rules defined inside the code block.

### Filtering elements of an Array
Filtering elements in a collection according to a boolean expression is a very common operation in day-to-day programming. Ruby provides the rather handy select method to make this easy.
```ruby
# select even numbers
[1,2,3,4,5,6].select {|number| number % 2 == 0} # =>	[2, 4, 6]
```
The method select is the standard Ruby idiom for filtering elements

You can familiarize yourself with the methods of the Sting class in the documentation
https://ruby-doc.org/core-3.0.2/Array.html

Hashes 
-----------------------------------
A hash assign its values to its keys
They can be looked up by their keys. Value to a key is assigned by ```=>``` sign. A key/value pair is separated with a comma between them and all the pairs are enclosed within curly braces.
### Creating a Hash
```ruby
{"Ben" => "JS developer", "Boris" => "Ruby developer", "Olga" => "Project Manager"}
# => {"Ben" => "JS developer", "Boris" => "Ruby developer", "Olga" => "Project Manager"}
```
### Fetch values from a Hash
```ruby
data = {"Ben" => "JS developer", "Boris" => "Ruby developer", "Olga" => "Project Manager"}
puts data["Ben"] # => "JS developer"
puts data["Boris"] # => "Ruby developer"
```
### Modifying a Hash
```ruby
data['Ben'] = 'React developer'
puts data['Ben'] # => 'React developer'
```
### Iterating over a Hash
You can use the each method to iterate over all the elements in a Hash. However unlike Array#each, when you iterate over a Hash using each, it passes two values to the block: the key and the value of each element.
Let us see how we can use the each method to display the restaurant menu.
```ruby
restaurant_menu = { "Ramen" => 3, "Dal Makhani" => 4, "Coffee" => 2 }
restaurant_menu.each do | item, price |
  puts "#{item}: $#{price}"
end
# =>	Ramen: $3
# => Dal Makhani: $4
# => Coffee: $2
```
The restaurant is doing well, but it is forced to raise prices due to increasing costs. Use the each method to increase the price of all the items in the restaurant_menu by 10%.

### Extracting the keys and values from a Hash
Every Hash object has two methods: keys and values. The keys method returns an array of all the keys in the Hash. Similarly values returns an array of just the values.

You can familiarize yourself with the methods of the Sting class in the documentation
https://ruby-doc.org/core-3.0.2/Hash.html


Computer programs exist to quickly analyze and manipulate data. For that reason, it’s important for us to understand the different data types that we can use in our programs.

Loops and Iterators in Ruby
=====================
Iterators are methods that naturally loop over a given set of data and allow you to operate on each element in the collection.
We said earlier that arrays are ordered lists. Let's say that you had an array of names and you wanted to print them to the screen. How could you do that? You could use the each method for arrays, like this:
```ruby
names = ['Bob', 'Joe', 'Steve', 'Janice', 'Susan', 'Helen']
names.each { |name| puts name }
```
Isn't that concise! We've got a lot of explaining to do with this one.
We have called the each method using the dot operator ```.``` on our array. What this method does is loop through each element in our array, in order, starting from 'Bob'. Then it begins executing the code within the block. The block's starting and ending points are defined by the curly braces ```{}```. Each time we iterate over the array, we need to assign the value of the element to a variable. In this example we have named the variable name and placed it in between two pipes |. After that, we write the logic that we want to use to operate on the variable, which represents the current array element. In this case it is simply printing to the screen using puts.
Run this program to see the output.
A block is just some lines of code ready to be executed. When working with blocks there are two styles you need to be aware of. By convention, we use the curly braces ```{}``` when everything can be contained in one line. We use the words do and endwhen we are performing multi-line operations. Let's add some functionality to our previous program to try out this do/end stuff.
```ruby
names = ['Bob', 'Joe', 'Steve', 'Janice', 'Susan', 'Helen']
x = 1

names.each do |name|
  puts "#{x}. #{name}"
  x += 1
end
#  => ["Bob", "Joe", "Steve", "Janice", "Susan", "Helen"]
```
We've added the counter x to add a number before each name, creating a numbered list output. The number x is incremented every time we go through the iteration.
Memorizing these small differences in syntax is one of the necessary tasks a Ruby programmer must go through. Ruby is a very expressive language. Part of what makes that possible is the ability to do things in more than one way.
There are many other iterator methods in Ruby, and over time, you'll get to use a lot of them. For now, know that most Rubyists prefer to use iterators, like the each method, to loop over a collection of elements.

### Loops are programming constructs that help you repeat an action an arbitrary number of times.
In Ruby, for loops are used to loop over a collection of elements. Unlike a while loop where if we're not careful we can cause an infinite loop, for loops have a definite end since it's looping over a finite number of elements. It begins with the for reserved word, followed by a variable, then the in reserved word, and then a collection of elements. We'll show this using an array and a range. A range is a special type in Ruby that captures a range of elements. For example 1..3 is a range that captures the integers 1, 2, and 3.
```ruby
x = gets.chomp.to_i #  for example x = 6
for i in 1..x do
  puts x – i
end
puts "Done!"
# => 1..6

# gets.chomp.to_i - prompt to enter a number from the keyboard into the console by the user
```
The odd thing about the for loop is that the loop returns the collection of elements after it executes, whereas the earlier while loop examples return nil. Let's look at another example using an array instead of a range.
```ruby
x = [1, 2, 3, 4, 5]
for i in x.reverse do
  puts i
end
puts "Done!"
# => 1..5
```
In this case, we had to reverse the array to ensure a proper countdown. Otherwise, the loop would have counted up.

You can see there are a lot of ways to loop through a collection of elements using Ruby. Let's talk about some more interesting ways you can use conditions to modify the behavior of your loops. Most Rubyists forsake for loops and prefer using iterators instead. We'll cover iterators later.
As with the while and until loops, for is not implemented as a method. Therefore, a for loop does not have its own scope -- the entire body of the loop is in the same scope as the code that contains the for loop.

You can read about other loops and iterators here
https://launchschool.com/books/ruby/read/loops_iterators

Ruby Conditional Branching : the 'if' statement
=====================
You can use Ruby's Boolean Expressions to specifiy conditions using the usual if..else construct. Let us take a look at a simple example:
```ruby
number = 0
if number > 0
    "#{number} is positive"
else
    "#{number} is negative"
end
```
When you run the above example, it will tell you that 0 is negative. But we know that zero is neither positive nor negative. How do we fix this program so that zero is treated separately?
Ruby gives you the elsif keyword that helps you check for multiple possibilities inside an ```if..else``` construct.
```ruby
if number > 0
    "#{number} is positive"
elsif == 0
  "#{number} is ZERO"
else
  "#{number} is negative"
end
```
Ruby also has an unless keyword that can be used in places where you want to check for a negative condition. unless x is equivalent to if !x. Here is an example:
```ruby
age = 10
unless age >= 18
  puts ‘Sorry, you need to be at least eighteen to drive a car. Grow up fast!
end
```
### The ternary operator
In english, "ternary" is an adjective meaning "composed of three items." In a programming language, a ternary operator is simply short-hand for an if-then-else construct.

In Ruby, ```?``` and ```:``` can be used to mean "then" and "else" respectively. Here's the first example on this page re-written using a ternary operator.
```ruby
number = 30
number > 0 ? "#{number} is positive" : "#{number} is negative" # => 30 is positive
```
### Truthiness of objects in Ruby
The conditional statements if and unless can also use expressions that return an object that is not either true or false.

In such cases, the objects false and nil equates to false. Every other object like say 1, 0, ""are all evaluated to be true. Here is a demonstration:
```ruby
if 0
  puts "Hey, 0 is considered to be a truth in Ruby" 
end
# => Hey, 0 is considered to be a truth in Ruby
```
</details>

----------

**Ruby ecosystem**

Gems, how to find, how to install
Live coding: Make a log parser and detect errors in the log file

----------

**Ruby Files, Formats, Templates**

TBD with Boris Tsarikov

----------


**OOP I**

What is class, what is method, Why we need OOP?
Basic OOP examples

----------

**OOP II**

Live coding: Log parser in the OOP way

----------


**End of Phase 1 HW1, HW2**

----------

**OOP Most common design patterns, SOLID, DRY**

----------


[**Testing in Ruby I**](https://github.com/RUBYLNIK-training-center/materials/blob/main/lectures/testing_ruby.md)

Why we need tests?
RSpec basics

----------

**Testing in Ruby II**

More advanced techniques
Mocks, stubs
Tests as a documentation

----------

**Databases**

SQL basics

----------


**End of Phase 2 HW3, HW4**

----------

**Rails basics**

Rails framework overview, scaffolding

----------


**Rails routing**

----------


**Rails controllers**

----------


**Frontend overview**

----------


**Rails models**

----------


**Rails testing**

----------


**Delayed jobs**

----------



**End of Phase 3 HW5, Self-passed HWs**

----------

**Ideas presentation**

----------

**Rails best practices**

----------

**Voting for projects**

