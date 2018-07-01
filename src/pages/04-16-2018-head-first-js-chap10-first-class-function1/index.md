---
path: "/head-first-js-chap10-first-class-function1"
date: "2018-04-16"
title: "Head first: JavaScript chapter 10: First Class Function: liberated functions"
---

At the beginning of the chapter, the role of function is emphasized and two ways of creating a function are introduced: function declaration and function expression. They seem to have no differences but actually there is and I'm going to figure out.

Basically, function declaration is called before your entire code is executed while function expression will wait until its turn to be invoked. Another thing is naming, function declaration has its name created before it refers to the function while function expression doesn't really have name. It can only get one when you assign a name to it.

That's why function in javascript is first class value. It does a few things in order to be entitled with that name

- It assigns value to a variable

- Pass the value to a function

- return the value from a function.

