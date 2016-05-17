---
layout: post
title:  "Write a lite API server with NODE-JS"
categories: sublime-text
comments: true
description: A elegant, lite api server with NODE JS and reusable components
tags:
  - express
  - nodejs
author: Nithin Krishna
handle: "nithinkrishh"
---

### Why NODE?

When it comes to getting a simple, lite restful API server up,running and deployed within a couple of hours there are 3 options.

* Rails API
* Python flask
* Express NodeJS

NodeJS is a better alternative topython-flask or rails-api when it comes to writing lite API servers. It's not as heavy as RAILS, it's much more stable when deployed compared to [flask](https://www.google.com/webhp?sourceid=chrome-instant&ion=1&espv=2&ie=UTF-8#q=flask%20deployment%20issues).

[Scaling nodejs](http://cjihrig.com/blog/scaling-node-js-applications/) application across a multi-process/multi-machine framework is pretty straight forward.

NodeJS generic/lite compontents for parameter validation and caching (etc) can be built once and reused across applications.

### Caching

A generic caching layer to store intermediate results accelarates responses.

```javascript
var redis = require("redis"),
    Q     = require('q');

var REDIS = redis.createClient();

function namespacedKey(key){
  return key ? "api-" + key : null;
};

function Cache(){
  this.client = REDIS;
};

Cache.prototype.set = function(key, data, expiry){
  var deferred = Q.defer();
  var self = this;

  self.client.set(key, JSON.stringify(data), function(error, r){
    if(error){
      deferred.reject(error);
    } else {
      deferred.resolve(data);
      if(expiry){
        self.client.expire(key, expiry)
      };
    };
  });

  return deferred.promise;
};

Cache.prototype.get = function(key){
  var deferred = Q.defer();
  var self = this;

  self.client.get(key, function(error, data){

    if(data){
      try{
        deferred.resolve(JSON.parse(data));
      } catch(e){
        deferred.resolve(data);
      }
    } else{
      deferred.reject(error);
    };

  });

  return deferred.promise;
};

Cache.reloader = function(query, key, expiry){
  return function(){
    return query().then(function(queryResult){
      new Cache().set(key, queryResult, expiry);
      return queryResult;
    });
  };
};

Cache.fetch = function(query, key, expiry){
  return new Cache().get(namespacedKey(key)).fail(Cache.reloader(query, namespacedKey(key), expiry));
};

// Example
Country.fetchAll = function(){
  function DBQuery(){
    return QueryBuilder("select * from countries", ["ID", "NAME"]);
  };
  return Cache.fetch(DBQuery, "country-list", 24 * 3600);
};

// Fetches from DB the first time, later requests are rendered from cache until expiry
Country.fetchAll();
```


### Parameter Validation
A generic parameter validation layer to validate request parameters.

```javascript
var util      = require( "util" );
var _         = require('underscore');
var Q         = require('q');

function Validator(request){
  this.request = request;
};

Validator.prototype.validationMessage = function(key, type, params){
  var self = this;
  switch(type){
    case "presence":
      return util.format("Required field [%s] is not present", key);
    case "includes":
      return util.format("Value [%s] is not within acceptable list [%s]", self.request[key], params);
    case "within":
      return util.format("Value [%s] is not within acceptable limits [%s,%s]", self.request[key], params[0], params[1]);
  }
};

Validator.prototype.$vFn = function(key, type, params, validator){
  var deferred = Q.defer(),
      self = this;

  if(self[validator](key, type, params)){
    deferred.resolve({ });
  } else {
    deferred.reject({ message: self.validationMessage(key, type, params) });
  };

  return deferred.promise;
};

Validator.prototype.validatePresence = function(key, type, params){
  var self = this;
  return self.request[key]
};

Validator.prototype.validateIncludes = function(key, type, params){
  var self = this;
  return !self.request[key] || _.contains(params, self.request[key]);
};

Validator.prototype.validateWithin = function(key, type, params){
  var self = this;
  return !self.request[key] ||  ( params[0] <= parseFloat(self.request[key]) && parseFloat(self.request[key]) <= params[1] );
};


Validator.prototype.validate = function(key, type, params){
  var self = this,
      validator = "validate" + type.charAt(0).toUpperCase() + type.slice(1);

  return self.$vFn(key, type, params, validator);
};

Validator.prototype.validateAll = function(args){
  var self = this;
  var validations = _.map(args, function(v){ return self.validate(v[0], v[1], v[2]) });
  var deferred = Q.defer();
  Q.allSettled(validations).then(function(r){
    var rejected = _.filter(r, function(p){ return p.state == "rejected" });
    if(rejected.length == 0){
      deferred.resolve( _.pluck(r, "value") );
    } else {
      deferred.reject(  _.pluck(rejected, "reason") );
    };
  });
  return deferred.promise;
};

// Example
// Basic validations for request paramters
validator.validateAll([
  [ "latitude"  ,  "presence" ],
  [ "longitude" ,  "presence" ],
  [ "interval"  ,  "includes",  [ "15", "30", "45", "60" ] ],
  [ "from_time" ,  "within",    [0, 24*3600 ] ],
  [ "radius"    ,  "within",    [0, Infinity] ],
  [ "latitude"  ,  "within",    [33.6, 34.6] ],
  [ "longitude" ,  "within",    [-118.9, -117.8] ],
])
.then(genApiResponse)
.fail(genFailResponse)
```
