---
layout: post
title:  "Zooming with CSS scale"
categories: sublime-text
comments: true
description: Zoom implementation on the browser with css scale
tags:
  - browser
  - css
author: Nithin Krishna
handle: "nithinkrishh"
---

### Zooming with CSS Transform Scale (TIL)

Altering the css3 transform scale property on a div can help you give the user ability to zoom in/out of a div.

[Example](https://www.youtube.com/embed/YAZ1RTWhGSI).

The problem with this approach is that when the element scales the size of the element is changed appropriately. This is because the browser changes the picture aspect ratio but not the amount of pixels.

A work around this is proportionally increasing/decreasing the size of the div when the scale property is changed.

Some simple math. Lets say the scale is changed from 1 to 0.8. It means that the dimensions are reduced by 25%. So to compensate for this, the height / width have to be increased in the same proportion.


```javascript
// Let's say 0.8
function onZoom(newScale){
  $("#holder").css({
    "webkit-transform": newScale,
    "width": ( (1 / newScale) * $("#holder").width()) + "px",
    "height": ( (1 / newScale) * $("#holder").height()) + "px",
  });
};
```
