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

