# NOTES-WEEK-4

# Asynchronous Control Flow

Javascript is always synchronous. JavaScript is synchronous, blocking and single-threaded. This means that the JavaScript engine executes our program sequentially, one line at a time from top to bottom in the exact order of the statements

for loop, foreach, for...in, for...of are synchronous

In JavaScript, code has to wait for the previous lines of code to finish, but these can take time to execute. The solution is to multitask using asynchronous control flow. In the next activities, you'll get comfortable with asynchronous control flow.

JavaScript has a few parts that work together to facilitate multitasking:
- the Call Stack,
- the Web APIs,
- the Callback Queue, and then
- the Event Loop.

Function calls always execute right away. But the setTimeout method schedules a callback for later execution on the event loop.
The main thread has to finish first before the event loop can even start!

We use callbacks when we are writing asynchronous code, but it also helps with modularity. We now know that callback chaining means writing nested callback functions.

## Using asynchronous functions

  Example:
  ```
  //Input

  const fs = require('fs');
  console.log('Starting main thread');

  const intervalreference = setInterval(() => {
    process.stdout.write('.'); //process.stdout.write - write in the console
  }, 30);

  const whenDoneReading = (error, data) => {
    if (errpr) {
      console.log('error', error);
      return;
    }

    clearInterval(intervalReference);
    console.log();
    console.log('file read successfully');
    console.log('Data Sample: ', data.slice(0, 50)); //
  };

  fs.readFile('large-test-file.txt', 'utf8', whenDoneReading);

  console.log('EndingMain Thread');
  ```

  Output
      Remember: The main thread has to finish first before the event loop can even start!
  ```
  //Output

  Staring main thread
  Ending Main Thread
  .......................
  file read successfully
  Data Sample: 3HRGRTaJ2d0khK1Som4PMHznJ2ILgx1XDizP9s2
  ```

Other examples of how asynchronous functions might be used include:
- Making a network API request
- Connecting to a chat server
- Anything that takes time and where we want users to know that the code is still running, like showing a basic loading animation

# OOP Part3: Super

## Method overriding and Super
Method Overriding - When a subclass implements a method hat already exists in the superclass.
Super - 

Example:

  Problem - <i>Sometimes you want a subclass to have similar but slightly different behaviour to its superclass. In our scenario, what if we want all mentor bios to start with "I'm a mentor at Lighthouse Labs." before saying the "My name is ..." bit?</i>
  
  #### Solution 1: Method Override -  When a subclass implements a method hat already exists in the superclass.

  ```
  // Superclass
    class Person {
      constructor(name, quirkyFact) {
        this.name = name;
        this.quirkyFact = quirkyFact;
      }

      bio() {
        return `My name is ${this.name} and here's my quirky fact: ${this.quirkyFact}`;
      }
    }

    // Subclass
    class Mentor extends Person {
      // Completely re-define the bio method since it has more to say
      bio() {
        return `I'm a mentor at Lighthouse Labs. My name is ${this.name} and here's my quirky fact: ${this.quirkyFact}`;
      }
    }

    // The Student class doesn't need to define bio since it can just use the one from Person

    // DRIVER CODE

    const bob = new Mentor('Bob Ross', 'I like mountains way too much');
    console.log(bob.bio());
  ```

  #### Solution Part 2: User super - Using super allows us to access the superclass, plain and simple.

  ```
    // Super class
    class Person {
      constructor(name, quirkyFact) {
        this.name = name;
        this.quirkyFact = quirkyFact;
      }

      bio() {
        return `My name is ${this.name} and here's my quirky fact: ${this.quirkyFact}`;
      }
    }

    class Mentor extends Person {
      // Mentor bios need to include a bit more info
      bio() {
        return `I'm a mentor at Lighthouse Labs. ${super.bio()}`;
      }
    }

    // DRIVER CODE

    const bob = new Mentor('Bob Ross', 'I like mountains way too much');
    console.log(bob.bio());
  ```

## Conclusion

1. Overriding methods in subclasses to change their behaviour. Sometimes this is all you need, but other times we end up repeating some things in the overriding methods. That brings us to point 2 below.
2. Using `super` in the overriding methods in order to avoid repeating code that's already present in the superclass.

# OOP Part 4: Getters and Setters
Getters and setters are special methods that are used to get the value of a property or set the value of a property.

There are many reasons you might want to use getters and setters in your app.

Let's go over two main reasons right now:

1. Validating data before assigning it to a property
2. Computing a value on the fly instead of simply pulling it out of a property

## Conclusion
 Setters allow us to validate data before assigning it to a property and getters allow us to compute a value on the fly instead of simply pulling it out of a property. The get and set keywords just make our object's interface more simple.

# OOP Goals and Practices
simpler to read, write and maintain.
## OOP Goals
- Reduce duplicated code (reusability)
- Breaking code up into sensibly-divided units (modularity)

We use OOP to help modularize our code. Sometimes it's the best option for a project and sometimes it isn't but modularization is the reason we use it.

## Abstraction
Abstraction is a technique for arranging complexity of computer systems. It works by establishing a level of complexity on which a person interacts with the system, suppressing the more complex details below the current level.

Abstraction involves hiding the inner workings of an object in favor of exposing a simple interface to that object.
  Example: the interface to a car is the steering wheel and pedals and doesn't expose how the engine works.

Abstraction makes it easy to change how an object works internally without having to change the code that uses the object.
  Example: Exposing a method that adds toppings to a pizza makes it easy to change the way we store toppings inside the pizza object.

Abstraction requires us to initially write more code to separate an object's interface from it's implementation.
  Example: Abstraction usually requires us to write even more code up front, but we write less code every time we use the object.

## Single Responsibility Principe

The single responsibility principle states that a class should be responsible for a single part of the app's functionality, giving it only one reason to change. Or more simply, a class should only have one job

Any class should only be responsible for a single part of the app's functionality.

  Example:
  ```
  // Manage the state of a task
  class Task {
    complete() {
      // Mark this task as complete
    }
  }

  class NotificationManager {
    sendNotification(task) {
      // Send a notification to the user that their task is complete
    }
  }

  class DatabaseManager {
    saveToDatabase(task) {
      // Save this task to the database
    }
  }

  let task = new Task();
  databaseManager.saveToDatabase(task);
  task.complete();
  notificationManager.sendNotification(task);
  databaseManager.saveToDatabase(task);
  ```

# Conclusion

Object Oriented Programming (OOP) is a programming paradigm where we use objects to encapsulate (group) data and behaviour. 

Why do we do this? What's it all for?

To reduce duplicated code (reusability)
To break code up into sensibly-divided units (modularity)

OOP by itself does not require the use of classes.

Summary of OOP features that we covered:
We learned the following features about Classical OOP:

1. A class is a blueprint from which instances of objects can be created (i.e. newTask vs a task)
2. Classes have data in the form of value properties and behaviour in the form of methods
3. Classes can inherit behaviour from other classes using the extends keyword
4. Subclasses can override methods that are inherited in their superclass
5. JavaScript also gives us get and set keywords to more cleverly define methods that are data getters and setters

# Mocha and Chai

### Mocha 
- gives us the describe and it functions. Each it is a test, and each test should have at least one assertion.
- Framework
- JavaScript test framework running on Node.js and in the browser, making asynchronous testing simple and fun.

### Chai
- is an assertion library. Chai assertion functions are deliberately designed to play nice with testing frameworks like Mocha.
- Library

Note:
use `npm test` to run the code testing.

- gives us `assert.deepEqual` to compare objects and arrays.

- `assert.strictEqual` simply uses `===` to compare values.

# setTimeout Introduction


<b>setTimeout</b> is used to delay the execution of some code to later. We specify the code via a callback, and the delay in ms.

The setTimeout function can actually take in more parameters, and isn't limited to just two. However, for our purposes, this simplified view of it is acceptable.

`setTimeout(callback, delay)`

  Example:
  ```
  console.log('first line');
  setTimeout(() => {
    console.log('timeout line');
  }, 1000);
  console.log('last line');
  ```
  ```
  //OUTPUT
  first line
  last line
  timeout line
  ```

### What's Used For?
1. Some sites will show a notice to the user and then automatically hide it after a few seconds. That's accomplished via setTimeout
2. In Gmail or other web-based email clients, a yellow "disconnected" message popus up at the top if we go offline. It usually indicates that it will retry to connect after x seconds. This countdown and its retry is implemented using setTimeout.
3. Some websites like to pop open an in-browser chat button after a few seconds. setTimeout is used to make them appear with a short delay.
4. If you use an Adblocker browser extension, you've likely seen prompts from websites asking us to disable them for that site. These don't come up right away and instead are delayed by a few seconds. The delay here would be implemented using setTimeout.


### Goals
Due to its simplicity, setTimeout is also a great way to learn about handling delays caused by heavy operations such as reading/writing files or downloading/uploading content.

### Summary

- The setTimeout function is used to defer code execution by a specified number of milliseconds
- A callback is passed in to setTimeout and setTimeout calls it after x ms
- It's used on many websites to delay a message or response
- We are learning about it for purposes of practicing async programming in JS

# Asynch JS
# Event handing and User Input

callbacks are a major way that JavaScript handles dealing with code that needs to run later.

  ```
  const stdin = process.stdin;

  stdin.setRawMode(true);
  stdin.setEncoding("utf8");

  // Event handling for user input

  // on any input from stdin,output a "$" to stdout
  stdin.on("data", (key) => { //"stdin" standard input. //.om method to register a callback to read user input
    // \u0003 maps to ctrl+c input - to exit/stop.
    if (key === "\u0003") {
      process.exit();
    }
    
    process.stdout.write("$"); // "stdout" standard output

  });

  console.log("after callback");
  ```

  Output:
  ```
    after callback
    $$$$$$$$$$$$$$$$$$$$$$$$% 

  ```

### Events in General

User events are a relatable way to get introduced to the concept of events. Not all event handling is due to direct user input.

## Conclusion

This interactive reading introduces the idea of events and how JavaScript uses callbacks as the strategy to handle their asynchronous nature. For our initial example, we looked at Node's `process.stdin` object and used `on` to register a callback to read user input. In later exercises, we'll now expect you to use this technique to create fun little solutions.


# Asynchronous Return Values

## Synchronous Function
With synchronous functions, we can simply return a value.

```
    // data in memory
    const catBreeds = {
      'Balinese': "Balinese are curious, outgoing, intelligent cats with excellent communication skills. They are known for their chatty personalities and are always eager to tell you their views on life, love, and what you’ve served them for dinner.",
      'Bombay': "The golden eyes and the shiny black coat of the Bombay is absolutely striking. Likely to bond most with one family member, the Bombay will follow you from room to room and will almost always have something to say about what you are doing, loving attention and to be carried around, often on his caregiver's shoulder."
    };

    // synchronous function to fetch a cat breed
    const breedDetails = function(breed) {
      // can simply return it (easy peezee, butter squeezy) ...
      return catBreeds[breed];
    };

    // get the return value right away from the function
    const bombay = breedDetails('Bombay');
    console.log(bombay); //=> prints out the description for that breed
```

## Asynchronous Functions cant return data
Instead of using return data, we would have to modify our function to give back the data without using return. If you want to see the data output you can use callback(data) or console.log(data).

```
    // asyncBreeds.js
    const fs = require('fs');

    const breedDetailsFromFile = function(breed) {
      console.log('breedDetailsFromFile: Calling readFile...');
      fs.readFile(`./data/${breed}.txt`, 'utf8', (error, data) => {
        console.log("In readFile's Callback: it has the data.");
        // ISSUE: Returning from *inner* callback function, not breedDetailsFromFile.
        if (!error) return data;
      });
      // ISSUE: Attempting to return data out here will also not work.
      //        Currently not returning anything from here, so breedDetailsFromFile function returns undefined.
    };

    // we try to get the return value
    const bombay = breedDetailsFromFile('Bombay');
    console.log('Return Value: ', bombay); // => will NOT print out details, instead we will see undefined!
    Warning

```

  Output:

  ```
  breedDetailsFromFile: Calling readFile...
  Return Value:  undefined
  In readFile's Callback: it has the data.
  ```

  take note asynchronouse js do not return value hence use callback if you want to see the data
  modify the example line 367 to below

  ```
   if (!error) callback(data); // previous was  `if (!error) return data;`
  ```
  modified function will be:

  ```
      // asyncBreeds.js
      const fs = require('fs');

      const breedDetailsFromFile = function(breed, callback) {
        console.log('breedDetailsFromFile: Calling readFile...');
        fs.readFile(`./data/${breed}.txt`, 'utf8', (error, data) => {
          console.log("In readFile's Callback: it has the data.");
          // ISSUE: Returning from *inner* callback function, not breedDetailsFromFile.
          if (!error) {
            callback(data);
          }
          else if (error) console.log("WRONG")
        });
        // ISSUE: Attempting to return data out here will also not work.
        //        Currently not returning anything from here, so breedDetailsFromFile function returns undefined.
      };
      const callback = function(data) {
        console.log("The dat is: ", data);
      }

      // we try to get the return value
      const bombay = breedDetailsFromFile('bombay', callback);
      console.log('Return Value: ', bombay); // => will NOT print out details, instead we will see undefined!

  ```

  output after modification

  ```
  breedDetailsFromFile: Calling readFile...
  Return Value:  undefined
  In readFile's Callback: it has the data.
  "The golden eyes and the shiny black coat of the Bombay is absolutely striking. Likely to bond most with one family member, the Bombay will follow you from room to room and will almost always have something to say about what you are doing, loving attention and to be carried around, often on his caregiver's shoulder."
  ```

## Conclusion
We saw why and how asynchronous functions such as readFile, and our function breedDetailsFromFile, cannot simply return their data. Instead they must use callback functions to pass that data back.
