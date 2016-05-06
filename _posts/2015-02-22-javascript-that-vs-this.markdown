---
layout: post
title:  "This != That"
categories: sublime-text
comments: true
description: Better way to preserve context
tags:
  - javascript
  - bind
author: Nithin Krishna
handle: "nithinkrishh"
---

### that != this (TIL)

To preserve context we often assign `this` to `self` or `that`. This works, but this isn't the most elegant way to solve the problem.

`bind` is one of the most unused but most powerful javascript functions.

Consider this.

```javascript
function Store(d){
  this.data = [d];
};

// 'that' approach
Store.prototype.add = function(){
  var self = this;

  $http.get('/new', function(response){
    self.data.push(response)
  });
};

// 'bind' approach
Store.prototype.add = function(){
  $http.get('/new', function(response){
    this.data.push(response)
  }.bind(this));
};
```
