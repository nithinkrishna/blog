---
layout: post
title:  "Mixins in Javascript"
categories: sublime-text
comments: true
description: Implementing mixins in javascript
tags:
  - javascript
  - angularjs
author: Nithin Krishna
handle: "nithinkrishh"
---

### Javascript Mixins (TIL)

One of the many things I loved about Ruby is the ability to define reusable modules/concerns to define behavior common to multiple classes.

In most of my projects we've tried to encapsulate business logic in the front end through a data layer(A set of Javascript classes which deal with sever interaction and domain logic). Today I was thinking about how to abstract the common functionality out of these classes and expressing it as elegantly as possible.

With a little inspiration from ruby, I came up with this.

```javascript
(function(){
  ResourceWrapper = function(){

    DEFINED_BEHAVIORS = {};

    function RW(r){ this.resource = r; };

    var proto = RW.prototype;

    RW.wrap = function(r){
      return new RW(r);
    };

    RW.defineBehavior = function(behavior, action){
      if(!isValidBehaviorName(behavior)){ throw "Invalid behavior name"; };
      DEFINED_BEHAVIORS[behavior] = action;
    };

    proto.attachBehavior = function(behaviors){
      var self = this,
          bNames = _.keys(DEFINED_BEHAVIORS);

      _.each(behaviors, function(b){
        if(!_.contains(bNames){ throw "This behavior isn't defined"; };
        self.resource[methodNameFrom(b)] = DEFINED_BEHAVIORS[b];
      });
    };

    proto.attachDefaultBehavior = function(){
      this.attachBehavior(DEFINED_BEHAVIORS);
    };

    // Private Methods
    var isValidBehaviorName = function(behavior){
      return (behavior.slice(-4) == "Able");
    };

    var methodNameFrom = function(behavior){
      return behavior.substr(0, behavior.length - 4);
    };

    return RW;

  };
}());

// NOTE: Behavior name ends with "Able"
ResourceWrapper.defineBehavior("logAble", function(){
  console.log(this.name);
});

ResourceWrapper.wrap(Country).attachBehavior(["logAble"]);
ResourceWrapper.wrap(City).attachDefaultBehavior();

var india = new Country({ name: "India" });
india.log(); // Logs 'India'


var chennai = new City({ name: "Chennai" });
chennai.log(); // Logs 'Chennai'

```
