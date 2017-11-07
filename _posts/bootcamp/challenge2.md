---
layout: normal
title: Bootcamp | Codebrahma
permalink: /bootcamp/challenge/2/
---

__Time:__ 16th Dec 12pm to 6pm

#FirstGem

Ruby is all about plug and play. [RubyGems](http://en.wikipedia.org/wiki/RubyGems) is a package manager for the Ruby programming language that provides a standard format for distributing Ruby programs and libraries (in a self-contained format called a "gem"), a tool designed to easily manage the installation of gems, and a server for distributing them.

[RubyGem.org](https://rubygems.org/) has over a hundred thousand gems.

This task requires you to build your first [gem](http://www.sitepoint.com/creating-your-first-gem/).

Not just any gem but a [command-line utility](http://robdodson.me/blog/2012/06/14/how-to-write-a-command-line-ruby-gem/).

* Please keep your code structured and modular.
* Use the concepts that you've learnt from the previous material.
* Ensure that there is a manual page for the gem you've created which describes succinctly the Gem's functionality.
* Cover all corner cases.

##Gem Ideas
1.__play-rps__: Command-line Rock, Paper and Scissors game.

{% highlight bash %}
> play-rps rock

The computer played paper.
You have lost. :(
{% endhighlight %}

2.__simple-ls__: A simplified implementation of unix ls.
{% highlight bash %}
> simple-ls <relative_path>

file_1
file_2
folder_3
#Lists all the files in the path
{% endhighlight %}

3.__reverse-search__: A simplified implementation of unix reverse search with regex.
{% highlight bash %}
> reverse-search /ssh/

ssh ubuntu@12.12.12.12
ssh ubuntu@12.12.12.13
#Lists all the commands typed in the active terminal session that match the given regex.
{% endhighlight %}

Standard challenge rules apply. Only one of you can work on an idea.

Additional points if your code is test covered. This is completely optional. Checkout [Rspec](http://rspec.info/).

After installing the gem, I need to be able to type in stuff into my terminal and view results. Once you are done push your code to github and publish your gem to [RubyGems](https://rubygems.org/). Email me the respective links at [nithin@codebrahma.com](mailto:nithin@codebrahma.com).

***

1. [play-rps](https://rubygems.org/gems/rps_gem): [https://github.com/balramkhichar/rps-gem](https://github.com/balramkhichar/rps-gem)
2. [simple-ls](https://rubygems.org/gems/simplels_gem): [https://github.com/gauravsarma1992/simplels_gem](https://github.com/gauravsarma1992/simplels_gem)
3. [reverse-search](https://rubygems.org/gems/reverse_search): [https://github.com/pgAdmin/reverse-search](https://github.com/pgAdmin/reverse-search)
