<summary>Information</summary>

Ruby Files, Formats, Templates
=====================
We'll begin learning how to work with files and directories by getting a big picture view of the file system.
And it's going to be helpful if we start by taking a look at the basics of ```input``` and ```output```.

- Input and output make programs interective and dynamic
- I/O = Input / Output
- Output: puts/print
- Input: gets

We've used gets to pause a programs execution and wait for the user to type a line of text on the command line that our program can then use.

Simple example:
```ruby
puts 'What is your name?'
print '> '
name = gets.chomp
puts "Nice to meet you, #{name}!"
```

There are many common input types. Starting with the keyboard which is what we just saw. But we also have files, databases, network, camera, microphone.
Input devices like mouse and trackpad, touchscreens, and of course, there's many more. 
We also have a number of different sources of output, We could have the screen which is what we were using there. Actually, outputting text on the screen so the user can see it. But we could also output data to a file. To a database, across a network, to a printer, or to speakers. And again, that's not an exhaustive list, you could have computer program that controls your Christmas lights.
Or outputs instructions to a 3D printer or controls some kind of machinery. But these are common input and output types.

In fact, there's a Ruby class that's dedicated to input and output. It's call IO. No slash in between it, just capital I, capital O. And the IO class is the basis for all input and output in Ruby. 
It says it right there at the beginning. So all types of input and output are going to be based on this IO class. 
So, IO forms the basis of working with files. So the File class is going to inherit behaviors from the IO class. We're going to be working with the File class in upcoming chapters. 
And you'll see how it's based on this IO class. And IO methods like puts, print, and gets will be useful when working with files too.

File system basics
-----------------------------------

We can also use Ruby to navigate the file system as well to find files and directories, to create or delete them, and to read and write to our files. To do that, we're going to need to tell Ruby how to find the file or directory by using the path as a string. So for example, we could have a file called examplefile.txt, which is inside a directory called Ruby_project, which is inside a directory called documents
/Documents/ruby_project/examplefile.txt

 However, Ruby gives us an even better way to handle it. The file class has a class method called join. Join takes a series of strings and joins them together with the appropriate file separator for the system that Ruby is currently working with.
```ruby
File.join('shared', 'lib', 'myfile.rb')
# shared/lib/myfile.rb
```
We don't even have to think about it, Ruby will take care of it for us. The file doesn't even have to exist. Join is literally just joining those strings together with the right separator. The file doesn't even have to exist and Ruby doesn't check. After all, we might be defining a file path for a new file that we haven't even created yet.

Types of file paths
-----------------------------------
- Absolute path: ```/path/to/file```
That is the path to a file or directory starting from the root of the hard drive. We can recognize an absolute path because it begins with a file separator.
- Relative path: ```./../../path/to/file```
Paths to files can also be described using something called a relative path. A relative path gives the location relative to the current location. We can recognize a relative path because it does not begin with a file separator. I
```ruby
File.dirname(__FILE__)
```
This returns an absolute path to get to the file. If we aren't as interested in the current file as we are in locating other nearby files then it may be more useful to have the directory name of the current file as a starting point in our navigation. We can use dirname as a way to get that directory name. And of course, if we want the absolute path to that directory name, you can use both expand_path and dirname together
```ruby
File.expand_path(File.dirname(__FILE__))
```

Work with Files
-----------------------------------
In this chapter, we are going to learn to work with files in Ruby. And we're going to start by learning how to access those files. We can access files in Ruby two different ways. The first is by using File.new, and the second is using File.open.
```ruby
File.new
File.open
```
And there are some differences that we need to understand. File.new, as you might expect, creates a new instance of the File class, just like when we're creating any new instance from a class. We provide two arguments to it, the first is the path to the file, that can be an absolute path or a relative path. And then the second is the file mode
```ruby
file = File.new('filename', 'w')
```
You can see here I've got a simple string with a w that puts it in write mode. So this is going to allow us to write to the file. You'll notice that I'm taking that instance and assigning it to the variable file. Then I can use that variable and work with the file. I can write to it, I can read to it, I can query it and ask questions about it, and at the end, I want to close the file. The file is open and allows me to work with it, I'm in the process of accessing it, at the end, I want to close it up. You don't strictly have to close your files, but it is a best practice and I encourage you to try and always remember to do it.
```ruby
file.close
```
Now, an alternative method would be to use open. Open is similar to new in that it takes two arguments, a path to the file, which can be either an absolute path or a relative path, and it takes the file mode. Again, here I'm using w for write mode. But notice that instead of taking a new instance and assigning it to an instance variable. Instead, now I've got a block of code after it, everything from do down to end, and you'll see that there is a block variable file that I'm able to then work with inside that block. I don't have to call close on it, because when it gets into the block, it'll automatically close the file for me.
```ruby
File.open('filename', 'w') do |file|
# work with file
end
```
Files Access Modes
- 'r' - Read (form start)
- 'w' - Truncate/write (from start)
- 'a' - Append/write (from end)

Write to Files
-----------------------------------
in Ruby, the process is pretty intuitive. The first thing we want to do is we want to access the file. I'm going to do that using the new method, but you could also do it using open. It works the exact same way. Once I have a file object that I can work with, then I can call methods on that object. You'll remember that for output with the command line we had available to us two methods, puts and print and we have those available here too. But instead of just calling them on their own, we're going to call them as methods on that file. So file.puts with whatever string we want to put in the file, and file.print with whatever string we want to print in the file. And you'll remember on the command line, the difference between puts and print, puts automatically adds a line return at the end. Print does not. If I want to have a line return then I need to use double quotes and use that backslash n as a line return. So here you can see I've got a line return on both of these items but the second one I have to explicitly write it out because I'm using print. 
And write works exactly the same way that print does. There's no difference.
```ruby
file = File.new('filename', 'w')
file.puts "Hi Ruby"
file.print " + Lab\n"
file.write "!!!!\n"
```
And then there's a fourth way that we can write to the file which is a little bit different. Instead of calling a method on on the file object, we can actually use the append operator to append something to that file object. So in this case file and then the less than less than sign appending a string on. It also doesn't add a line return. What's different about append is that it always adds that content to the end of of the file. That's not necessary true with puts, print, and write.
```ruby
file << "Let's learn smth new\n"
file.close
```
Append on the other hand ignores the current position of the cursor and just adds content to the end of the file no matter what. Once we're done writing a file, of course if we're using the new method to open it we want to close it at the end as well.

Read from Files
-----------------------------------
The first and the simplest is just to use the read method. So again, we access our file, notice that I'm using an r, that puts it in read only mode. So I can read back from the file, but I can't write to it. I have that file instance stored in the variable file. And I'm calling the read method on that file instance. Read takes an argument, which is the number of characters that we want to read back. So read four, will grab the first four characters out of that file. And then, I can read again. Now if I call read a second time, it doesn't go back and read the same first four characters, it continues reading from where it left off. Ruby's going to keep track of its position. It's a lot like having a cursor in a word processing program. That cursor's going to move forward four spaces, and then be waiting there for when we read or write again
```ruby
file = File.new('filename', 'r')
str1 = file.read(4)
str2 = file.read(4)
file.close
```
There might be a reason you need to do that. But more common, you want to read whole lines from a file at the same time. And to do that, we can use another familiar method to us, which is gets. So we open up our file, and then we call gets, the same way that we call puts and print when we wanted to output to the file, we're using gets to read data back from the file. When we use gets previously, we used it with the command line, we were looking for user input. We were asking the user to give us a line of input, and it would take that line, plus the ending line return, and bring it back into Ruby so we can work with it. And we learn that we can use chomp on the end if we don't want that trailing line return, it'll lop it off for us. So it works the same were here, gets goes and gets the line from the file, and then, if we want to get rid of that trailing line return, we can use chomp. 
```ruby
file = File.new('filename', 'r')
# File contains four lines
line1 = file.gets.chomp
line2 = file.gets.chomp
line3 = file.gets.chomp
line4 = file.gets.chomp
file.close
```
Now one thing we've got to be careful about, is when we get to the end of the file. That's often abbreviated as eof. End of file. If we get to the end of the file, we can run into some problems

So here I have a while loop, and it says line equals file.gets, right. It's not comparing, it's not checking to see if like is equal to file.gets, it's doing an assignment, it's saying do file.gets, assign that to line, and while that has a value, keep doing whatever's inside this loop. If it returns nil, then the loop will exit. So that's one approach. But if we know that we want to go through every single line in a file, a much more elegant way to do it is using each_line. This is a method that does that exact same thing. It goes and it gets every single line in the file, and it exits gracefully when it gets to the end of the file
```ruby
File.open('filename', 'r') do |file|
  while line = file.gets
    puts file.chomp.reverse
  end
end
```
-----
```ruby
File.open('filename', 'r') do |file|
  file.each_line do |line|
    puts line.chomp.reverse
  end
end
```

File pointer
-----------------------------------
- Similar to the cursor in a word-processing application
- Move pointer forward and backward
- Choose a position to start reading or writing
- Important difference: pointer overwrites text
- The gets and read methods moved the pointer
```ruby
file.pos
# => 0
file.read(4)
file.pos
# => 4
file.gets
file.pos
# for example => 14
file.pos += 6
# => 20
file.eof?
```

Read or write an entire file
-----------------------------------
sometimes it's useful to be able to work with an entire file. And if you want to do that, you can use File.read and provide it a filepath. Notice that I'm not providing any access mode because it's presumed that I'm using read-only mode for this and the instance does not need to be closed, like when we're working with New or Open. So, Read will just open the file, read its contents in, and then close it automatically for me. 
- File.read(filepath)
- File access mode is omitted
- File instance does not need to be closed
- Only use with small data files
- Holds all file data im memory

Another option, is readlines. Readlines works exactly the same way as file.read, but it returns an array. It takes Read but, as it's reading in the lines, every time it sees a line return, it breaks it into a new element in the array. It does not remove the ending line returns, though. They stay there, they're in the end of the line.
- File.readline(filepath)
- Same as File.read, but returns an array
- Does not remove ending line returns

 If we have a chunk of data and we just want to write the entire thing to disk without going through it line by line, well, we can just call File.write, with a file path, and give it a string. And that entire string will be written to the file path. Now, if we want line returns, of course we have to include those in our string, but it's just going to drop all that data in. Notice again, it doesn't have a file access mode, it assumes that it's going to be right. And like the right access mode, it's going to truncate any existing file by default. So, if that file already exists, it will override it destructively. You can provide an optional argument for position if you want to prevent it from truncating.
 - File.write(filepath, string)
 - File access mode is omitted
 - Truncates any existing file by default
 - Provide an optional arguments for position to prevent truncating


Rename, Delete and Copy files
-----------------------------------
```ruby
File.rename('oldfilename.txt', 'newfilename.txt')
File.delete(filename)

require 'fileutils'
FileUtils.copy('orig.txt', 'dube.txt')
```


Common Data Formats
=====================
CSV
-----------------------------------
CSV is an abbreviation for comma-separated values and it's frequently used when we want to export data from databases or spreadsheets and be able to import it somewhere else. It's a good file interchange format. The way that a line in a CSV file would look is that you have a number of values that are separated by commas. Here you can see I've got someone's name, their street address, their city, and their state. That's four values and each one of them is separated by a comma.

- Comma-separated values
- Often used for exporting data from DB and spreadsheets
- "Boris Tsarikov, Traugutta street, Wroclaw"

Ruby has the ability to work with CSV files with part of the Ruby Standard Library. That means the code for CSV files isn't loaded by default, but it's easy for us to ask Ruby to go get that functionality. You just put require CSV in your file. That will tell Ruby to go and get that functionality and make it available. That allows me to use the CSV class. You can see that I'm calling the for reach method on it. I'm providing a file path for the CSV file that I want it to target and what that does is it loads in the file, CSV parses it into rows, and then it makes each row available to me in a block.
```ruby
require 'csv'
CSV.foreach('file.csv') do |row|
  # use row ...
end

array_for_arrays = CSV.read('file.csv')
```
We can also read in an entire CSV file at the same time using the read method. You want to make sure, of course, that you don't have a CSV file that's too large because it's going to read the entire file into memory.
What it will give you is an array of arrays. That is one outside array that's holding all the other arrays and then each row that's in the CSV file will also be an array and each of its values will be an element in that array. 

When we want to write to a CSV file, we just make sure we have that CSV functionality loaded and then we can call CSV.open. It works a lot like file open. You can see I'm giving it a file path and I'm putting it into a write mode, just like we did before, and this will create a new file and allow me to write to it. You can see that I'm appending onto the CSV block variable just like we were doing when we were working with a file. I
```ruby
CSV.open('file.csv', 'w') do |csv|
  csv << ['Row', 'of', 'CSV', 'file']
end
```
The difference here is that the CSV class is going to transform an array of data that we passed into a line in the CSV file. It'll handle that transformation for us and it'll escape any characters it needs to escape in the process. It makes it very easy. 

CSV to hashes
-----------------------------------
In this part, I want to touch on something that frequently comes up when working with CSV files, and that is how to take CSV values and turn them into hashes. The problem is because the header row of a CSV file contains all of the labels, and it's not repeated again for each row after that, it's just contained at the very top. After that, we only have values. But hashes are structured differently, hashes use labels as keys for each value, every time we have another hash, that is, it's repeated in each hash. 

So what we need is a way to efficiently match up the labels with the values in each row. And Ruby gives us a handy way to do that. The first thing I would suggest is to take the header row that you've got, and make it into suitable labels. There's a number of different ways you could do that, here's a simple one that just downcases everything that's in the header item, and replaces all the spaces with underscores. You could also do more substitutions, or you could turn it into a symbol if you wanted, all of those things would give you suitable labels that we could use in a hash. Once you've got that, then you can call map on the data that you want to work with, so it goes through each item in the array, and we can use the zip method on it, to combine the labels and the row. What zip does is it says, take an array and take another array, and merge them together, right, match them up, and it generates another array in the process. So we also want to call to_h to convert it into a hash. That'll then give us back an array of hashes.
```ruby
label = heaser.map {|item| item.downcase.gsub(/\s/, '_')}

new_array = names.map do |row|
  labels.zip(row).to_h
end

{
  "number" => "1"
  "name" => "Boris"
  ...
}
```

YAML
-----------------------------------
- YAML Ain't Markup Language
- More about YAML: http://yaml.org
- Human friendly data serialization standard
- Often used for configurations files
- In Ruby Standard Library: YAML, Psych

```ruby
require 'psych'

yaml = File.read('file.yml')
ruby_data = Psych.load(yaml)
```
 If we want to write yaml, the process is the same. We take the data that we have, the ruby_data, those familiar structures, hashes and arrays, and we passed them into psych dot dump and that'll give us yaml for it. Or an even better easier way is to call two underscore yaml on something. We have the ability to call that on our arrays or hashes and it'll turn it into yaml data for us. It's much easier to remember, once we have that yaml data, then we just use ruby's regular file write, in order to write that to a yaml file. 
 
 ```ruby
require 'psych'

yaml = File.dump(ruby_data)
yaml = {'enabled' => true}.to_yaml

File.write('file.yml', yaml)
```

JSON
-----------------------------------
 In this part we're going to learn about a data format called JSON. JSON is short for JavaScript Object Notation and you can go to json.org to find out more about it. In short, JSON is meant to be a lightweight data interchange format. It's most frequently used for the live exchange of data between two systems, however it's also possible to store JSON into files as well.
 
 - JavaScript Object Notation
 - http://json.org
 - Lightweight data-inerchange format
 - In Ruby Standard Library

```ruby
require 'json'

json = File.read('file.json')
hash = JSON.parse(json)
```
When we want to write to a file we just do the same process in reverse. We can either call JSON generate on our Ruby code in order to get JSON, or much easier is just to call to_json on it and that will give us some json data, and then we can call file write to write that data to a file.
 ```ruby
require 'json'

json = JSON.generate(hash)
json = {'enabled' => true}.to_json

File.write('file.json', json)
```

XML
-----------------------------------
 In this part, we're going to learn about the XML data format. XML is short for extensible markup language, and it's purpose is to make documents both human and machine readable. If you've ever seen XML, it looks similar to HTML in that we have tags that surround all of the content. It essentially gives us a way of marking up a page. 
Now there are built in Ruby XML libraries called REXML, however it's from a long time ago, over 10 years ago, and so most developers don't use it. Instead they use Ruby gems, and there are many Ruby gems that can help you work with XML. The most popular ones tend to be nokogiri, nori, gyoku, multi_xml, and xml-simple. You can look at each one to evaluate which one you like the best. Nokogiri is the most powerful and probably the most popular, but xml-simple has a lot of fans, because it is very simple.

Check nokogiri.org

ERB Templating
=====================
Embed Ruby
-----------------------------------
- ERB
- Embedded Ruby
- eRuby templating system to embed Ruby
- In Ruby Standard Library

The first is that we can use a less than and percent sign together to open an ERB tag. And then we can close that same tag with a percent sign and a greater than, and everything in between would be Ruby code, and that code would be evaluated when the template is evaluated by ERB.
We can also have these same tags to open and close the code but also add an equal sign at the beginning, and that will both evaluate our code and output the result to the template. So they work the same way, both of them will evaluate the Ruby code when it gets there, but the difference is that the first one will not output any result to the template. It'll just evaluate the code. The second will evaluate and do output. 
```ruby
<% code %>

<%= code %>
```
And it's probably the one you're going to use more often. So let's get an example of how this would work. Now we're going to be using this with template files eventually. But we can also use it with just simply strings. A template doesn't have to be a file. It can just be any string that we want to drop information into. So the first thing we want to do is tell Ruby to load up erb so we have access to it from the standard library. Then we define our template. Here you can see I have a string. And the string says the year is, and then inside those erb tags, which do output, we know that because of the equal sign, I have a bit of Ruby code. And it just says Time.now.year. So that'll return the current year. So that's just a string. Don't misunderstand that. That's not actually Ruby code right now. That is a string. What we're going to do is tell ERB that it should take that string and look for any places that look like they could be Ruby code and execute that code. So be clear about that.
```ruby
require 'erb'

template = "The year is <%= Time.now.year %>"
```
At the moment that is just simply a string. When I tell ERB, the class, I call new on it and I pass in that template, that string that we just came up with? It'll return back an ERB renderer object to me. Then when I tell that renderer object to give me the result, then it takes that string. It goes through looking for those ERB tags, and it evaluates the code that's inside of them and outputs it if appropriate. At that point now, we get the string that we would want. The year is and then 2018, 2019, 2020 whatever it might be. So this is a very simple but powerful way for us to execute Ruby code inside a template. Let's try it together in irb.
```ruby
require 'erb'

template = "The year is <%= Time.now.year %>"

renderer = ERB.new(template)
puts renderer.result
```

Binding
-----------------------------------
In this part we're going to learn about a very cool feature with IRB called binding. Binding is based on the idea that every Ruby object stores its instance variables in a Binding object. It's actually a class in Ruby called Binding. We don't need to know much about the class, we just need to know that it's used for the storage of instance variables. And we can access that Binding object with a private instance method called binding
Every Ruby object has one. Where this is really powerful is that it allows us to pass in the binding as an argument to ERB result. So ERB then receives this binding object, which has a collection of instance variables stored inside of it, and that gives our template access to those instance variables so that it can make use of them in the template. Now this only works with instance variables, it doesn't work with local variables and it doesn't work with class variables. And that makes instance variables a little bit special when we're working with templating.
```ruby
require 'erb'

@year = Time.now.year

template ="The year is <%= @year %>"
renderer = ERB.new(template)
puts renderer.result(binding)
```


Template files
-----------------------------------
In this part, I want us to talk about how we can use template files instead. Hopefully, you've realized that the process is very simple. All we need to do is require ERB, set any instance variables we want, and then when it comes time to provide the template, instead of having a simple string, well, we just read from the file. We know how to do that. We've learned how to read from a file and turn it into a string inside Ruby. Then we can take that template, pass into into ERB, give it its bindings, and it'll put it all together and give us the result that we want from this template file.

```ruby
require 'erb'

@year = Time.now.year

template = File.read(filepath)
puts ERB.new(template).result(binding)
```
