---
path: "/head-first-js-chap12-advanced-object-construction-creating-objects"
date: "2018-05-08"
title: "Head first JS Chap 12: Advanced Object Construction: Creating objects"
---

*This is not the first time I read about Object Construction but last time was so brief that now I can barely recall anything except a metaphor about a factory that churns out object each time you need to call any of them.*

###1.
As far as I know **Object Constructor** is like a child between function and object because it has both features. It takes parameters and can be reused like function while having "this" in it and contains properties and methods. Unlike its father - function, its name is capitalized for the first letter and unlike its mother - object, it doesn't use comma. I can provide an example of object constructor from the book. It goes like this:

```javascript
function Coffee(roast, ounces) {
    this.roast = roast;
    this.ounces = ounces;
    this.getSize = function() {
        if (this.ounces === 8) {
            return "small";
        } else if (this.ounces === 12) {
            return "medium";
        } else {
            return "large";
        }
    };
    this.toString = function () {
        console.log("You've ordered a " + this.getSize() + " " + this.roast + " coffee.");
    };
}
```

I think its look is quite balanced with 2 properties (roast and ounces) and two methods (`getSize` and `toString`). Now let see how it create objects:

```javascript
var houseBlend = new Coffee("House Blend", 12);
var darkRoast = new Coffee("Dark Roast", 16);
```

It has keyword **new** which is really new to me (because I had thought that it would have been invoked like a normal function.). Come to know of it, **new** is a operator (like +, -, +=, === etc.) that would work only with function (as far as I know). An interesting detail is that **new** is the one who create object not the constructor.

###2
Something quite annoying has happened today about object contructor. Let say I have one like this:

```javascript
function Car(make, model, year, color, passenger, convertible, mileage, started) {
            this.make = make;
            this.model = model;
            this.year = year;
            this.color = color;
            this.passenger = passenger;
            this.convertible = convertible;
            this.mileage = mileage;
            this.started = started;
            this.start = function () {
                this.started = true;
            }
            this.stop = function () {
                this.started = false;
            }
            this.drive = function () {
                if (this.started) {
                    return this.make + " goes zoom zoom!";
                } else {
                    return "Start the engine first!";
                }
            }
        };
```

That many parameters may one day get me into big trouble with hard-to-find bugs. So they propose a way to refactor this constructor for easier use:

```javascript
function Car(params) {
    this.make = params.make;
    this.model = params.model;
    this.year = params.year;
    this.color = params.color;
    this.passengers = params.passengers;
    this.convertible = params.convertible;
    this.mileage = params.mileage;
    this.started = params.started;
    this.start = function() {
        this.started = true;
    }
    this.stop = function() {
        this.started = false;
    }
    this.drive = function() {
        if (this.started) {
            console.log(this.make + " " + this.model + " goes zoom zoom!");
        } else {
            console.log("Start the engine first.");
        }
    }
};
```

and now each time I want to create a new object, just make one object literal and pass it into the constructor. Something like this:

```javascript
var cadiParams = {make: "GM",
                model: "Cadillac",
                year: 1955,
                color: "tan",
                passengers: 5,
                convertible: false,
                mileage: 12892};

var cadi = new Car(cadiParams);
```

So basically, apart from the methods, I need to hand-write most of the properties much like declaring object literals. Such a half-baked solution! Can't believe I was rejoiced when I had learned about object constructor at the beginning of this chapter.
Btw, this chapter introduces the book "*JavaScript the definitive guide*" which is about roughly 1100 pages and if I want to learn more about JS built-in object, this one is definitely a good choice.