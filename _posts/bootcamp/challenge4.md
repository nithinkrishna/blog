---
layout: normal
title: Bootcamp | Codebrahma
permalink: /bootcamp/challenge/4/
---

##TheGuitarApp

* In this simplified musical world, there are only 6 notes(A-F).
* A guitar has six strings which can correspond to one of these notes, not necessarily unique.
* The tuner box is used to tune the guitars. It can only tune one guitar string at a time.
* Each note has a unique color associated to it. So when Jimmy wants to pick a guitar to play, he'll know the notes it can play just by looking at it.

###Capabilities

1. User should be able to add an Awesome guitar to the guitar collection.
2. User should be able to remove the guitar from the guitar collection.
3. User can name his guitars, while adding them to his collection.
4. The User can choose one of the 6 possible strings from the slider(s1-s6).
5. The User can choose a guitar by clicking on one from the list. The selected guitar name should be highlighted in the list.
6. The User can choose one of the 6 notes from the tuner, after selecting the guitar and the string. This will tune the selected guitar's selected string to the selected tuner note.

<img src="/images/guitar.png" width="100%" />

###CodeSmells

We expect the anuglar code to be properly structured and as declarative as possible. This is how your final code should look like.

{% highlight html %}
<div data-ng-repeat="guitar in collection">
  <guitar data-guitar="guitar" data-retune-with="notes"></guitar>
</div>

<guitar-collecter data-collection="collection"></guitar-collecter>

<tuner data-string="selectedString" data-guitar="selectedGuitar"></tuner>
<tuner-addon data-selected-string="selectedString" data-selected-guitar="selectedGuitar"></tuner-addon>
{% endhighlight %}

##TechSpec

1. Data should persist in a MySql Database.
2. Build backend controllers and models, add necessary validation.
3. Every frontend change needs to persist.
4. Javascript code needs to be structured. Use ngResource for server interactions.

##Bonus

Additional points if you are able to incorporate sound. Have 6 sounds, each sound corresponds to a defined note. When I click on a guitar string, the corresponding sound associated to the string's tuned note needs to play.
