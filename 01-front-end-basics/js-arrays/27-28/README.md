# <img src="https://cloud.githubusercontent.com/assets/7833470/10423298/ea833a68-7079-11e5-84f8-0a925ab96893.png" width="60"> Array Methods

|Learning Objectives|
| :--- |
| Create arrays and store them in variables |
| Access and change information inside arrays with array methods |
| Explain examples that use callback functions to create more flexible code |
| Traverse arrays with `for` loops and the `forEach` iterator array method |



##Array Method Basics##

```javascript
var fruits = ["Apple", "Banana", "Cherry", "Durian", "Elderberry",
"Fig", "Guava", "Huckleberry", "Ice plant", "Jackfruit"];
```

Accessing the **first** element:  

```javascript
fruits[0]; // "Apple"
```

Accessing the **length**:

```javascript
fruits.length; // 10
```
Accessing the **last** element:  

```javascript
fruits[fruits.length-1]; // "Jackfruit
```
**Adding** an element to the **front**:

```javascript
fruits.unshift("Apricot"); // 11
```

**Adding** an element to the **end**:  

```javascript
fruits.push("Kiwi"); // 12
```

**Removing** an element from the **front**:

```javascript
fruits.shift(); // "Apricot"
```

**Removing** an element from the **end**:  

```javascript
fruits.pop(); // "Kiwi"
```
**Finding** the index of an element:  

```javascript
fruits.indexOf("Jackfruit"); // 9
fruits[9]; // "Jackfruit"
```

**Removing** an element by index position:  

```javascript
var huckleBerryPos = fruits.indexOf("HuckleBerry");
var removedItem = fruits.splice(huckleBerryPos, 1);
// ["Apple", "Banana", "Cherry", "Durian", "Elderberry", "Fig", "Guava", "Ice plant", "Jackfruit"];
```

![img](https://thewaysofk.files.wordpress.com/2015/03/fruit-row.png)


## Basic array traversal with `for` ##

By now you've all used `for` to iterate over your arrays.  

```js
var fruits = ["Apple", "Banana", "Cherry", "Durian", "Elderberry",
"Fig", "Guava", "Huckleberry", "Ice plant", "Jackfruit"];

for (var i=0; i<fruits.length; i++) {
  console.log("eating a", fruits[i]);
}
```   

<!--  --> 



**Quick Exercise**:  Practice array methods with  [Challenge Set A](exercises.md)!



## Passing functions to other functions ##

When we call a function, we usually pass some arguments to it.  For example here, we're passing a string `Strawberry` to the `indexOf` function.

```js
fruits.indexOf("Strawberry");
```
We can do this with our own functions as well.

```js
function makeSandwich(meat, cheese) {
  return "bread, " + meat + ", " + cheese + ", bread";
}

// call makeSandwich and pass arguments to it
makeSandwich("turkey", "provolone");  // => bread, turkey, provolone, bread
```


Arguments can also be passed in with their variable names.

```javascript
var favoriteMeat = "ham";
makeSandwich(favoriteMeat, "colby");  // call makeSandwich with "ham" and "colby"
```

We can pass other types of arguments too, including arrays and objects.

```js
function makeBigSandwich(toppingsArray) {
  return "bread," + toppingsArray.toString() + ", & bread";
}

makeBigSandwich(['ham', 'salami', 'provolone']);
// "bread,ham,salami,provolone,&bread"
```

**We can also pass functions as arguments.**  In fact, JavaScript treats functions a lot like any other data type; you can pass them into other functions as arguments, return functions from functions, and store them in variables. 

When a function is passed in as an argument, it can be called within the function at whim.  

First let's look at a function that just uses another function.

```javascript
function add(a, b) {
  var result = a + b;
  console.log(result);
}
```

<details>
  <summary>What are the two functions that are called above?</summary>
  <p>The functions that get called are `add` and `console.log`! </p>
</details>


Now let's make our `add` function a little more flexible. We'd like the option to display the result in multiple ways instead of always using `console.log`.  We'll remove `console.log` and pass in a more generic display function to call instead.

```javascript
function add(a, b, displayFunction) {
  var result = a + b;
  displayFunction(result);  // use the displayFuction function to show the result
}

function printToConsole(input) {
  console.log(input);
}

// then calling it:
add(2, 2, printToConsole); // => console logs 4
```

When a function takes in another function and calls it, we say the second function is a "callback" function.  

<details><summary>Which function above is a callback function?</summary><p>`displayFunction` is the name of the callback in the definition of `add` above. When we actually called `add`, we gave it the specific callback function `printToConsole`. </p></details>

We can also use a different function as the `displayFunction`.  This gives us a lot of flexibility.

```javascript
function toAlert(input) {
  alert(input);
}

// then calling it:
add(8, 9, toAlert); // => alerts 17
```

A common way to write this is to define the `displayFunction` function **in-line** with the main function call.

```javascript

// defining our specific display function as we call the add function ("in-line"):
add(8, 9, function toAlert(input) {
  alert(input);
}); // => still alerts 17
```

![img](http://i.giphy.com/lUQxdO6Y7Vmx2.gif)

Let's have another example, a more delicious example:

```javascript

function eatSandwich(topping1, topping2, topping3, sandwichMaker) {
    console.log("I'm going to make and eat a sandwich with: " + topping1 + ', ' + topping2 + ' and ' + topping3);
    var layers = [topping1, topping2, topping3];
    var sandwich = sandwichMaker(layers);
    console.log("Finished eating my " + sandwich + " sandwich!");
}

function makeBigSandwich(toppingsArray) {
  return "bread," + toppingsArray.toString() + ",&bread";
}

// then to call the function:
eatSandwich('bacon', 'lettuce', 'tomato', makeBigSandwich);
```

We passed the `makeBigSandwich` function to the `eatSandwich` function as an argument.  `eatSandwich` calls `makeBigSandwich`.

![img](http://i.giphy.com/ZgWYWo814vti8.gif)

And now we'll re-write this with the function definition in-line with the function call.

```javascript

// eatSandwich stays the same
var eatSandwich = function(topping1, topping2, topping3, sandwichMaker) {
    console.log("I'm going to make and eat a sandwich with: " + topping1 + ', ' + topping2 + ' and ' + topping3);
    var layers = [topping1, topping2, topping3];
    var sandwich = sandwichMaker(layers);
    console.log("Finished eating my " + sandwich + " sandwich!");
}

// then to call the function:
eatSandwich('bacon', 'lettuce', 'tomato', function makeBigSandwich(toppingsArray) {
  return "bread," + toppingsArray.toString() + "&bread";
});
```

## Array Traversals and Actions ##

Let's get back to arrays.

We've seen we can traverse an array of elements with a simple `for` loop, but this isn't the most streamlined approach to accessing and changing a list in Javascript.

Javascript has provided us with quite a few powerful built-in "iterator" methods that make it a breeze to do something to each element in an array. Plus, they give us great opportunities to practice using callbacks! 

*Being able to use these methods is one sign of a more mature developer.  We encourage you to use iterators instead of traditional `for` loops wherever you can!*



### `array.forEach()` ###

To loop through an array with the ability to alter each element, similar to a `for` loop traversal, JavaScript gives us an Array method called `forEach()`.

**`forEach` function skeleton**:

```javascript
array.forEach(function callBack(element, index) {
    console.log(index + ". " + element);
});
```

Fruity Example - Make a numbered list

```javascript
fruits.forEach(function callBack(element, index) {
  console.log(index + ". " + element);
});
/*  0. Apple
  1. Banana
  2. Cherry
  3. Durian
  4. Elderberry
  5. Fig
  6. Guava
  7. Huckleberry
  8. Ice plant
  9. Jackfruit
*/
```


**Quick Exercise**:  Practice `forEach` with  [Challenge Set B](exercises.md)!

![img](http://www.ontariotenderfruit.ca/trade/images/fruit-row.png)

### Array Method Documentation!

Check out Mozilla Developer Network's <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array" target="_blank">Array documentation</a> for more information on arrays. All of the methods listed in the <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array#Array_instances" target="_blank">Array instances</a> section are available to use with JavaScript arrays. Commonly used methods in this section include `join`, `sort`, and `reverse`.

