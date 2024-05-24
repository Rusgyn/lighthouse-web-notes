# NOTES-WEEK-2

# Week 2

## DATA Types and Objects

Primitive vs Non-primitive Types in Javascript
- Primitive data types are immutable (cannot be altered), store single values, do not have methods, cannot be shared, and have default values when not assigned. 
  - Undefined - no value has been assigned to a variable
  - Null - variable has no value or no object.
  - Number - numerical values = Integer and floats
  - String - seq of characters that can hold text
  - Boolean - Logical entity which only two possible values: True or False
  - Symbol (ES6)

- Non-primitive data types are mutable (can be modified), store multiple values, have pre-defined methods, can be shared, and their default value is null when not assigned.
  - Object
  - Array
  - Class
  - Functions

## Objects

- Contain key-value pairs; each key maps to a value.
- Contain keys which are always strings (or symbols, but it's less common and not important right now).
- Have unique keys; the same key cannot appear twice in an object.
- Have their keys point to values which can be of any type.

#### Accessing Objects Value.

  Example:
  ```
    const person = { firstName: "Khurram" };
    const firstName = person["firstName"];
    console.log(firstName);
  ```
  Output:
  
  ```
  Khurram
  ```

  Example:
  ```
    const person = { firstName: "Khurram" };
    const firstName = person["firstName"];
    console.log(firstName);
  ```
  Output:
  
  ```
  undefined
  ```
  JavaScript will indeed look for a variable named firstName. If such a variable is not defined, you will get a ReferenceError: firstName is not defined error, not undefined.

  However, if firstName was defined as a variable and its value was a string that matches a key in the object, you would be able to access the object's property. For example:

  ```
    const person = { firstName: "Khurram" };
    const firstName = person["firstName"];
    console.log(person[firstName]);
  ```
  Output:
  
  ```
  Khurram
  ```
  In this case, firstName is a variable that holds a string, and you can use it to access the property of the object.

#### Assigning a new Value to a Key

Square bracket notation can also be used to assign a new values to new or existing key

  Example:
  ```
  const mary = { name: "Mary Sue" };
  mary["name"] = "Mary Jane";
  mary["age"]  = 22;
  mary // shows the resulting object with both properties
  ```
  Output:
  ```
  { name: 'Mary jane', age: 22}
  ```

#### Object as Values

  Example:
  ```
  const person = {
  name: "Paul",
  address: {
    street: "310 W 95th",
    city: "New York",
    zipCode: 10027
    }
  };
  console.log(perosn["address"]["city"])
  ```
  Output:
  ```
  "New York"
  ```

## Object Keys

Rules:

- Keys are always strings
- Each key is unique (can only occur once in the object)
- Each key is associated with exactly one value. (Note that technically, an array or another object would count as "one value" here, even though they contain other values.)

When writing out object literals, like { myKey: "some value" }, the key is always interpreted as a literal string, even if it's unquoted. It's only necessary to use quotes around the key if the key contains spaces, hyphens or periods. For instance: { "my-hyphenated-key": "some value" }.

By convention, we omit the quotes around keys in string literals whenever we can. If the key is a valid variable name, then we don't have to include quotes

The following example shows two ways of specifying the same value in an object literal: using a literal string for the value, or using a variable.

```
const spam = "spam";
person["dislikes"] = { food: spam, "e-mail": "spam" };
```

## Object.keys
built-in javascript method
tho inspect an objects keys that returns an array of keys

Example:
  ```
  const mary = { name: "Mary Sue" };
  mary["name"] = "Mary Jane";
  mary["age"]  = 22;

  console.log(Object.keys(mary));
  ```
  Output:
  ```
  ['name', 'age']
  ```

## Object Iteration

JavaScript objects, `{key: value}`, themselves are not iterable in the way that arrays are. Instead we need to do things a little differently, using a `for...in` statement.

  Example:
  ```
  var planetMoons = {
    mercury: 0,
    venus: 0,
    earth: 1,
    mars: 2,
    jupiter: 67,
    saturn: 62,
    uranus: 27,
    neptune: 14
  };

  // We can traverse all properties of this object using a for-loop.

  for (var planet in planetMoons) {
    var numberOfMoons = planetMoons[planet];
    console.log("Planet: " + planet + ", # of Moons: "+ numberOfMoons);
  }
  ```

  Output:

  ```
  Planet: mercury, # of Moons: 0
  Planet: venus, # of Moons: 0
  Planet: earth, # of Moons: 1
  Planet: mars, # of Moons: 2
  Planet: jupiter, # of Moons: 67
  Planet: saturn, # of Moons: 62
  Planet: uranus, # of Moons: 27
  Planet: neptune, # of Moons: 14
  ```

  or you may use `for...in` method.

  ```
  for (var planet in planetMoons) {

  // additional filter for object properties:
    if (planetMoons.hasOwnProperty(planet)) {
      console.log("Planet: " + planet + " , #of Moons: " + planetMoons[planet]);
    }
    
  };
  ```

  Output:
  ```
  Planet: mercury , #of Moons: 0
  Planet: venus , #of Moons: 0
  Planet: earth , #of Moons: 1
  Planet: mars , #of Moons: 2
  Planet: jupiter , #of Moons: 67
  Planet: saturn , #of Moons: 62
  Planet: uranus , #of Moons: 27
  Planet: neptune , #of Moons: 14
```

The `hasOwnProperty()` method returns true if the specified property is a direct property of the object — even if the value is null or undefined. The method returns false if the property is inherited, or has not been declared at all.

## this
we cannot use arrow functions when using `this`, always use function operations
arrow function ()=>{} doesn't have context or idea what is it but using ordinary function() {} knows what its referring to (name of the object).
no matter how deep your object is, `this` will always point to the object name.

  Example:
  ```
  const objectOne = {
    breed: "Husky",
    age: 2,
    happyBday: function() {
      this.age++;
    }
  }

  console.log(this.age);
  ```
  Output:
  ```
  3
  ```
## Comparing Objects
- when comparing arrays using `===`, it will always return false 

because they are two separate arrays, regardless of whether they contain the same values or not
- util library's inspect function, intended for debugging and returns a string representation of the object.
  Example:
  ```
  const assertObjectsEqual = function (actual, expected) {
    const inspect = require("util").inspect;

    if (eqObjects(actual, expected)) {
      console.log(console.log(`✅✅✅ Assertion Passed: ${inspect(actual)} === ${inspect(expected)}`));
    } else {
      console.log(`🛑🛑🛑 Assertion Failed: ${inspect(actual)} !== ${inspect(expected)}`);
    }
  };

  assertObjectsEqual({ a: '1', b: 2 }, { b: 2, a: '1' });
  ```

  Output: (with inspect)
  ```
  ✅✅✅ Assertion Passed: { a: '1', b: 2 } === { b: 2, a: '1' }
  ```
  Output: (without inspect)
  ```
  ✅✅✅ Assertion Passed: [object Object] === [object Object]
  ```

## Function as Objects
#### JavaScript Functions as Objects
- One of the distinctive things about JavaScript is that functions are <b>[first-class objects](https://en.wikipedia.org/wiki/First-class_citizen)</b>.

This means two important things:
1. Functions can be stored in variables and passed around
2. Functions can do everything that other objects can do (like having properties assigned to them)

```
const myFn = function () {
  console.log("I am function.");
};

myFn.someAttribute = 42;
console.log(myFn.someAttribute);

function runner(func) {
  func();
}

runner(myFn);
```
Output:
```
42
I am function!
```

So what is going on, and why is it special?

- We assign a function to our variable myFn
- An attribute someAttribute is assigned to that function object
- A `runner()` function is defined that runs the argument `func` that we pass it
- We pass a reference to our `myFn`, which gets invoked by the runner function

#### Callback Functions
- having functions as values in JavaScript is a <b>callback function</b>.

A callback function:

1. Is a function passed (by reference) into another function (let's call that one the "receiver" function)
2. The receiver function is therefore accepting behavior to perform by calling the callback function that it now has access to
3. The receiver function can decide to call the callback function at any time, as many times as it wants

Remember, a callback function is a function that is passed as an argument to another function and is executed after some operation has been completed. 

  Example:
  ```
    // The second argument/parameter (found) is expected to be a (callback) function.

    const findWaldo = function (names, found) {
      for (let i = 0; i < names.length; i++) {
        let name = names[i];
        console.log(name);
        if (name === "Waldo") {
          found(); // execute callback
        }
      }
    };

    const actionWhenFound = function () {
      console.log("Found him!");
    };

    findWaldo(["Alice", "Bob", "Waldo", "Winston"], actionWhenFound);
  ```
  Output:

  ```
  Alice
  Bob
  Waldo
  Found him!
  Winston
  ```
  Note:

  This code illustrates how a function can be treated as an ordinary value and passed around to another function. We pass a reference to the function named actionWhenFound as an argument to another function findWaldo.

  The function actionWhenFound is known as a callback function. It is first defined, then passed as an argument to another function, and finally executed once a specific event occurs.

  Example: 

    ```
    const findWaldo = function (names, found) {

      let foundWaldo = false; //flag that checks if Waldo is found;

      names.forEach((name, index) => {
        if(name === "Waldo") {
          found(name, index);
          foundWaldo = true;
        }
      });
    
      //statement if Waldo is not in the argument.
      if(!foundWaldo) {
        console.log("Waldo not found!");
      }

    };

    const actionWhenFound = function (element, idx) {
      console.log(`Found ${element} at index ${idx}!`);
    };

    //Test Case:

    findWaldo(["Alice", "Bob", "Waldo", "Winston"], actionWhenFound); // => Found Waldo at index 2!
    findWaldo(["Alice", "Bob", "Winston"], actionWhenFound); // => Waldo not found!

    ```
  Output:

  ```
  Found Waldo at index 2!
  Waldo not found!
  ```

#### Anonymous Functions
- Functions dont need to be named, or even assigned to a variable
- cannot be reuse
- Anonymous functions are often declared while being passed in as callbacks to other functions. Why? Because the receiving function that takes in the anonymous function will give that parameter a name anyway.

  Example: callback function defined as "inline"

  ```
  findWaldo(["Alice", "Bob", "Waldo", "Winston"], function (index) {
    console.log("Waldo is located at:", index);
  });
  ```

  ```
  const findWaldo = function(names, actionWhenFound) {

  let foundWaldo = false; // This flag is used to determine if "Waldo" was found during the iteration.

  names.forEach((name, index) => {
    if (name === "Waldo") {
      foundWaldo = true; // If "Waldo" is found, the flag is set to true.
      actionWhenFound(name, index); // The anonymous callback function is invoked with the name and index as arguments.
    }
  });
  
  // If "Waldo" was not found during the iteration, an error is thrown.
    if (!foundWaldo) {
      console.log("Waldo not found!");
    }
  };

    //Test Case:
    
    findWaldo(["Alice", "Bob", "Waldo", "Winston"], function(element, idx) {
    console.log(`Found ${element} at index ${idx}!`);}); // => Found Waldo at index 2!
    
    findWaldo(["Alice", "Bob", "Winston"], function(element, idx) {
      console.log(`Found ${element} at index ${idx}!`);
    }); // => Waldo not found!
  ```
  Output:
  ```
  Found Waldo at index 2!
  Waldo not found!
  ```

#### Arrow Functions
- shorter function


## Higher Order functions
- Functions that take in callbacks
- functions which operate on other functions
- functions that takes other function as an argument or returns a function as a result.
- built-in functions such as forEach, filter, rejects (opposite of filter), map and others can be called "Higher-Order Functions".

functions are values

```
function triple(x) {
  return x * 3;
}
```
```
let triple = function(x) {
  return x * 3;
}
let waffle = triple;

console.log(waffle(30));
```

Function is assigned to a variable waffle or pass to other functions (higher order functions)

#### Filtering Using Callbacks
  ```
  const numbers = [1, 2, 3, 4, 5, 7, 10, 14, 17, 18];
  const evens = numbers.filter(function(num) {
    return num % 2 === 0;
  });
  console.log("Subset of even numbers:", evens);
  ```

  > Question:
    Can you spot the callback function in the above example? What is it responsible for and what is it named?
  > Answer:
    evens' is actually the name of the array that stores the result of the filter operation.
    The callback function in this case is an anonymous function, which means it doesn't have a name. Here it is:
    ```
    function(num) {
      return num % 2 === 0;
    }
    ```

    Remember, a callback function is a function that is passed as an argument to another function and is executed after some operation has been completed. In this case, the callback function is executed for each element in the 'numbers' array when the filter method is called.

## VIM
- is pretty useful - if not absolutely necessary - if you have to edit a file in a remote ssh terminal.
- Vim is also the default editor for git -- it launches vim when it needs additional text from you, such as a commit message.

> <b>Instruction:</b>
> To launch, open your terminal and type vim.

#### Moving around
- "H" moves left
-  "K" moves up; 
- "L" moves right;
- "J" moves down.
- Y copies a line of text to the buffer
- P pastes it to the cursor's current position.
- dd will delete the whole line of text. This will also effectively "cut" a line of text as well. When you delete a line, it's placed in the buffer.
- yy copies a whole line of text.

#### Create/Open a file
> <b>Instruction:</b>
> Create a new file and open it in vim by typing `vim tutorial.txt`
> Will create a file named `tutorial.txt` and open it in vim

#### Edit a file
- To switch to edit mode (also called "insert mode") you need to give VIM a command to tell it to switch modes.
  - Press "i" to begin inserting text at the current cursor position.
  - Press "a" to begin inserting after the current cursor position.

> <b>Instruction: </b>
> Press "i" in the file to enter insert mode. Add some text to the file.

Getting out of editing mode

> <b>Instruction: </b>
> Press `ESC` in the file to make sure you are back to command mode.

#### Saving a File
- Make sure you are in command mode. Use escape key to make sure.
>type `:w`

#### Quit VIM
> `:wq` - write (save) and quit file (and vim)
> `:q!` - quit and ignore changes made since last file save.