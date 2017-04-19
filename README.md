# ES6_features

> **LET**

- Use the keyword let in place of var in most cases
- With var there is a lot of scoping issues
- Whenever you declare a variable using the keyword let that variable is accessible from the same block {}

```JavaScript
function theNotebook() {
	let movie = ‘The Notebook’;
	return movie;
       }
console.log(theNotebook());
RESULT: The Notebook

console.log(movie);

RESULT: 
Error as the movie variable is not accessible from outside this block
```


If you then add variable outside the block statement it will access what is essentially a global variable.

```Javascript
let movie = ‘Legally Blonde’;

function theNotebook() {
	let movie = ‘The Notebook’;
	return movie;
       }

console.log(theNotebook());
RESULT: The Notebook

console.log(movie);

RESULT: 
Legally Blonde

```


If you remove the movie variable in the block. It kind of works like a family tree so it will see there is no movie in the block scope so it will look outside the scope to the next one.```
console.log(theNotebook());
RESULT: Legally Blonde```

```JavaScript
let movie = ‘Legally Blonde’;

function theNotebook() {
	return movie;
       }

console.log(theNotebook());
RESULT: Legally Blonde

console.log(movie);
RESULT: Legally Blonde
```

First two are defined within blocks and so are constricted to those blocks. Whereas the third console was unrestricted and so it will look at the parent element which with would be same to Before if as it was not closed.

```JavaScript
function asmaFunction() {
	let isDog = true;
	let response = ‘You can have a dog’;
	console.log(‘Before if:’ , response);
 if (isDog) {
	let response = “You can’t have a dog”;
	console.log(‘Inside if:’ , response);
} 
	console.log(‘After if:’, response
}

asmaFunction();

RESULT:
Before if: You can have a dog
Inside if: You can’t have a dog
After if: You can have a dog
```
________________________________

> **CONST**

As mentioned above with ES6 we should avoid using the word variable whenever possible.

Now we have the ability of making a constant with const.
Anytime you want to have a variable where the value never changes use const.
This prevents you from accidentally assigning another value to this variable.


Instead of ```var PI = 3.14;```

Use ```const PI = 3.14;```

__________________________

> **ARROW FUNCTIONS**

The arrow function is essentially where you can leave out the word function and instead use =>

Arrow functions have lexical scope, being the parent scope

```JavaScript
function circleArea1(r) {
	var PI = 3.14;
	return PI * r * r;
}
```

Instead,
```JavaScript
let circleArea2 = (r) => {
	const PI = 3.14;
	return PI * r * r;
};
```


Alternatively,
```JavaScript
let circleArea3 = r => 3.14 * r * r;
```

Anytime you have one parameter you could just write the parameter without the parentheses(). It also goes for whenever you are returning a value directly and you don’t need multiple statements. We’ve lost the ```return``` keyword because when omitting {}, single line arrow functions perform an implicit return.


**Lexical scope of arrow functions**

Where arrow functions are going to be tricky is with the ```this``` keyword.

```JavaScript
let person = {
name: ‘Asma’,
sayName: function() {
	console.log(`Hi I am ${this.name}`);
 }
}
person.sayName();

RESULT: 
“Hi I am Asma”
```

By default when you have an object, any method on that  this keyword of a set method will be bound to the object.

If you replaced the function keyword ```this``` with an arrow.  Error cannot read property name of undefined will appear.

Arrow functions have lexical scope. Lexical scope being as parent scope. So in the case of an arrow function the scope is not going to be our object, its going to be whatever  that this keyword was referred to before that. In the above case its going to be something like the window. 

```JavaScript
let person = {
name: ‘Asma’,
hobbies: [‘Reading’ , “Computers’, ’Internet’],
showHobbies: function() {
this.hobbies.forEach(function(hobby) {
console.log(`${this.name} lies ${hobby} ‘)
  });
 }
}

person.showHobbies();

RESULT:
“JS Bin Output likes Reading”
“JS Bin Output likes Computers”
“JS Bin Output likes Internet”
```

Our ```${this.name}``` function inside our foreach function is no longer referring to person. ```this.hobbies``` refers to ```person.hobbies``` but the binding of ```this.name``` has changed. However, if we want it to change to be parent scope, that person object we change it to be an arrow function.

Instead,

```JavaScript
let person = {
name: ‘Asma’,
hobbies: [‘Reading’ , “Computers’, ’Internet’],
showHobbies: function() {
this.hobbies.forEach((hobby)  => {
console.log(`${this.name} lies ${hobby} ‘)
  });
 }
}

person.showHobbies();

RESULT:
“Asma likes Reading”
“Asma likes Computers”
“Asma likes Internet”
```


____________________________________

> **TEMPLATE LITERALS**


Before

```JavaScript
let name = ‘Asma’;

console.log(“My favourite person is” + name + “because she’s funny”);

RESULT:
My favourite person is Asma because she’s funny
```


Instead,

```JavaScript
let name = ‘Asma’;

console.log(`My favourite person is ${name} because she’s funny`);

RESULT:
My favourite person is Asma because she’s funny
```

Ensure you are using back ticks `` instead of single quotes ‘’.



You can also do this although its not good practice to because you usually want to separate your logic from your formatting. It better to make another result variable.

```JavaScript
let a = 5;
let b = 7;

console.log(`result ${a + b}`);

RESULT:
result 12
```

 
Another feature of template literals is that it can interpret a new line.

```JavaScript
let name = ‘Asma’;

console.log(`My favourite person is ${name} 
because she’s funny`);

RESULT:
My favourite person is Asma 
because she’s funny
```

_____________________________________________

> **SPREAD OPERATOR**

Before

```JavaScript
function addNumbers(a, b, c){
console.log( a +b + c);
}

var nums = [3, 4, 5];

addNumbers(nums[0], nums[1], nums[2]);

RESULT:
12
```

Now we can do three dots and the name of the expression or the array.

```JavaScript
function addNumbers(a, b, c){
console.log( a +b + c);
}

var nums = [3, 4, 5];

addNumbers(…nums);

RESULT:
12
```


You also add arrays easily on without doing push etc. For instance 

```JavaScript
var meats = [‘beef’ , ‘chicken’];
var food = [‘fish’, …meats,  ‘veg’];
console.log(food);

RESULT:
fish, beef, chicken, veg
```
__________________________________________

> **CLASSES**

A class in terms of OOP is a blueprint for creating objects. A class encapsulates data for the object.

You are going to create a class whenever you need a piece of code to be self-aware or remember something. ES6 classes just makes the syntax cleaner and easier to use.

Classes can be included in the code either by declaring them or by using class expressions.

```JavaScript
class person {

 constructor(name, age, weight){
	this.name = name;
	this.age = age;
	this.weight = weight;

displayWeight() {
	console.log(this.weight);
}

let asma = new Person(‘Asma’, 23, 55);
let ellie = new Person(‘Ellie’, 21, 45);

asma.displayWeight();
ellie.displayWeight();

RESULT:
55
45
```
____________________________________

> **INHERITANCE**

Inheritance is making one base class that has functions that you share. 

```JavaScript
class person {

 constructor(name, age, weight){
	this.name = name;
	this.age = age;
	this.weight = weight;

displayName() {
	console.log(this.name);
 }

displayAge() {
	console.log(this.age);
 }

displayWeight() {
	console.log(this.weight);
 }
}

class programmer extends Person {
	 constructor(name, age, weight, language) {
	   super(name, age, weight);
	   this.language = language;
 }

displayLanguage() {
	console.log(this.language);
 }
}
```

1. What ```extends person``` does is saying go ahead and grab all the code in ```Person``` and bring it into this class.
2. Inside the constructor we are going to call the parents constructor by using keyword ```super()```. Now the parents constructor since the ```programmer``` is a type of ```person``` it will take ```name, age, weight``` which is what we pass into super.
3. This programmer has an extra attribute language, you can also add custom functions such as ```displayLanguage```.

```JavaScript
let ellie = new Person(‘Ellie’, 21, 45);
ellie.displayName();
ellie.displayWeight();


let asmarion = new programmer(‘Asmarion, 45,86, ‘JavaScript’);
asmarion.displayName();
asmarion.displayAge();
asmarion.displayLanguage();

RESULT:
Ellie
45

Asmarion
86
JavaScript
```

______________________________________
> **GENERATORS**


It allows you to make functions with checkpoints in them e.g. run the first two lines and pause.

1. Whenever you make a generator function add the ```*``` after the function keyword then add whatever function name you want.
2. These checkpoints are determined by the ```yield``` keyword which basically means pause.
3. ```let sample``` is just a reference to the function. When you call is for the 1st time its going to run till the yield e.g. return only apples.
4. This next function means run the generator until you get to the yield statement.
5. The results return ```object``` with value of apple and the ```done``` will be set to false until it has through all the yield statements.
6. If you do a ```sample.next``` after the list is done it will return undefined

```JavaScript
function* sampleGenerator() {
	yield ‘apples’;
	yield ‘banana’;
	console.log(‘ok this is the after banana…’);
	yield ‘corn’;
}

let sample = sampleGenerator();
console.log(sample.next());

RESULT:
{ value: ‘apple’, done: false }
```

**Tip:** You can add .value  if you only wanted the value returned e.g. *apple*
```console.log(sample.next().value);```


_____________________________________________________________________

> **REFERENCES**

[Lets Learn ES6 - Ryan Christani] ([https://www.youtube.com/watch?v=oTRujqZYhrU)

[The New Boston ES6 playlist](https://www.tutorialspoint.com/es6/es6_classes.html)

[Tutorial point ES6](https://www.tutorialspoint.com)

