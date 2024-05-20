# Week 1 - Day 1

## Gists and Template Repos

What's a Template Repo?
- Template repositories are regular GitHub repositories that are marked as templates. They allow you to create new repositories with the same directory structure, files, and commits as the original template repository.

What are Gists?
- A gist is just another git repository, except that its interface on GitHub's website is designed specifically for quickly and easily sharing code snippets.
- Gists cannot be given names - instead GitHub automatically assigns them a long, cryptic and unmemorable one.
- Gists come in two flavours: public and secret.
  - Public gists: Like public GitHub repos, these gists are searchable and discoverable by anyone.
  - Secret gists: These are neither searchable nor discoverable, but they're not private. They can be viewed by anyone but only as long as they know the gist's URL. This means that if you'd rather share your code snippets only with a few select people and not with the whole wide web, you should make them secret!

What's a Fork?
- A fork is a GitHub operation (not strictly a git command or feature) by which one GitHub user creates their own copy of another GitHub user's existing repository or gist.

Using Cloning and Template Repos
- While forking is used to create a copy of a repository on GitHub, cloning is used to create a copy of a repository on your local machine for local development.

## Linting and Eslint
Code Linting is one part of the solution towards writing maintainable, consistent code.

From any directory in our terminal, please run:

```shell
npm install -g eslint@8.57.0
```

Running eslint

```shell
eslint <file.name>
```

or

```shell
eslint .
```

## Command Line Args
Command line arguments are strings of text used to pass additional information to a program when an application is run through the command line interface (CLI) of an operating system. Command line arguments typically include information used to set configuration or property values for an application.

syntax:

```
$ [runtime] [script_name] [argument-1 argument-2 argument-3 ... argument-n]
```

Why use Command Line Arguments?

* Advantage
  * You can pass information to an application before it starts. 
  * Command line arguments are passed as strings to your program
  * You can pass an unlimited number of arguments via the command line.
  * Command line arguments are used in conjunction with scripts and batch files, which is particularly useful for automated testing.

* Disadvantage
  * the interface has a steep learning curve, so it's difficult for most people to use unless they have a good deal of experience using CLI tools.
  * an be difficult to use unless you're using a desktop or laptop computer, so they're not typically used on smaller devices like phones or tablets.

To run:
The simplest way of retrieving arguments in Node.js is via the process.argv array.

```
$ node processargv.js tom jack 43
```

Here we are passing three arguments to the processargv.js program. 
2nd index = "tom"
3rd index = "jack"
4th index = "43"

The output should look something like this:

```
$ node processargv.js tom jack 43
0 -> /Users/scott/.nvm/versions/node/v4.8.0/bin/node
1 -> /Users/scott/javascript/processargv.js
2 -> tom
3 -> jack
4 -> 43
```

0 index = path to our node executable
1st index = contains the path to the script file
rest = are arguments

## Console: assert()
The console.assert() static method writes an error message to the console if the assertion is false. If the assertion is true, nothing happens.

> #### Instruction
> Try out console.assert in the node REPL

```shell
node 
console.assert(1 === 1); // => nothing happens because true
console.assert (1 === 1.1); // => print outs "Assertion failed" to the terminal
```
We could use this to test 

```shell
// FUNCTION IMPLEMENTATION
const sum = function (a, b) {
  return a + b;
};

// TEST CODE
console.assert(sum(1, 2) === 3);
console.assert(sum(1, 20) === 3); // bad / incorrect assertion, and we see it fail!
```

```shell
// FUNCTION IMPLEMENTATION
const sumBuggy = function (a, b) {
  return a * b;
};

// TEST CODE
console.assert(sumBuggy(1, 2) === 3); // fails, because bug!
```

The console.assert function prints to the console for us, the developer, when an expected outcome is not met (fails) so that we can look into why.

## ES6 - Template Literals
also known as Template Strings.

```shell
const name1 = 'Gabrielle Kaye';
const name2 = 'Dean Aurelius';
console.log(`Hello, ${name1} and ${name2}!`);
```
output:
```
Hello, Gabrielle Kaye and Dean Aurelius!
```
## Function

Conventions for naming a functions:
- avoid generic names like 'data', or 'run'.
- name your functions beginning with action words like createUser, or sendUserData.
- be consistent with your naming conventions.
- if you're joining an existing project, observe and adapt any existing conventions.

Following best practices when creating functions:

1. Give your functions precise verb/action based names
2. Use camelCasedNames (like this one)
3. Properly indent the function code
4. Functions should focus on a single task: returning a value or causing a side effect. Break your function into additional smaller functions if you find it doing two or more things.
  - One single task could be to compute and return a value (eg: zeroPad)
  - Another single task could be to perform a side effect such as logging a message to the screen (eg: printFarmInventory)
5. Data needed by Functions should be passed in as parameters/arguments (i.e. local scope) instead of being accessed directly

## Javascript scope
1. Global-scope - variable is available everywhere in the code
2. local-scope - variable would only be available within the function in which it's defined.

  Example:
  ```
    let myGlobalVar = "global";

    const printMyVars = function() {
      let myLocalVar = "local";
      console.log("-- Inside printMyVars --");
      console.log("myLocalVar is:", myLocalVar);
      console.log("myGlobalVar is:", myGlobalVar);
    }

    printMyVars();

    console.log('-- Outside of printMyVars now --');
    console.log(myLocalVar);
  ```

  Output:

  ```
  -- Inside printMyVars --
  myLocalVar is: local
  myGlobalVar is: global
  -- Outside of printMyVars now --
  /Users/rus/lighthouse/lotide/tail.js:52
  console.log(myLocalVar);
              ^

  ReferenceError: myLocalVar is not defined
  ```
## Coercion and TruthyFalsey
The === does not only compare two values, but also the type of those values

  Example:
  ```
  23 === '23'
  ```
  Output:
  ```
  False
  ```
  Even though both of the above values are 23, one is a String and the other is a Number. Before comparing the actual values, === will compare the types, see that they are not the same, and immediately return False without going any further.

The == operator will attempt to force the two values to be of the same type, if possible. This is called type coercion, and it can really mess up your expected results if you're not careful. 

  Example:
  ```
  23 == '23'
  ```
  Output:
  ```
  True
  ```

## Iteration using for..of or for..in

Difference between for...of and for...in
The main difference between them is in what they iterate over. The for...in statement iterates over the enumerable string properties of an object, while the for...of statement iterates over values that the iterable object defines to be iterated over.

> for...of
>
> For arrays, a regular for loop or for...of loop is usually a safer choice.

loop operates on the values sourced from an iterable one by one in sequential order. Each operation of the loop on a value is called an iteration, and the loop is said to iterate over the iterable. Each iteration executes statements that may refer to the current sequence value.

  Example:
  ```
    const array1 = ['a', 'b', 'c'];

    for (const element of array1) {
      console.log(element);
    }

    // Expected output: "a"
    // Expected output: "b"
    // Expected output: "c"
  ```

> for..in
>
> it's generally recommended to use for...in with objects, not arrays. 

statement iterates over all enumerable string properties of an object (ignoring properties keyed by symbols), including inherited enumerable properties.

  Example:
  ```
  const object = { a: 1, b: 2, c: 3 };

  for (const property in object) {
    console.log(`${property}: ${object[property]}`);
  }

  // Expected output:
  // "a: 1"
  // "b: 2"
  // "c: 3"
```




