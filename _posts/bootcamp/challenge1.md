---
layout: normal
title: Bootcamp | Codebrahma
permalink: /bootcamp/challenge/1/
---

#MidnightAuthor

__Time:__ 15th 8pm to 16th Dec 9am

_“A good idea is an orphan without effective communication.”_ ― Andrew Hunt, The Pragmatic Programmer: From Journeyman to Master.

Writing is a very important skill for a programmer. Having the ability to express abstract concepts in simple understandable language is key to stand out from the crowd. A step toward this direction is writing your first blog post.

##Topics
1. Compare and contrast inheritance in Ruby and Java.
2. What are some of the cool things you can do with `method_missing`?
3. Ruby and syntactic sugar.

##Rules of the game
No person can write about the same topic. If two or more people write about the same topic, then only the first blog will be considered. Please turn in you posts by 9am tomorrow. Create a `markdown` [Gist](https://gist.github.com) with the blog contents and email the link to me at [nithin@codebrahma.com](mailto:nithin@codebrahma.com).

The best post will go onto the Codebrahma blog.

Happy Authoring!

***

#Inheritance in Ruby and Java
In object-oriented programming (OOP), inheritance is when an object or class is based on another object or class, using the same implementation (inheriting from a class) or specifying implementation to maintain the same behavior (realizing an interface; inheriting behavior). It is a mechanism for code reuse and to allow independent extensions of the original software via public classes and interfaces. The relationships of objects or classes through inheritance give rise to a hierarchy.

Multiple inheritance is the ability of a single class to inherit from multiple classes.

Both ruby and java do not support multiple inheritance.

This is so because the diamond shaped inheritance problem faced in both the cases. For example, if class A is derived from both class B and class C, any call to the superclass methods would be ambiguous because it wouldnt be sure whether to call the version derived from class B or class C. This is the diamond inheritance. That's a major reason why multiple inheritance is shunned in both ruby and java.

However, both languages provide ways to overcome the shortcomings in not being able to inherit methods from multiple sources. Ruby handles the issue in a sophisticated manner using modules and mixins.
Modules in ruby allow classes to use methods defined in them. Thus, a single class can use the methods defined in multiple modules and hence achieve an inheritance like structure in a much simpler and efficient way.

<center><img src="http://gauravsarma.me/images/img1.png" /></center>

{% highlight ruby %}
module A end;
module B end;
module C end;

class X
  include A
  include B
  include C
end
{% endhighlight %}

When a method is called in ruby, Ruby walks up the chain of ancestors until the method is found. So, the objects of the subclass also get the methods defined in the superclass. This is why using modules in place of superclasses has proved to be more efficient.

Java has interfaces which help it to overcome the limitations of no multiple inheritance to an extent. One disadvantages of using interfaces is that the methods are not defined in the interfaces and the classes have to derive abstract classes which defeat the main aim of multiple inheritance.

Java is both compiled and statically typed which enables the compiler to analyze the code and prevent type related mistakes. For example, if a method is expecting minerals and you pass a dog to it, then the compiler will complain the dog is an animal and not mineral. These kinds of problems are not at all faced in ruby because type casting is not an issue at all as the types are not declared. Moreover, there wouldn't be a compiler double checking in ruby.

Another plus point which can be deemed from the usage of modules is that modules can be managed at runtime whereas superclasses are set in stone as the class definitions are written beforehand. Modules are also easier to test and manage because of their low coupling. Finally, in advanced ruby, modules can be used to cast metaprogamming magic spells like singleton methods and class extensions.

This is a major reason why inheritance in ruby is not used popularly and developers prefer to use modules in case of inheriting emergencies. Ruby modules prove to be more manageable than multiple superclasses. In ruby, the chain of ancestors always follow a single path, where each module can appear only once, so diamond shaped inheritance can be avoided.

Replacing methods with Monkeypatches prove that there is no reason why ruby shouldn't get used to managing methods with modules instead of classes.

<img src="http://gauravsarma.me/images/img2.jpg" width="300" />
<img src="http://gauravsarma.me/images/img3.jpg" width="300" />

This is basically why large Ruby projects such as Rails barely use inheritance at all, and rely almost exclusively on modules. One outstanding example of this is ActiveRecord. The entire library basically consists of a single class that is enriched by including a *lot* of modules. Both the base class and the modules can be tested, used and documented in isolation, so even if the resulting interface is huge, it doesn't get in your way nearly as much as a chain of superclasses does. The resulting code is surprisingly decoupled and maintainable.

Inheritance should be used sparingly.


#What is method_missing?

When we send a message to an object, it first method it finds on its method lookup path with the same name as message. If it fails to find any method like this then it will raise NoMethodError exception.

`method_missing` is a known tool in the Ruby meta-programming toolbox. It's a callback method that gets called when an object tries to call a method that is missing. An example of this is dynamic finders in ActiveRecord. Let's say Member has an email attribute, you can do `Member.find_by_email('balram@codebrahma.com')` and the interesting fact is that `Member` and `ActiveRecord::Base` have not defined it.


{% highlight ruby %}
class MyClass
  def do_ten(x)
    10
  end

  def do_something(task, times)
    puts "Did Something"
  end
end

class DemoClass
  def initialize(obj)
    @obj = obj
  end

  def method_missing(method, *arguments, &block)
    puts "Called method #{method}"
    @obj.send(method,*args)
  end
end

#now let's test this

myclass = MyClass.new
wrapped_class = DemoClass.new(myclass)
wrapped_class.do_something("Something", 5)
wrapped_class.do_ten(100)
wrapped_class.respond_to?(:do_something)

# output:
# "Called method do_something"
# "Did Something"
# "Called method do_ten"
# Awesome right?
{% endhighlight %}


#Ruby and syntactic sugar.

Syntactic sugar is nothing but one or more ways/syntax that can be used to perform a similar operation. It gives the developer options so that he can choose and use whichever method he/she find convenient to use.

{% highlight ruby %}
#Example
collect = {1 =>"num"} #1.1

collect = {}          #1.2
collect[1] = "num"
{% endhighlight %}

In the above two groups of statements(s), both create a new collection with name "collect" and the first key-value pair is: `{1 => "num"}`.

In Ruby, there are a lot of syntactic sugars. Using one or the other is just a matter of choice and how better one understand the underlying concept.

{% highlight ruby %}
  class Square
   def initialize()
    @side = 5
   end
   attr_reader :side   # create reader only
   # setter method
   def set_side(s)
    @side = s
   end
  end

  sq = Square.new()
  sq.set_side(5)
  puts sq.side
{% endhighlight %}

Ruby allows us to define methods that end with an equal sign (=). Like,

{% highlight ruby %}
  def side=(s)
    @side = s
  end
{% endhighlight %}

However, we can use either of the following ways:

{% highlight ruby %}
  sq.side=(5) and sq.side = 5
{% endhighlight %}

Note the missing brackets. On execution, the interpreter automatically ignores the blank spaces and reads the method as `side=`.

Other common syntatic sugars are:

{% highlight ruby %}
4 - 2  OR   4.-(2)  OR 4.send(:-, 2) #Arithmetic operations

a1 = Array.new(3, 2) OR a1 = [2, 2, 2] #Array creation

puts var1; OR var1 #Output statements

Array1.map() {|num| num * 3} OR Array1.map() do |num| num * 3 end #Loops

Object.method_name() OR Object.send(:method_name) #Method calls
{% endhighlight %}
