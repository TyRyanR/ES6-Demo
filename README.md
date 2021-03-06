# ES6-Demo
Arrow functions, Default Parameters, Shortening Properties and Methods

**************************************

## Default Params

Default function parameters allow formal parameters to be initialized with default values if no value or undefined is passed.

### Passing undefined

In the second call here, even if the second argument is set explicitly to undefined (though not null) when calling, the value of the color argument is the default one.

function setBackgroundColor(element, color = 'rosybrown') {
  element.style.backgroundColor = color;
}

```js
setBackgroundColor(someDiv);            // color set to 'rosybrown'
setBackgroundColor(someDiv, undefined); // color set to 'rosybrown' too
setBackgroundColor(someDiv, 'blue');    // color set to 'blue'
```

### Evaluated at call time

The default argument gets evaluated at call time, so unlike e.g. in Python, a new object is created each time the function is called.

```js
function append(value, array = []) {
  array.push(value);
  return array;
}

append(1); //[1]
append(2); //[2], not [1, 2]
```

##Arrow functions
An arrow function is an anonymous function expression that doesn't change the value of `this`.

When one wants to call the `this` function repeatedly over the course of your code, using an arrow function is a way to execute functions without throwing that off or needing to save `this` to a variable.

For example:

```
function Person() {
  this.age = 0;

  setInterval(function growUp() {
    this.age++;
  }, 1000);
}
```
In this code, the first `this` is referring to the Person object, but the second `this` is instead referring to the growUp function. That means it won't be able to find the age value, and this whole thing won't work like it's supposed to.

The old way of fixing this would involve saving a reference to `this` early on:
```
function Person() {
  var person = this;
  person.age = 0;

  setInterval(function growUp() {
    person.age++;
  }, 1000);
}
```
But now, the arrows can help you sidestep this problem entirely.
```
function Person() {
  this.age = 0;

  setInterval(() => {
    this.age++;
  }, 1000);
}
```
Now, the arrow function runs the function without creating its own context for `this`, and the age value should increase as intended.

Arrow function expressions don't work especially well in method functions, though. You shouldn't worry about them if you're not working with non-method functions.





### Object Methods Shorthand
```js
//
// ES 5 **
//

var dog = {
  bark: function() {

  },
  layDown: function () {

  }
}

//
// ES 6 **
//
var dog = {
  bark() {},
  layDown() {}
}
```

### Object Properties Shorthand
```js
//
// ES 5 **
//
function createCar(make, model) {
  return {
    type: "car",
    make: make,
    model: model
  };
}

var ferrari = createCar("Ferrari", "488 GTB");

/* RETURNS */
{
  type: "car",
  make: "Ferrari",
  model: "488 GTB"
}



//
// ES 6 **
//
function createCar(make, model) {
  return {
    type: 'car',
    make,
    model,
  };
}

var ferrari = createCar("Ferrari", "488 GTB");

/* RETURNS */
{
  type: "car",
  make: "Ferrari",
  model: "488 GTB"
}
```

### Computed Property Names

```js
//
// ES 6 **
//

var a = 1;
var b = 2;

var obj = {
  [a + b]: 12
}

console.log(obj);

/* RETURNS */
{
  3: 12
}
```
