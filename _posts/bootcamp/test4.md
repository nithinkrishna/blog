---
layout: normal
title: Bootcamp | Codebrahma
permalink: /bootcamp/test/4/
---

#Jquery Test

1)
What is event bubbling? How do we prevent it?
Run the code below. Right now when we click on the inner square the event on the outer square is being fired too We need to fix this issue i.e when we click on the inner square only the inner square event should fire and when we click on the outer square the event on the outer square should fire.

{% highlight html %}
<!doctype html>
<html>
  <head>
      <script src="http://code.jquery.com/jquery-1.10.2.min.js"></script>
      <style>
          body{
              position:relative;
          }
          .parent.box{
              border:1px solid black;
              background-color:rgb(51,51,51);
              height:100px;
              width:100px;
          }
          .child.box{
              border:1px solid red;
              background-color:gray;
              height:50px;
              width:50px;
              margin:auto;
          }
    </style>
  </head>
  <body>
      <div class="parent box">
          <div class="child box"></div>
      </div>
      <script>
          $(".child").click(function(){
            alert("clicked on child");
          });
          $(".parent").click(function(){
            alert("clicked on parent");
          });
      </script>
  </body>
</html>
{% endhighlight %}

2)Why do we need callbacks in javascript? Explain with an example

3)Using the JQuery library implement the following. This the html.

{% highlight html %}
<ul id="p-0">
  <ul id="c-1">
    <li id="gc-1">grandchild one</li>
    <li id="gc-2">grandchild two</li>
  </ul>
  <li id="c-2">child one</li>
  <li id="c-3">child two</li>
</ul>
<div id="message">
  <p id="current-element"></div>
  <p id="parent-element"></p>
  <p id="children"></p>
</div>
{% endhighlight %}

When ever you hover on any "ul" or "li" element the p#current-element tag should display the id of the element you hovered on and p#parent-element should display the id of the parent of that particular element and p#children should display the ids of the child elements(if any).

4)
What is AJAX and why do we use it?

5)
Somewhere on your server resides a file called books.json whose contents are as follows

{% highlight json %}
{
 "head":["Author","Book"],
 "values":[
   {
     "book":"JS The Good parts",
     "author":"Douglas Crockford"
   },
   {
     "book":"JS The Definitive guide",
     "author":"David Flanagan"
   },
   {
     "book":"Professional JS",
     "author":"Nicholas Zakas"
   }
 ]
}
{% endhighlight %}

Using the Jquery ajax function grab the contents of this file from the server and display it in the html page in form of a table.


6)
Write a short note about jquery custom events.
Create a js class called Collection.

* This class should have an instance variable called "arr" which is an array
* An instance method on the prototype object of the class called "add" which takes in a number as a parameter and adds it to the "arr".
* An instance method again on the prototype object called "get" which the returns all the elements of the array.

After you have successfully constructed this class use jquery custom events to create to an event which is fired every-time an element is added to the array using the "add" method. The handler should have access to the newly added value.

Resultant code should work something like this.

{% highlight javascript %}
var l = new List();
//Here i have used a static class method which can be used to bind events
List._bind("add",function(event,val){
  console.log(val)
});
l.add(1);//when an element is added the handler is fired
l.get();
{% endhighlight %}

