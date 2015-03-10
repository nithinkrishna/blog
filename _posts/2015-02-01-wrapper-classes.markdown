---
layout: post
title:  "Wrapper Classes"
categories: sublime-text
comments: true
description: The need for wrapper classes
tags:
  - javascript
  - angularjs
author: Nithin Krishna
handle: "nithinkrishh"
---

###Wrapper Classes (TIL)

Wrapper classes are good. Whenever you are using a 3rd party plugin / API, make sure that you wrap within a container of your own. By standardizing the interface between your code and the 3rd party plugin you are making your a lot easier. Even if you have to change the underlying plugin completely code changes would be limited to the wrapper class, you don't have to touch any other part of the codebase.

These wrapper classes are also a great place to put in logic which is specific to initializing / operating the plugin. Think about it, if you are using a jquery draggable plugin it doesn't make sense to put in code to configure the plugin in your controller.

One other notable advantage of wrapper classes WRT angular is that it forces you to explicitly inject them as a dependency where ever you use them. Trust me, This is a good thing.

In my latest project, [Anand](mailto:anand@codebrahma.com) had used a 3rd party library called dagre to handle graph layouting. I wrapped this plugin my own wrapper class. The client now isn't satisfied with the current library. Even if I have to use a new plugin now, my life is going to be a whole lot easier.

```javascript
angular.module("md.data")
.factory("md.data.Dagre", function(){

  /*
    The page will have have only one instance of dagre.
    This factory returns that dagre instance. It also provides wrapper methods
    to simplify interactions with the dagre api.
  */

  if(!dagre){
    throw "Dagre not defined";
  };

  var instance = new dagre.graphlib.Graph(),
      Dagre,
      INTERFACE_METHODS,
      INTERFACE_ATTRS;

  INTERFACE_METHODS = [
    "setEdge",
    "setNode",
    "removeEdge",
    "removeNode",
    "nodeCount",
  ]

  INTERFACE_ATTRS = [
    "edges",
  ]

  Dagre = function(){ };

  Dagre.getInstance = function(){
    return instance;
  };

  Dagre.initialize = function(){
    instance.setGraph({ directed: true, compound: true, multigraph: true });
    instance.setDefaultEdgeLabel(function() { return {}; });
  };

  Dagre.generateLayout = function(){
    return dagre.layout(instance);
  };

  Dagre.asJSON = function(){
    return dagre.graphlib.json.write(this);
  };

  _.each(INTERFACE_METHODS, function(m){
    Dagre[m] = instance[m].bind(instance);
  });

  _.each(INTERFACE_ATTRS, function(m){
    Dagre[m] = return instance[m];
  });

  return Dagre;
});
```
