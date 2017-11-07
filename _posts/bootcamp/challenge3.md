---
layout: normal
title: Bootcamp | Codebrahma
permalink: /bootcamp/challenge/3/
---

__Time:__ 27th Dec 2pm to 29th Dec 10am

##LocalTodo

Check out the sample todo app here
[http://localtodos.com/](http://localtodos.com/)

Go through the specifications below and implement all the features mentioned. Make sure you don't leave out anything. Please Use Twitter Bootstrap for UI. Go through the docs carefully.

##Application Specification

We have created this short spec to help you create awesome and consistent todo apps. Make sure to not only read it, but also understand.

###Template Application

Our template should be used as the base when implementing a todo app. Before implementing, we recommend you interact with some of the other apps to see how they're built and how they behave. If something is unclear or could be improved, let us know.

###Directory Structure

Recommended file structure:

{% highlight bash %}
index.html
bower.json
bower_components/
css
└── app.css
js/
├── app.js
├── controllers/
└── models/
readme.md
{% endhighlight %}

Try to follow this structure as close a possible while still keeping to the best practices.
Components should be split up into separate files and placed into folders where it makes the most sense.

Example:

{% highlight bash %}
js/
├── app.js
├── controllers/
│   └── todos.js
└── models/
    └── todo.js
{% endhighlight %}

Keep in mind that best practices on how to structure your app comes first.


###README

All examples should include a README describing the application, the general implementation and the build process if required.

###Dependency Management

Unless it conflicts with the project's best practices, your example should use bower for package management. Specify your dependencies in a bower.json file in the root directory of your app. The name of the component must follow the schema todomvc-local and must include todomvc-common as dependency. An example bower.json could look like this:

{% highlight json %}
{
  "name": "todomvc-sample",
  "version": "0.0.0",
  "dependencies": {
    "underscore": "~1.5.0",
    "jquery": "~2.0.0",
    "todomvc-common": "~0.1.0"
  }
}
{% endhighlight %}

The files in `bower_components/` should be limited to the files actually used by your example.

###Code

Please try to keep the HTML as close to the template as possible. Remove the comments from the HTML when done. The `base.css` file should be referenced from the assets folder and not be touched. If you need to change some styles, use the `app.css` file, but try to keep it to a minimum. Remember to update the relative paths when using the template.

Make sure to follow these:

* Follow our code style
* Use double-quotes in HTML and single-quotes in JS and CSS.
* Use bower components for your third-party dependencies and manually remove files that aren't required for your app to run.
* Use a constant instead of the keyCode directly: `var ENTER_KEY = 13`;
* Apps should be written without any preprocessors (`Sass/CoffeeScript/..`) to reach the largest audience.
* The app should look and behave exactly like the template and the example.
* We require apps to work in every browser we support.

Functionality
------------------
1)
No todos - When there are no todos, #main and #footer should be hidden.

2)
New todo - New todos are entered in the input at the top of the app. Pressing Enter creates the todo, appends it to the todo list and clears the input. Make sure to .trim() the input and then check that it's not empty before creating a new todo.

3)
Mark all as complete - This checkbox toggles all the todos to the same state as itself. Make sure to clear the checked state after the the "Clear completed" button is clicked. The "Mark all as complete" checkbox should also be updated when single todo items are checked/unchecked. Eg. When all the todos are checked it should also get checked.

4)
Item

A todo item has three possible interactions:

* Clicking the checkbox marks the todo as complete by updating it's completed value and toggling the class completed on it's parent <li>
* Double-clicking the <label> activates editing mode, by toggling the .editing class on it's <li>
* Hovering over the todo shows the remove button (.destroy)

5)
Editing

When editing mode is activated it will hide the other controls and bring forward an input that contains the todo title, which should be focused (.focus()). The edit should be saved on both blur and enter, and the editing class should be removed. Make sure to .trim() the input and then check that it's not empty. If it's empty the todo should instead be destroyed. If escape is pressed during the edit, the edit state should be left and any changes be discarded.
Counter

Displays the number of active todos in a pluralized form. Make sure the number is wrapped by a `strong` tag. Also make sure to pluralize the item word correctly: 0 items, 1 item, 2 items.

Example: 2 items left

###Clear completed button

Displays the number of completed todos, and when clicked, removes them. Should be hidden when there are no completed todos.

###Persistence

Your app should dynamically persist the todos to localStorage. If possible, use the keys id, title, completed for each item. Make sure to use this format for the localStorage name: todos-local. Editing mode should not be persisted.


***

PS: Refer the last question from yesterday's test. That's your hint.

{% highlight javascript %}

// models/todo.js
function Todo(){

}

// models/todo_collection.js
function TodoCollection(){

}

TodoCollection.prototype.add = function(todo){
  // Do something and then trigger view changes.
  $(this).trigger("todoAdded", todo)
}

window.collection = new TodoCollection();

// controllers/todo_controller.js

// Define events
var addTodo = function(todo){
  // Dom manipulation logic.
}

// Register events
$(collection).on("todoAdded", addTodo);

// Chrome console.

var t = new Todo("I need to give these guys a test");
collection.add(t);

{% endhighlight %}

* Use Javascript classes to store/manipulate data.
* Have callbacks which trigger view changes when there are changes in the data.
* Think about how/when you can persist this data in localStorage.
