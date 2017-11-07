---
layout: normal
title: Bootcamp | Codebrahma
permalink: /bootcamp/lesson/3/
---

#Rails

Rails is the most vibrant happening open source web framework there is. There are innumerable resources out there for you to understand and learn about rails. The best place to start would be Rails Guides. With rails comes a whole bunch of tools, commands, text editor optimizations all of which will help you be on top of your game and ship code efficiently.

Rails is all about plug n play, there are innumerable gems out there. Each gem is always well documented. For those of us who are too lazy to read the documentation, rails casts are a great way for you to understand their usage and functionality just by watching a bunch of videos.

* [Rails Guides](http://guides.rubyonrails.org/)
* [Rails Cheat Sheet](http://www.pragtob.info/rails-beginner-cheatsheet/index.html)
* [Rails casts](http://railscasts.com/)


#FirstRailsApplication

Things to remember.

* Never have more than 4 lines of code in a method.
* Your controllers need to be thin, they should have minimal logic.
* Never interpolate your javascript with rails views. Keep your javascript pure.
* Use [Gon](https://github.com/gazay/gon) to pass data to javascript if necessary.
* Use proper naming conventions.
* Use services and pure ruby classes to handle your business logic.
* Break up your views into manageable partials and layouts.
* __DO NOT REPEAT YOURSELF__. Ensure that you don't write duplicate code.

Ah. I totally forgot. For those of you coming in form the php world. Rails is follows the [MVC](http://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller) framework. Read about how its better than code from scratch with no abstractions. You will eventually understand this as you write more code.


After you application is done. Additional points for deploying it into [heroku](https://www.heroku.com/).

