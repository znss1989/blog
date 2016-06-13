---
layout: post
title: "On object-oriented JavaScript"
date: 2016-06-13
author: Wu Lei
categories: Article
tags: JavaScript
---

### Object-oriented JavaScript

An **object** is a container for values in the form of **properties**, and functionalities in the form of **methods**.

Name of an object property is a key, content of the property is a value. Methods may or may not return values.

Category of objects:
- Native objects: like string, number, boolean, array and object.
- Host objects: provided by environment where JS is running, like `document`, `console` and element.
- Customized objects: designed by developer.

Access to properties: 
- Dot notation: More convenient, but may not work when keys are not valid JS variable name.
- Bracket notation: with its key always as a string inside, this always works.

##### Methods

Encapsulation of functionality as a method:


```
var someOjbect = {
    "someMethod": function() {
        console.log("This is an anonymous function.");
    }
}
```

For methods to access variables of the object:

```
var dice = {
    sides: 6;
    roll: function() {
        var randomNum = Math.floor(Math.random() * this.sides) + 1; // this means the object where the method is being called, do not use dice.sides
        console.log(randomNum);
    }
};
```

For methods to change object properties:

```
var calculator = {
    sum: 0,
    add: function(value) {
        this.sum += value;
    }
};
```

##### Constructor

Constructor functions describes how an object should be created. Each object created this way is an instance of the object type. An instance is a specific realization of particular type of object.

E.g:

```
// Constructor
function Contact(name, email) { // Uppercase is usually used for constructor
    // this = {}; 'this' is a new instance of the object, when constructor gets called
    this.name = name;
    this.email = email:
    this.sendEmail: function() {
        /* Do something */
    };
    // return this; The return statement is also neglected in a constructor
}
// Create a new instance
var tom= new Contact("Tom", "tom@example.com");  // The new keyword turns a regular function call into a constructor call
```

The [new](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new) keyword turns a regular function call into a constructor call. 

##### Prototype

In the way above for creating the constructor of a specific type of object, the method would be instantiated for each implementation of instance as well, even though, different instances share the identical method.

One solution might be:

```
function diceRoll() {
    var randomNum = Math.floor(Math.random() * this.sides) + 1;
    return randomNum;
}

function Dice(sides) {
    this.sides = sides;
    this.roll = diceRoll;
}

var dice = new Dice(6);
var dice10 = new Dice(10);
console.log(dice.roll === dice10.roll);
```

But this is difficult for encapsulation and code management.

The other better solution is to use **prototype**. 

```
function Dice(sides) {
    this.sides = sides;
    this.roll = diceRoll;
}
// Prototype
Dice.prototype.roll = function () {
    var randomNum = Math.floor(Math.random() * this.sides) + 1;
    return randomNum;    
};

var dice = new Dice(6);
var dice10 = new Dice(10);
console.log(dice.roll === dice10.roll);
```

Prototypes are used as templates for objects, which would be share by all instances from the same object template/prototype. 

##### Inheritance

[Inheritance](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain) is a technique that allows sharing same code between similar types.

How **Prototype chain** works: 
- When accessing a property or a method, JS first checks whether it is in the instance.
- If not, it will check the prototype.
- If not, it will check the next prototype up the chain.

E.g.:

```
function Media(title, duration) {
    this.title = title;
    this.duration = duration;
}
Media.prototype.play() = function() {
    this.isPlaying = true;
};

function Song(title, artist, duration) {
    var self = this;
    Media.call(self, title, duration); // The call method allows executing a function where we specify what the function should use as 'this', now Media is called as a regular function
    this.artist = artist;
}
Song.prototype = Object.create(Media.prototype); // It copies the prototype methods and propertis of Media to Song's prototype

// Add prototype specific to type of Song here
```
