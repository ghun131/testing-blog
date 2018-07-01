---
path: "/head-first-js-chap10-first-class-function1"
date: "2018-04-16"
title: "Head first: JavaScript chapter 10: First Class Function: liberated functions"
---

1.
At the beginning of the chapter, the role of function is emphasized and two ways of creating a function are introduced: *function declaration* and *function expression*. They seem to have no differences but actually there are and I'm going to be told.

Basically, *function declaration is called before your entire code is executed while function expression* will wait until its turn to be invoked. Another thing is naming, function declaration has its name created before it refers to the function while function expression doesn't really have name. It can only get one when you assign a name to it.

That's why function in javascript is first class value. It does a few things in order to be entitled with that name:

- It assigns value to a variable
- Pass the value to a function
- Return the value from a function.

2.
Everything's been okay until something go like this:

```javascript
function createDrinkOrder(passenger) {
  if (passenger.ticket === "firstclass") {
    alert ("Would you like a cocktail or wine?");
  } else {
    alert ("Your choice is cola or water.");
  }
}
```
and then it is passed into this function

```javascript
function serveCustomer(passenger) {
    createDrinkOrder(passenger);
    //get dinner order
    createDrinkOrder(passenger);
    createDrinkOrder(passenger);
    //show movie
    createDrinkOrder(passenger);
    // pick up trash
}
```

It is said that "we’re unnecessarily **recomputing what kind of passenger** we’re serving in createDrinkOrder every time we take an order." which I don't understand how did we recompute the passenger. May be they are talking about the `if (passenger.ticket === "firstclass")`.
Let move on to see if I get it right. Another approach to avoid that redundant computing goes like this:

```javascript
function createDrinkOrder(passenger) {
    var orderFunction;
    if (passenger.ticket === "firstclass") {
        orderFunction = function() {
            alert ("Would you like a cocktail or wine?");
        };
    } else {
        orderFunction = function() {
            alert ("Your choice is cola or water.");
        };
    }
    return orderFunction;
}
```

And here is how it is passed:

```javascript
function serveCustomer(passenger) {
    var getDrinkOrderFunction = createDrinkOrder(passenger);
    getDrinkOrderFunction();
    //get dinner order
    getDrinkOrderFunction();
    getDrinkOrderFunction();
    //show movie
    getDrinkOrderFunction();
    // pick up trash
}
```

I can see that it has the same structure with the previous approach but now `createDrinkOrder(passenger)` is hooked into `getDrinkOrderFunction` which would be later invoked in function style `getDrinkOrderFunction()`.

One question come to my mind after reading this part is that whether this new way would avoid the pitfall of the old approach. I guess it can only do that if from var `getDrinkOrderFunction = createDrinkOrder(passenger);`, passenger type is calculated and `orderFunction` is returned. Therefore, `getDrinkOrderFunction()` only triggers the alert box.

*Hope I get it right because it would be a real pain in the neck if this question still hang over my head when I'm at chapter 11*

3.
Btw before finishing all of my babbling nonsense, I just want to say how amazing it is to know that JS function is first class value and it can be passed around like number, string or object. Just yesterday I took any method that use callback function (such as map, filter, reduce or sort - this one I learn from this chapter) for granted, now it makes so much sense. Each day I connect every single dot to see the big picture.