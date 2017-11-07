---
layout: normal
title: Bootcamp | Codebrahma
permalink: /bootcamp/test/1/
---

#ToughRubyTest

* Write the most elegant, well documented, readable, ruby code and remember to use the ruby methods and idioms.
* Please refrain from using the Internet.
* Please don't discuss, or exchange answers or ideas.
* Please place your code in one single ruby file, test.rb and email it to me at [nithin@codebrahma.com](nithin@codebrahma.com). I should just have to be able to require this file, and test all the methods/classes you have created.
* You have 90 minutes. You can start now.

***

1.
Define an instance method on the Array class that will convert the array into a hash. The hash values should be the same as the array values, but the keys of the hash should be defined by a block sent to the method.

{% highlight ruby %}
class Array
  def to_hash_values(&block)
    #IMPL GOES HERE
  end
end

ary = [1,2,3,4,5]
#Keys should be double
result = ary.to_hash_values{|a| a*2}
result[2].eql?(1) #true
result[6].eql?(3) #true
result[10].eql?(5) #true

#Keys should be string of value
result = ary.to_hash_values{|a| a.to_s}
result["1"].eql?(1) #true
result["3"].eql?(3) #true
result["5"].eql?(5) #true
{% endhighlight %}

2.
1+1=3. Ridiculous right? But can you make it happen? Somehow Make ruby say, a+b = a+b+1
{% highlight ruby %}
1+1.eql?(3) # True ? WTF :/
{% endhighlight %}
3.
What does the following code return?  Explain your answer.

{% highlight ruby %}
[1, 2, 3, 4].map() do |number|
  number ** 2
end
{% endhighlight %}

4.
Here is some Ruby code. Describe every component of the code.

{% highlight ruby %}
class CreateCourses < ActiveRecord::Migration
  def change
    create_table :courses do |t|
      t.string :name
      t.float :credits
      t.timestamps
    end
  end
end
{% endhighlight %}

5.
Sheldon Cooper discovered the game Rock,Paper,Sissors, Lizard and Spock. Define a method `sheldon_game` which takes in a hash as agrument.

{% highlight ruby %}
sheldon_game({"nithin"=>:rock,"kamesh"=>:paper})
#The above should return 'Nithin wins'

sheldon_game({"nithin"=>:rock,"kamesh"=>:spock})
#The above should return 'Kamesh wins'
{% endhighlight %}

Rules of the game as quoted by the great Sheldon are "It's very simple. Scissors cuts paper. Paper covers rock. Rock crushes lizard. Lizard poisons Spock. Spock smashes scissors. Scissors decapitates lizard. Lizard eats paper. Paper disproves Spock. Spock vaporizes rock. And as it always has, rock crushes scissors."

6.
Create a `BaseballPlayer` class that is initialized with hits, walks, and at_bats.  Add a `batting_average()` method that returns hits divided by at_bats as a floating point number.  Add an `on_base_percentage()` method that returns (hits + walks) divided by at_bats as a floating point number.  Demonstrate how the `batting_average()` and `on_base_percentage()` methods can be used.

7.
Caching in web browsers is common. Similarly can you cache data in a ruby class? If so how would you do it.

Consider a class `Calculator`. `Calculator` has a method factorial which returns the factorial of a number.

Consider that I find the factorial of 100. It's a really expensive calculation. If I want to find the factorial of 100 again, it doesn't make sense to perform this expensive calculation again.

Optimize this factorial method. Cache the result.

__HINT:__ If I run `Calculator.new.factorial(100)` and then `Calculator.new.factorial(101)` the second one should execute faster.

{% highlight ruby %}
class Calculator
  def factorial(n)
    #Factorial
  end
end
{% endhighlight %}

8.
Create a 10 X 10 array and randomly fill each cell with "D" or "A".

9.
What is the difference between `include` and `extend`? Explain with example.

10.
If everything in ruby is an object. Could we consider methods as objects too? If yes, how?

11.
How is a `Lambda` different from a `Proc`, explain with an example.

12.
How does `attr_accessor` work, can you write your own `attr_accessor` name it `attr_brahma` takes in a attribute names in symbols and defines getters and setters for each of the attributes.

13.
Use YAML to serialize an object and deserialize the same object.

14.
What is modules in ruby? What is the difference between modules and classes? and Why do we have that?

15.
Explain how the following line of code works?

{% highlight ruby %}
array.inject(:+)
{% endhighlight %}

16.
Create a class `CodebrahmaCalculator`. It should have behaviors to perform basic arithmetic operations. Whenever any non-exist method invoked on instance of the `CodebrahmaCalculator` class, it should return your name.

17.
You are given a library called `RubyMonk`. It contains a module Parser which defines a class `CodeParser`. Write another class `TextParser` in the same namespace that parses a string and returns an array of capitalized alphabets.

18.

a) Include a sum method in `Array` Class. The `sum` method should not use any looping constructs.

b) Create a `CodebrahmaArray` class which should extend `Array` class. Override the sum method from `Array` class. This `sum` method should use loops to calculate `sum`.

c) Implement benchmarks to analyze the time taken by both of the `sum` methods and conclude which is better.

__HINT__: `Benchmark.measure`.

19.
Do we have a interfaces in ruby? If no, then how to construct it?

{% highlight ruby %}
module AbstractInterface
  # IMPL GOES HERE
end

class Bicycle
  include AbstractInterface

  needs_implementation :change_gear, :new_value

  def apply_brakes(decrement)
    # do some work here
  end
end

class AcmeBicycle < Bicycle
end

bike = AcmeBicycle.new
bike.change_gear(1) # AbstractInterface::InterfaceNotImplementedError: AcmeBicycle needs to implement 'change_gear' for interface Bicycle!
bike.apply_brakes(10) #Works Fine
{% endhighlight %}

20.
Implement attribute accessors with validation.

{% highlight ruby %}
class Dog
  def self.attr_validated(method_name, &validation)
    # Impl goes here
  end

  attr_validated :num_legs do |v|
    v <= 4
  end
end

dog = Dog.new
dog.num_legs = 3 # Works fine
dog.num_legs = 27 # Raises ArgumentError
{% endhighlight %}

