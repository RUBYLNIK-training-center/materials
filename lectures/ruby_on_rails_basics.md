## Ruby on Rails basics

In the scope of this article we will touch on three most essential Rails topics: MVC paradigm, object relational mapping and avtion view. 

### MVC

Is the pattern for the architecture of a software application. It separates an application into the following components:

- models
- views
- controllers

This separation results in user requests being processed as follows:

The browser (on the client) sends a request for a page to the controller on the server.
The controller retrieves the data it needs from the model in order to respond to the request.
The controller gives the retrieved data to the view.
The view is rendered and sent back to the client for the browser to display.

The biggest advantages of this approach are: improved scalability, ease of maintenance, reusability.

---

### ORM

Stands for ```object relational mapping```. It is a technique that lets you query and manipulate data from a database using an object-oriented paradigm.
Rails' ORM is ```Active Record```. system responsible for representing business data and logic. Active Record facilitates the creation and use of business objects
whose data requires persistent storage to a database.

Active Record provides it's own DSL(domain specific language) for making requests to database, for example:
```rb
# return the first user named David
david = User.find_by(name: 'David')
```

### Action View
Action View templates are created for representing data in browser and written using embedded Ruby in tags mingled with HTML to give them access to data.
For each controller there is an associated directory in the ```app/views``` directory which holds the template files that make up the views associated with that
controller. These files are used to display the view that results from each controller action.

Template example:
```rb
<h1>Names of all the people</h1>
<% @people.each do |person| %>
  Name: <%= person.name %><br>
<% end %>
```

### Usefull links:
-----------------------------------

- https://www.youtube.com/watch?v=Cj2VDSugHM8&t (probably the best vidoe on the topic ever)
- https://guides.rubyonrails.org/getting_started.html
