---
layout: normal
title: Bootcamp | Codebrahma
permalink: /bootcamp/test/2/
---

##Core Javascript Concepts(10 questions - 35 points - 1 hour 15 minutes)

***

###Instructions

* Create an answer sheet and add the jsfiddle link related to the answer. If answer requires an explanation write it and give the js fiddle link with the code example.
* Make your explanations short and talk more with code.
* Time for the exam is 1 hour 15 minutes, I would recommend you to go for the easy one's first.
* After the completion of the test please email the answer sheets to [abhishek@codebrahma.com](mailto:abhishek@codebrahma.com)


1) Explain the concept of private namespaces. What is it’s significance? Give a good example for the same (2)

2) Study the following code sinppet (2)
{% highlight javascript %}
  (function(){
      var i = 127; j = 128;
  }());
  console.log(j); // 128
  console.log(i); // ReferenceError: i is not defined
  // Explain why the value of "i" is undefined.
{% endhighlight %}

3) How does inheritance work? Explain with an example. (3)

4) What is a closure? Explain with an example. (2)

5) Using closures implement a private variable inside a class such that it can only and only be accessed via getter and setter functions (2)

6) Consider the following code (2)
{% highlight javascript %}
  var ob = {
    foo: "Foo",
    bar: function() {
      (function(){
         console.log(this.foo);
      }());
    }
  };
  ob.bar();
  // undefined
{% endhighlight %}

Why isn’t "Foo" being printed? Correct the code so that "Foo" get’s printed.
P.S: Do not remove the anonymous function, console.log() should be called from
within it.

7) Write a function "Maybe" such that it takes in an object as parameter and makes that object forgiving in nature (3)
{% highlight javascript %}
  user = {
    name: "John",
    age: 23,
    address: {
      street: "Some street"
    }
    // we were expecting "education" too but the server did not return it
  };

  user.name //John
  user.address.street //Some street
  user.education.school // Uncaught TypeError: Cannot read property 'street' of undefined

  // using Maybe this should not happen

  var addr = Maybe(user.address), edu = Maybe(user.education);
  user.name // john
  user.age // 23
  addr.street // Some Street
  edu.school // undefined (but no error)
{% endhighlight %}

8) Write a function "extends" which simplifies the JS based inheritance (4)
{% highlight javascript %}
   function Car() {
     this.type = "Car";
   };
   function Ferrari() {
     this.name = "Ferrari";
   };
   Ferrari.extends(Car);
   var f = new Ferrari();
   f.name // Ferrari
   f.type // Car
{% endhighlight %}

9) It’s the year 2150 now and man has found a way to convert himself/herself to any species of their choice and revert back too. Write a class Transformer such that.

* The constructor takes in two Species objects i.e new Transformer(from, to) (1)
* Write a convert function on the transformer class such that it modifies the behaviour of the "from" object and makes it similar to the "to" object. The function should throw an exception in the following cases (4)
    * When the "from" object is not of type human throw "Converting other species is not possible".
    * When the "to" object is of type human throw "Conversion to a human is not possible".

{% highlight javascript %}
  var human = new Human();

  human.whoAmI() // human
  human.makeSound // I am a human

  var dolphin = new Dolphin();

  dolphin.whoAmI() // dolphin
  dolphin.makeSound() // *whistle and click*

  var transformer = new Transformer(human, dolphin);
  transformer.convert();

  human.whoAmI() // dolphin
  human.makeSound() // *whistle and click*

  dolphin.whoAmI() // doplhin
  dolphin.makeSound() // *whistle and click*
{% endhighlight %}

* Write a revert function on the transformer class such that it reverts the converted human back to the original form. It should throw errors in the following cases. (5)
  * If "from" and "to" are not of the same type throw "Type mismatch, reverting not possible".
  * If the "from" object is not an object that went through the conversion process throw "Original form of species cannot be determined, reverting not possible".

{% highlight javascript %}
  // continuing with the same example above
  transformer.revert(); // should not throw any error as it satisfies both the cases

  human.whoAmI() // human
  human.makeSound // I am a human
{% endhighlight %}

P.S. The Dolphin, Human or any other class should extend the base "Species" class. Use your extends function from question 8. While checking for types please use the constructor function to do so.


10) Write a function "PropertyFill" such that it adds dynamic methods based on an array of objects to a class (5)

{% highlight javascript %}
  var arr = Country.query(); // returns an array of countries from the server
  // [{ id: 1, name: "India" }, { id: 2, name: "USA" }, { id: 3, name: "United Kingdom" }]

  PropertyFill.on(Country).using(arr).withProperty("name");
  Country.india() // { id: 1, name: "India" }
  Country.usa() // { id: 2, name: "USA" }
  Country.unitedKingdom() // { id: 3, name: "United Kingdom" }
{% endhighlight %}

Notice the naming convention is camelcase for the method names that have been dynamically added to Country.
