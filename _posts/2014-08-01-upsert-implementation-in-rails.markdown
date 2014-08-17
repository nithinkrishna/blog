---
layout: post
title:  "Implementing Upsert in Rails"
categories: ruby
comments: true
description: Implementing Upsert in Rails
tags: 
  - ruby
  - rails
  - upsert
  - implement
author: Nithin Krishna
handle: "nithinkrishh"
---

An upsert is `update` or `insert`. Upsert in database terms refers to an operation which should insert a row into a database table if it doesn't not already exist, or update it if it does. We can implement an upsert function in Rails by writing an `ActiveRecordExtension`. This will allow you to call the upsert method on any model.

##The ActiveRecordExtension

1.Create a file `active_record_extension.rb` in `app/extensions`.

{% highlight ruby %}
module ActiveRecordExtension
  extend ActiveSupport::Concern

  #All extensions go here.

  def self.upsert(attributes)
    #Upsert implementation goes here.
  end
end

ActiveRecord::Base.send(:include, ActiveRecordExtension)
{% endhighlight %}

2.Set up an initializer `extenstions.rb` in `config/initializers` which initializes your extension.

{% highlight ruby %}
require "active_record_extension"
{% endhighlight %}

---

As I see it there are two ways to implement `upsert`. Lets look at both and run through some numbers.

##1.Playing it safe

{% highlight ruby %}
def upsert(attributes)
  where(:primary_key => attributes['primary_key']).
  first_or_initialize.
  update(attributes)
end
{% endhighlight %}

##2.Rescue from failure
s
{% highlight ruby %}
def upsert(attributes)
  begin
    create(attributes)
  rescue ActiveRecord::RecordNotUnique, PG::UniqueViolation => e
    find_by_primary_key(attributes['primary_key']).
    update(attributes)
  end
end
{% endhighlight %}

So just after looking at the code, you'd notice that the first implementation makes _2 queries_ everytime regardless of whether the record is present or not. The second implementation makes _1 query_ when the record is not present, but _3 queries_ if the record is present.

##Some numbers

Ideally an `INSERT` or `UPDATE` query takes around 100ms. However I'm stubbing the `create`, `update` and `where` methods with `sleep(0.00001)` for benchmarking. _Actual numbers will be 10,000 times higher._

`n = 5000`

{% highlight bash %}
case | user                      | system    | total     | real
------------------------------------------------------------------------------
  1  | new-record-upsert-1       | 1.020000  | 0.050000  | 1.070000 (1.232924)
  2  | new-record-upsert-2       | 0.020000  | 0.020000  | 0.040000 (0.098955)
  3  | existing-record-upsert-1  | 0.890000  | 0.060000  | 0.950000 (1.098148)
  4  | existing-record-upsert-2  | 1.100000  | 0.070000  | 1.170000 (1.384870)
  5  | random-upsert-1           | 1.010000  | 0.150000  | 1.160000 (1.311646)
  6  | random-upsert-2           | 0.560000  | 0.060000  | 0.620000 (0.764272)
{% endhighlight %}

The numbers seem to suggest that __Implementation#2__ is faster. The best case scenario is __37%__ _faster_ while the worst case is only __18%__ _slower_. Even when best/worst case scenarios are randomized __Implementation#2__ wins hands down.

Gist: [upsert.rb](https://gist.github.com/nithinkrishna/549fa9d7213485cad392)
