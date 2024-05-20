# Javascript Objects

1. Which of the following is not a primitive data type in JavaScript?
Array

Correct, arrays are a type of Object in JavaScript, not a primitive

2. Which of the following is a valid way to access an object value? (Multiple correct)
myObject['key']

Correct, you can access object values using square bracket notation

myObject.key

Correct, you can access values using .key notation

3. Are primitive data types the same across most programming languages?

No, primitives are a defining feature of a programming language

Correct, primitives are similar, but often unique to a given programming language

4. Is the following code a valid Object in JavaScript?
```
var myObjected = {
'key-1': 42,
keyB: 'value B',
'keyC': [1, 2, 3]
};
```

Yes, although the keys could be defined more consistently

Correct, the object would work despite inconsistent key definitions

5. Given the following object, how would you access the first borough, Manhattan (using JavaScript)?

```
var nyc = {
  name: 'New York City',
  boroughs: [
    'Manhattan',
    'Queens',
    'Brooklyn',
    'The Bronx',
    'Staten Island'],
  population: 8491079,
  area_codes: [212, 347, 646, 718, 917, 929],
  position: { lat: 40.7127, lng: -74.0059 }
}
```

nyc['boroughs'][0]

Correct, this would return the first element of the boroughs array
