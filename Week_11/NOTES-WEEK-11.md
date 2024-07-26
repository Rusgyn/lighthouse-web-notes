# Visualizing Database

ERD - Entity Relationship Diagram.
- Graphical representation of a database.
- visualizes the relationships between entities like people, things, or concepts in a database

ERD

1. Entity - Represents a person, place, or thing that you want to track in a database. Table e.g. Students

Entity instance - this will be each record or "row" in a table. E.g. Each Individual student, Single student is an instance of Entity students.

2. Attribute - Describes various characteristics about an individual entity.
Columns in the table. 
e.g. First Name of a student

3. Primary Key - attribute or group of attributes tht uniquely identifies an instance of the entity. e.g. ID

Foreign Key -

5. Relationship - Describe how one or more entities interact with each other.

A verb is often used to describe the relationship.

6. Cardinality - The count of instances that are allowed or are necessary between entity relationships. Crows foot notation. 

This is the link that connects the entities.
One - Mandatory = Must have at least one instance
Many Mandatory
One - Optional
Mamy - Optional

One (|) and Many (crow's feet)refers to minimum
Optional (o) and Mandatory (||) means to maximum.

# SQL INTRO

1. You can use WHERE name LIKE 'B%' to find the countries that start with "B".

The % is a wild-card it can match any characters

```
\\Find the country that start with Y

SELECT name FROM world
  WHERE name LIKE 'Y%';
```

```
\\Find the countries that end with y

SELECT name FROM world
  WHERE name LIKE '%y';
  ```

```
\\ Luxembourg has an x - so does one other country. List them both.

Find the countries that contain the letter x

SELECT name FROM world
  WHERE name LIKE '%x%';
```

```
\\Iceland, Switzerland end with land - but are there others?

Find the countries that end with land

SELECT name FROM world
  WHERE name LIKE '%land';
```

```
\\Columbia starts with a C and ends with ia - there are two more like this.

Find the countries that start with C and end with ia

SELECT name FROM world
  WHERE name LIKE 'C%ia%';
```

```
\\Greece has a double e - who has a double o?

Find the country that has oo in the name

SELECT name FROM world
  WHERE name LIKE '%oo%'
```

```
\\Bahamas has three a - who else?

Find the countries that have three or more a in the name

SELECT name FROM world
  WHERE name LIKE '%a%a%a%';
```

```
\\Find the countries that have "t" as the second character.

SELECT name FROM world
 WHERE name LIKE '_t%'
ORDER BY name;
```

```
\\Lesotho and Moldova both have two o characters separated by two other characters.

Find the countries that have two "o" characters separated by two others.

SELECT name FROM world
 WHERE name LIKE '%o__o%';
```

```
\\Cuba and Togo have four characters names.

Find the countries that have exactly four characters.

SELECT name FROM world
 WHERE name LIKE '____';
```

```
\\The capital of Luxembourg is Luxembourg. Show all the countries where the capital is the same as the name of the country

Find the country where the name is the capital city.

SELECT name
  FROM world
 WHERE name = capital;
```

```
\\The capital of Mexico is Mexico City. Show all the countries where the capital has the country together with the word "City".

Find the country where the capital is the country plus "City".

SELECT name
  FROM world
 WHERE capital LIKE concat(name, ' City');
```

```
\\Find the capital and the name where the capital includes the name of the country.

SELECT capital, name
  FROM world
WHERE capital LIKE concat(name, ' %')
OR capital LIKE name;
```

```
\\The capital of Monaco is Monaco-Ville: this is the name Monaco and the extension is -Ville.

Show the name and the extension where the capital is a proper (non-empty) extension of name of the country.

You can use the SQL function REPLACE.

REPLACE('vessel','e','a');
-> 'vassal'

SELECT name,
 replace(capital, name, '')
FROM world
WHERE capital LIKE concat(name, ' %');
```

```
\\Give the name and the per capita GDP for those countries with a population of at least 200 million.

SELECT name, gdp/population
 FROM world
WHERE population >= 200000000;
```

```
\\Show the name and population in millions for the countries of the continent 'South America'. Divide the population by 1000000 to get population in millions.

SELECT name, population/1000000
FROM world
WHERE continent LIKE 'South America';
```

```
\\Show the name and population for France, Germany, Italy

SELECT name, population
FROM world
WHERE name IN ('France', 'Germany', 'Italy');
```

```
\\Two ways to be big: A country is big if it has an area of more than 3 million sq km or it has a population of more than 250 million.

Show the countries that are big by area or big by population. Show name, population and area.

SELECT name, population, area
FROM world
WHERE population >= 250000000
OR area >= 3000000
```

```
\\Exclusive OR (XOR). Show the countries that are big by area (more than 3 million) or big by population (more than 250 million) but not both. Show name, population and area.

Australia has a big area but a small population, it should be included.
Indonesia has a big population but a small area, it should be included.
China has a big population and big area, it should be excluded.
United Kingdom has a small population and a small area, it should be excluded.

SELECT name, population, area
FROM world
WHERE population >= 250000000
XOR area >= 3000000
```

```
\\Show the name and population in millions and the GDP in billions for the countries of the continent 'South America'. Use the ROUND function to show the values to two decimal places.

For Americas show population in millions and GDP in billions both to 2 decimal places.

ROUND(7253.86, 0)    ->  7254
ROUND(7253.86, 1)    ->  7253.9
ROUND(7253.86,-3)    ->  7000

SELECT name,
ROUND(population/1000000, 2) as population, 
ROUND(gdp/1000000000 , 2) as gdp
FROM world
WHERE continent = 'South America';
```

```
\\Show the name and per-capita GDP for those countries with a GDP of at least one trillion (1000000000000; that is 12 zeros). Round this value to the nearest 1000.

Show per-capita GDP for the trillion dollar countries to the nearest $1000.

SELECT name, 
ROUND((gdp/population), -3) as 'per-capita GDP'
FROM world
WHERE GDP >= 1000000000000;
```

```
\\Greece has capital Athens.

Each of the strings 'Greece', and 'Athens' has 6 characters.

Show the name and capital where the name and the capital have the same number of characters.

LENGTH('Hello') -> 5 

SELECT name, capital
FROM world
WHERE LENGTH(name) = LENGTH(capital);
```

```
\\The capital of Sweden is Stockholm. Both words start with the letter 'S'.

Show the name and the capital where the first letters of each match. Don't include countries where the name and the capital are the same word.

You can use the function LEFT to isolate the first character.
You can use <> as the NOT EQUALS operator.

 LEFT('Hello world', 4) -> 'Hell'     

SELECT name, capital
FROM world
WHERE LEFT(name,1) = LEFT(capital,1)
AND name <> capital;
```

```
\\Equatorial Guinea and Dominican Republic have all of the vowels (a e i o u) in the name. They don't count because they have more than one word in the name.

Find the country that has all the vowels and no spaces in its name.

You can use the phrase name NOT LIKE '%a%' to exclude characters from your results.
The query shown misses countries like Bahamas and Belarus because they contain at least one 'a'

SELECT name
   FROM world
WHERE name LIKE '%a%' 
  and name LIKE '%e%' 
  and name LIKE '%i%' 
  and name LIKE '%o%'
  and name LIKE '%u%'
  and name NOT LIKE '% %';
```

# PSQL setup

## Start
```
brew services start postgresql
```

## Stop
```
brew services stop postgresql
```

## Create database
```
CREATE DATABASE test_db
```

## CREATE ROLE / USER
```
\\SuperUser. In real world, avoid using Superuser.

CREATE ROLE 'development' LOGIN SUPERUSER PASSWORD 'development';
```

```
\\Normal User

CREATE ROLE 'labber' LOGIN PASSWORD 'labber';
```

# LOGIN to PSQL
```
psql
```

## CHANGE DBASE and USER
```
\\Syntax:
\c <DBASE NAME> <USERNAME>

\c test_db labber
```

## CHECK EXISTING ENTITY
```
\dt
```

## CREATE TABLE
```
\\SYNTAX: CREATE TABLE <TABLE NAME> (property)

CREATE TABLE famous_people (
  id SERIAL PRIMARY KEY,
  first_name VARCHAR(50),
  last_name VARCHAR(50),
  birthdate DATE
);
```

## DELETE TABLE
```
//SYNTAX: DROP TABLE <property name/ entity>;

DROP TABLE famous_people;
```

## INSERT SOME DATA
```
//SYNTAX: INSERT INTO <database name> (properties);

INSERT INTO famous_people (first_name, last_name, birthdate)
  VALUES ('Abraham', 'Lincoln', '1809-02-12');

INSERT INTO famous_people (first_name, last_name, birthdate)
  VALUES ('Mahatma', 'Gandhi', '1869-10-02');
```

# GENERATE DBASE DATA

* Select all columns for all rows in the famous_people table.

```
SELECT * FROM famous_people; 
```

* Only return people with a birthday on or after '1920-01-01'.
```
SELECT * FROM famous_people WHERE birthdate >= '1920-01-01';
```

* Only return people with a birthday before '1920-01-01'.
```
SELECT * FROM famous_people WHERE birthdate < '1920-01-01';
```

* Select the total number of people in the famous_people table.
```
SELECT count(*) FROM famous_people;
```