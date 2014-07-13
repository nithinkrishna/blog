---
layout: post
title:  "Angular-js Game of Life"
date:   2014-02-23 20:22:07
categories: angularjs
---


##Life and Beyond

Ever heard of the game of life challange? Well, It involves building a working version of [John Convoy's game of life](http://en.wikipedia.org/wiki/Conway's_Game_of_Life) in any programming language in under 45 minutes. Though I fell way short of the 45 minute mark, I did manage to make a working version of it.

Quoting Sheldon Cooper _"Quantum physics makes me so happy. It's like looking at the universe naked."_ well understanding the game of life kinda brings up a similar feeling.

So what's this game of life? Like the name suggests the game of life is not a mere game. __There are no players, no winners or loosers only the game.__ There is just an initial configration and rules which govern the system.

So what are the rules?

* Any live cell with fewer than two live neighbours dies, as if caused by under-population.
* Any live cell with two or three live neighbours lives on to the next generation.
* Any live cell with more than three live neighbours dies, as if by overcrowding.
* Any dead cell with exactly three live neighbours becomes a live cell, as if by reproduction.

Simple enough right? Create a matrix of (n*n) cells, impose these constraints and watch the system progress form one generation to another. __The results of this simple experiment is mindblowing.__ Try playing around with the initial configration of the system and observe the diverse patterns which are produced by minute changes to the initial configration.

Let's break this down. You can see 2010 in there, which is the my year of joining and '10z10y00xx' which is apparently my register number. I was a little bored last night so changed the register number at the end of the URL to 10z10y00x(x+1).jpg and guess what? I was able to see my friend's picture as well. What did this mean? Well.. I can now access every fourth your student's image from the SRM database.

In essence the game of life demonstrates how complex patterns and behaviors can emerge from simple rules imposed on a system. The infinite diversity of nature can be explained by this very simple idea.

Everything form the __Big bang__ to __Abiogenesis__ are examples of systems with a fixed initial configration and rules governing the interaction of the various elements in the system, with each other. The results of both these phenomenon is the world as we know it today.

Propability suggests that in almost all situations, systems endup with stable patterns. Once a system reaches such a stable state, it remains stable forever if not acted upon by an agent form outside the system. This stable state may not necessarily be static. With this observation and my understanding of string theory I'd say that it's possible that even our universe is in such a state and will remain so for ever untill acted upon by another universe governed by laws that control a system of universes.

It's also conceivable to look at these elements in a system as individual subsystems which have numerous elements within them, and any interaction between two such subsystems would result in changes in elements within each subsystem as well.

Thus everything from quarks to quasars can be seens in such a light.

Well the most amusing part of the theory is that a half baked computer engineer can claim to understand the universe just after writing a few lines of code :)

There are some facinating patterns that arise from this experiment. [These](http://en.wikipedia.org/wiki/Conway's_Game_of_Life#Examples_of_patterns) are a few you should try out. One such intersting pattern is depicted below. It's called [Gosper Glider Gun pattern](http://en.wikipedia.org/wiki/Gun_(cellular_automaton)). Originally Conway thought that no pattern could ever grow indefinitely, he offered a 50$ prize for a person who could disprove his assumption. A team form MIT did exactly that and came up with the gosper glider gun which is the smallest possible pattern which can grow indefinitely.

[Epic?](https://www.youtube.com/watch?v=C2vgICfQawE)

Try out the [single player game](http://gameoflife-nithink.rhcloud.com/home.php) I made based on the game of life. Try to top the [attempts](http://gameoflife-nithink.rhcloud.com/attempts.php).


<img src="https://db.tt/HkuLY0Pu" />

* * *

[Github](https://github.com/nithinkrishna/angularjs-game-of-life).
[Website](http://gameoflife-nithink.rhcloud.com).
[Screen Shot](https://db.tt/HkuLY0Pu)