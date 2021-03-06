---
layout: post
title:  "Ruby rescue vs try vs ternary"
categories: ruby
comments: true
description: Ruby-Benchmark
tags: 
  - ruby
  - rails
author: Nithin Krishna
handle: "nithinkrishh"
---

All of us have faced this situation when, the current-resource object provided by devise turns out to be nil. All method invocations on current-resource will throw an `undefined method for nil:NilClass` exception.

To handle this, we can try one of the following.

{% highlight ruby %}
1. current_resource.name rescue nil
2. current_resource.try(:name)
3. current_resource ? current_resource.name : nil
{% endhighlight %}

But, what is the most efficient way? Let's find out.

{% highlight ruby %}
require 'benchmark'

n = 5000000
current_resource = nil

Benchmark.bm do |x|
  x.report("rescue") { n.times { current_resource.name rescue nil } }
  x.report("try") { n.times { current_resource.try(:name) } }
  x.report("ternary") { n.times { current_resource ? current_resource.name : nil } }
end

{% endhighlight %}


{% highlight bash %}
                user       system        total         real
--------------------------------------------------------------
rescue   | 16.300000   | 0.600000  | 16.900000 | (16.910213)
try      | 0.7800000   | 0.000000  | 0.7800000 | ( 0.783828)
ternary  | 0.2800000   | 0.000000  | 0.2800000 | ( 0.277966)
{% endhighlight %}

Note that __rescue__ is considerably inefficient compared to the other two_(almost 60 times)_. __The Ternary operator__ seems to be the most sound option.