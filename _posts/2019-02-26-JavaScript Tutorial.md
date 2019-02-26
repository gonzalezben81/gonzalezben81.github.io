## Elementary Javascript

**Remember Javascript is case sensitive**
Example: nostarch and noStarch will return different results if assigned improperly. 

### Comments in Javascript

Comment that is on the same line or on a line by itself.
````
//Comment
````
Comment that spans several lines:

````
/*
This is a comment in javascript
     that spans multiple lines
*/
````

### Datatypes in Javascript

#### Numbers:

Numbers are represented by their numeric expression just like in Math class. 

````
5;
6;
10;
100;
````

Mutliplaction, Addition, Division, and Subtraction
````
99 * 123; //Multiplication

9 + 9; //Addition

9/9; //Division

10-9; //Subtraction

2005 + 89 * 9 -6 /5; //Remember the Order of Operations matters in Javascript as well.
2804.8

//This can't be right!!!
8 / 1 + 3;
11

//This looks better!!!
8 / (1 + 3); //Keep an eye on things as you need to put certain things in parentheses. 
2


//This is wrong!!!
15 + 9 * 2;
33

//This is right!!!
(15 + 90) * 2; //Remember that parentheses matter in Javascript. 
33
````

#### Strings:

Strings are words that are contained in quotes in Javascript.

````
"This is a string";
"This, is another string that works!";
````

#### Boolean Expressions

What is a Boolean expression?
Answer: Simple true or false statements. 

These come back as a 0 or a 1 in computer language. 
````
true;
false;
TRUE; //This will error out
FALSE; //This will also error out
````

#### Assigning variables in Javascript


You create a variable in Javascript by assigning it first. You will want to use **var** and then your variable. Afterward you can change your variable by simply assinging a new value with it w/o using **var**.
````
var nick; //We did not define the variable properly
undefined

var age = 37; //Assign a number to a variable
age = 32; //Assigned a new number without calling var

var car = 'chevy'; //Assign a string to a variable
car = 'ford'; //Assigned a new string without calling var
````

#### Doing things with variables. 

You can multiple, concantenate, and do many other things with variables in Javascript. 

````
var secondsinaminute = 60; //seconds in a minute
var minutesinanhour = 60; //minutes in an hour
var secondsinanhour = secondsinaminute * minutesinanhour; //seconds in an hour
secondsinanhour; //the answer
````

#### Auto incrementing in Javascript
Sometimes you will need to auto-increment in Javascript. You want to continually count without having to reassing the variable. 
**++** increments by one

**--** decreases by one

````
var morePumpkins = 0;

//Increase
++morePumpkins; //Increase the number of pumpkins

++morePumpkins;
1

++morePumpkins;
2

//Decrease
--morePumpkins; //Decrease the number of pumpkins
1
--morePumpkins;
0
````

