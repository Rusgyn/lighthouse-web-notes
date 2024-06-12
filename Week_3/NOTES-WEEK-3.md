# Week_3
## Debugging
#### Troubleshooting Tips
Have I...
...pseudo-coded the solution?

...googled the error message I am getting?

...actually READ the error message?

...double-checked my syntax?

...linted my code?

...pair programmed or gotten a peer to code review?

...rubber-ducked the problem?

If the answer to all of these questions is yes, then you have done your due diligence and should be calling a mentor over.

## Mocha and Chai

Assertion
- only flase message will be printed in the console
  Example:
  ```
  console.assert(trues === true, 'is true');
  console.assert(true === false, 'not equal');
  ```
  output:
  ```
  not equal
  // true is not equal to false hence its false, you will see the output
  ```
  Example 2:
  ```
  function sayHello() {
    return 'hello there!';
  }

  const hello = sayHello();
  console.log(hello);
  console.assert(sayHello() === 'hello theyee', 'not equal');
  ```
  output:
  ```
  hello there!
  not equal //because the output is not the same, check the spelling.
  ```
## Object methods and -this-

<u>Functions as Object Properties (AKA Methods)</u>

  Example:
  ```
  const person = {
    firstName: 'Bob',
    lastName:  'Smith',
    fullName: function() {
      return this.firstName + ' ' + this.lastName;
    }
  }

  // Nice, now I can just say:
  console.log('Hello, ' + person.fullName());
  // And it's much "cleaner" every time I need their full name!
  ```
  Output:
  ```
  Hello, Bob Smith
  ```

<b>Method</b> - functions that are attached to the object. Introducing concept of method, we've also introduced the concept of `this`

<u>A Limited Introduction to `this`</u>
- `this` only needing to be used inside methods like the `fullname of person object` example above.
- `this` refers to the object method (function) was called on.

## Arrow Functions and -this-
- Arrow Function syntax can vary based on how simple the function is
- Arrow functions don't get assigned a value for this (in the way that traditional function expressions do).
  - This "limitation" is in fact intentional, and can be used as an advantage in certain situations - situations where it is beneficial to inherit the value of this from its lexical scope. Such as the this.firstName being read in the sayHello method.

# Recursion
- When a function calls itself until it doesn't.

Recursion is an alternative to traditional looping that allows you to do the same thing, just in a slightly different way. Recursion isn't necessarily a better way of doing this, it's just a different way of doing this.

In fact, some languages don't have any for or while loops, and recursion is the only way of repeating code like this.

  Example:
  ```
  1.| function countEvenToTwelve(number) {
  2.|   if (number <= 12) { // Recursive Case
  3.|     console.log(number);
  4.|     // The function will call itself again and get closer to the base case
  5.|     countEvenToTwelve(number+2);
  6.|   }
  7.|   // Base case, do nothing when number > 12
  8.| }
  9.| countEvenToTwelve(0);
  ```
  Output:
  ```
  0
  2
  4
  6
  8
  10
  12
  ```

<b>Recursion</b> is a tool you can use as an alternative to traditional iteration using for and while loops.

- Every recursive function must have a base case and a recursive case.
- Each recursive call should break down the current problem into a smaller, simpler one.
- The recursive calls must eventually reach the smallest version of the problem, the base case.
- The base case is when the problem can be solved without further recursion.

- Any problem that you can solve with a for loop, you can solve with recursion, and vice versa.
- Every recursive function has at least one recursive case that causes the function to call itself.
- A recursive function cannot stop calling itself if it doesn't have a base case.
Every recursive function must stop calling itself at some point using a base case, otherwise it will just continue to call itself forever, like an infinite loop.

#### Breaking down recursion
1. Figure out the base case
2. Recursive case

Base case - involves no calls to itself. The base case happens when the input to the function is so basic that calling the function again is not required.

Recursive case - when the function will continue to call itself. Every time the function calls itself, the input gets closer and closer to the base case.

#### Summary
- Any iteration problem can be solved with recursion and  vice versa

To recap, recursion is a technique whereby a function calls itself until it doesn't. Any iteration problem can be solved with recursion and vice versa. Each has its advantages and uses, and some problems, like the one we explored earlier, are easier to solve with recursion.

It's also worth noting that recursion is a type of control flow. When we read loops and if statements, we know which line will execute next based on the situation. With recursion, it may seem harder to follow the control flow but only because you are not yet used to dealing with it. As with all things, it will take practice.

# Introduction to Modules

- modules are its way of organizing code into individual files
- every js file in node is implicitly a module
  - we can `console.log(module)` and see its details
- `module.exports` tells node what to export from a file
  - it defaults to `{}`
  - exporting a function or variable makes it accessible to other modules that import it. If a function or variable is only used within the module it's defined in, there's no need to export it.
- we can use `require` with relative paths (like ./myModule)
  - it doesn't need the `.js` extension, as that is implied

With this knowledge, we can now start to DRY up our Lotide project!

  Example: 
  ```
  //myModule.js

  const sayHelloTo = function(person) {
    console.log(`Hello, ${person}`);
  }
  // add this line to the end of the file.
  module.exports = sayHelloTo;
  ```
  ```
  //main.js

  const sayHelloTo = require('./myModule');

  // Just to check the value of what we just required here
  console.log('sayHelloTo: ', sayHelloTo);

  sayHelloTo('Bernie');
  ```

  Output:
  ```
  > node main.js //Runt this command
  sayHelloTo:  [Function: sayHelloTo]
  Hello, Bernie
  ```

# Packages and npm
Packages - are self-contained code libraries that we can install and use in our projects.

npm - Another powerful feature of Node.js is its package manager

A "library" is a collection of pre-written code. Libraries can be private, but many are packaged up nicely, branded and made publicly available for other developers to use in their own projects.

<b>jQuery</b> and <b>Bootstrap</b> are a couple examples of publicly available libraries used by many web developers. 

<i>Which of the following best explains the difference between packages, modules, and libraries?</i>

<b>Library:</b> an independent collection of code that can be used by programs (not JS specific) - 

<b>Module:</b> JS code in a separate file, that can be required by other JS programs - 

<b>Package:</b> a collection of JS modules, with a package.json, usually published on NPM

<b> Dependencies in package.json </b>
The dependencies section of package.json lists the packages that need to be installed for the project to run properly. 

<b> node_modules</b> contains each installed package.

<b> package-lock.json</b> lists all the details about our project's dependencies. It should be checked into git, along with package.json

# Automated Testing
Automated testing is the practice of writing code to programmatically test the actual code we want to write.

benefits:
- it saves testing time (by not having to perform manual tests over and over)
- it saves debugging time (by catching bugs earlier)
- it makes it easier to program (because we don't need to keep the entire application in our heads, just the part that we're working on... if we break something, our tests will let us know)
- it makes it easier to come back to a program after some time (programmers forget things, but tests do not)
- it makes it easier to work together (we wrote some widget and know how it works, but our team-mates probably don't; our tests will catch bugs introduced by others on our team, and vice versa)
- it acts as documentation (readings tests is a great way to learn about how code is meant to be used)
- it improves the quality of our code (writing code that is easy to test often requires us to change how our code is structured -- for the better)

#### Type of Testing

1. Unit Testing - Unit testing is the practice of testing small pieces of code, typically individual functions, alone and isolated. 

    If your test uses some external resource, like the network or a database, it’s not a unit test.

2. Integration Testing -  Integration tests are similar to unit tests, but there’s one big difference: while unit tests are isolated from other components, integration tests are not. For example, a unit test for database access code would not talk to a real database, but an integration test would.

    Integration tests are often slower than unit tests because of the added complexity. They also might need some set up or configuration, such as the setting up of a test database. 

3. Functional Testing - Functional testing is also sometimes called E2E testing, or browser testing. They all refer to the same thing.

    Functional testing is defined as the testing of complete functionality of some application. In practice with web apps, this means using some tool to automate a browser, which is then used to click around on the pages to test the application.

#### Happy Path Testing

"Happy path" tests are very useful, because they catch the most critical bugs, but are definitely not sufficient for building reliable and robust applications.

# Unit Testing
is a magic button that tells us if our code is working. But instead of a button, it's a terminal command. And instead of magic, it's just `npm test`.

  Example:
  ```
  // Example of a simple function
  function largestNumber(array) {
    return array.reduce((previousValue, currentValue) => {  
      return Math.max(previousValue, currentValue);
    });
  }
  ```

  ```
  // Example of a test for that function
  const array = [1,2,3,4,5];
  const largest = largestNumber(array);
  assert.equal(largest, 5);
  ```

# Mocha and Chai

  mocha - testing framework
  chai - assertion library.

  Example:
  ```
  // code

  exports.isGroupValid = function (array) {
    if (array.length >= 6) {
      return false;
    } else if (array.length <=1) {
      return false;
    } else {
      return true;
    }
  };
  ```
  ```
  // test or validator

  const chai = require("chai");//import the chai library
  const assert = chai.expect; // establish a variable to be used in our tests
  const validator = require("../javascript/groupValidator"); // import the file where our function lives

  describe("The function groupValidator()", () => {
    it("should return true if there are between 2 and 5 group members", () => {
      assert(validator.isGroupValid(["a", "b", "c"])).to.be.true;
    }) 
  })
  ```

  Note:
  - The `it` line gives a description of the test, 
  - then runs a callback function. That function finds our validator file and then runs the groupValidator function inside with the parameters we pass it. Since we’re testing a group that should work, we’ve given it an array with three strings inside.

  As for assert and to.be.true, these logically declare what they’re doing. When we run the function isGroupValid() with an input of ["a", "b", "c"], we want chai to assert that the result that comes back is true.

  run `npm test`

  output:
  ```
    rus@Rusgyns-Air test % npm test 

  > unit_testing@1.0.0 test
  > ./node_modules/mocha/bin/mocha


    The function groupValidator()
      ✔ should return true if there are between 2 and 5 group members

    1 passing (3ms)
  ```


# Object Oriented

In object oriented programming, we use objects to group related variables and functions together to keep our code more organized.

Object-Oriented Programming is a way of writing code that encourages modularity and reduces duplication through the use of objects. It originated in the 1960s and became popular with C++ in the 1990s.

Here's a list of some programming languages that are predominantly OO:

- C++
- C#
- Java
- Python
- Ruby
- PHP
- Swift
- Objective-C

Here are some other languages that chose to use Functional Programming (FP), a different paradigm:

- Erlang
- Common Lisp
- Elixir
- Haskell
- Clojure

JavaScript has multiple paradigms; it initially popularized Functional Programming but was also object-oriented

Having multiple paradigms arguably makes a language more flexible and powerful, but also tends to cause confusion among its community. That said, in using JavaScript to learn OOP we have the benefit of learning OO in an evolutionary way. This is a luxury that most other languages don't support.

#### Conclusion

- OO is a software development paradigm
- OO is a popular way to solve code organization, re-use - and modularity
- OO is very important to learn due to its popularity
- JavaScript is not strictly OO in the way that Java or Ruby are
- Functional Programming is an alternative paradigm, and one that JavaScript also encourages

# Classes & Instances
In OOP, classes are blueprints (templates) that we use to create instances of objects. A class describes what the object is going to be and we can create new objects using the class.

#### Class
To declare a class, you use the class keyword with the name of the class.

```
//Class or blueprint

class Pizza {

}
```

- We can use any name for the class - Noun
- First letter always be capitalized

#### Object
To create a new object from a class, we use `new` keyword.

```
//Object or instances

let pizza1 = new Pizza();
let pizza2  = new Pizza();
```

`pizza1` and `pizza2` are pizza objects.
When you create an object using a class, it is an instance of that class.
So `pizza1` and `pizza2` are instances of the Pizza class.

## Methods and Properties

```
class Pizza {

  constructor() {
    this.toppings = ["cheese"];
  }

  addTopping(topping) {
    this.toppings.push(topping);
  }

}
```
Methods are the `constructor` and `addTopping`
Property is `topping`

```
//Method Syntax

class SomeClassName {
  methodName(parameters) {
    //thi is a method
  }
}
```


#### Introduction to `constructor`

<b>constructor</b> is a special kind of method that gets executed when an object instance is created from a class.

#### Customizing the construction

  Example:
  ```
  //CUSTOMIZING THE CONSTRUCTOR

  //Class or blueprint/template
  class Pizza {
    //constructor is a special kind of method that gets executed when an object instance (method) is created from a class
    constructor(size, crust, dough) {
      this.size = size;
      this.crust = crust;
      this.dough = dough;
      this.toppings = ['cheese']
      this.order = function() {
        return `Your order is a ${this.size} Pizza, with ${this.crust} crust, ${this.dough} dough, and toppings: ${this.toppings}`;
      };
    }
    //method
    addTopping(topping) {
      this.toppings.push(topping);
    }

  }

  //Object or instance
  let pizza = new Pizza('large', 'thin', 'wheat');
  pizza.addTopping('mushroom');
  console.log(pizza.order()); //=> Your order is a large Pizza, with thin crust, wheat dough, and toppings: cheese,mushroom

  //pizza Object its properties will look like this:
  /*
  let pizza = {
    size: 'large',
    crust: 'thin',
    dough: 'wheat'
    toppings: ['cheese'];
    order: function() {
      return `Your order is a ${this.size} Pizza, with ${this.crust} crust, ${this.dough} dough, and toppings: ${this.toppings}`
    }
  }
  */

  ```

#### Primitive as Objects:

Note:
```
typeof(true); 
// "boolean" 
typeof(Boolean(true)); 
// => "boolean" 
typeof(new Boolean(true));
// => "object"
```

== (type coercion vulnerable).
=== (strict comparative)

```
const greeting = "Hello, world!" 
const objGreeting = new String("Hello, world!");

greeting == objGreeting; 
// => true

greeting === objGreeting; 
// => false

```

## Conclusion
- The class syntax.
- The purpose of the new keyword and the concept of constructor functions.
- The difference between classes and instances.
- How we are able to create new object instances with and without class.

# Inheritance

Build a new class based on an existing class.
Duplication problem solution

if two classes have same constructor() then use inheritance.

```
//Duplication Problem
// Class Student and Class Mentor has same constructor

  class Student {
    // this constructor is identical to that of a mentor!
    constructor(name, quirkyFact) {
      this.name = name;
      this.quirkyFact = quirkyFact;
    }

    // here is a method that is specific to students
    enroll(cohort) {
      this.cohort = cohort;
    }

    // identical! Smells of code duplication
    bio() {
      return `My name is ${this.name} and here's my quirky fact: ${this.quirkyFact}`;
    }
  }

  class Mentor {
    // this constructor is identical to that of a student!
    constructor(name, quirkyFact) {
      this.name = name;
      this.quirkyFact = quirkyFact;
    }

    // specific to mentors
    goOnShift() {
      this.onShift = true;
    }

    // specific to mentors
    goOffShift() {
      this.onShift = false;
    }

    // identical! Smells of code duplication
    bio() {
      return `My name is ${this.name} and here's my quirky fact: ${this.quirkyFact}`;
    }
  }


```

Solution usng inheritance

```
//Inheritance

// This class represents all that is common between Student and Mentor
class Person {
  // moved here b/c it was identical
  constructor(name, quirkyFact) {
    this.name = name;
    this.quirkyFact = quirkyFact;
  }

  // moved here b/c it was identical
  bio() {
    return `My name is ${this.name} and here's my quirky fact: ${this.quirkyFact}`;
  }
}

```

```
class Student extends Person {
  // stays in Student class since it's specific to students only
  enroll(cohort) {
    this.cohort = cohort;
  }
}

class Mentor extends Person {
  // specific to mentors
  goOnShift() {
    this.onShift = true;
  }

  // specific to mentors
  goOffShift() {
    this.onShift = false;
  }
}
```
