
# JS

## Types

- **Primitive** (numbers, strings, booleans, NaN, Undefined, Null, Symbol, Object...) values passed by **value**
- **Objects** (Object, Array, Functions...) are passed by **reference** 
- `typof` returns the type of given statement. In JS, values have types, not variables. 
- `NaN` is a value we get when we try to do numerical operations with non numerical values.(like converting non numeric string to number)
  - two identical NaN values not equals themselves 
  - `isNaN` converts given statement to number and returns if it is NaN. `Number.isNaN` does not converts.
  - `typof NaN` is number (but invalid number)
- **Fundamental objects**: Top level build in objects we can create with new keyword
  -  `Object()` `Array()` `Function()` `Date()` `RegExp()` `Error()`
  - `String()` `Number()` `Boolean()` (not recommended to use them)
- **Coercion** converting between types
  - `+` operator do concetenation if one side is a string and if other side is number, it will be coerced to string. 
  -  `==` Double Equals (compares values after  coercing)
    - if types are equal > does triple equals(compares value and types without coercing)
    - if they are null and undefined > true
    - if non primitive > convert to primitive and compare
    - if two primitive with different types > toNumber and compare

---

## Objects, Arrays and Functions

```js
//Creating
obj1={};
obj1.name="clem"
//or
obj2={"name":"clem"}

//2 methods of calling
obj1.name; //dot notation
obj["name"] //bracket notation
```

- Arrays are objects `[alfa,beta]` ~= `{"0":"alfa", "1":"beta",}`

- Bracket notation can be used when we cannot use dot notation. (like array's indexes `array[0]` == ~`array.0` but we cannot use string literals in dot notation) 

- With bracket notation we can use variables as keys `key = "name"; obj1[key]` == `obj["name"]` == `obj1.name;` 

### Array Methods

- **ForEach and ForIn** 

  ```js
  //ForEach
  let food = ['mango','rice','pepper','pear'];
  food.forEach(function(item, index, array){
      console.log(`I want to eat number ${index+1}:  ${item} in >> [${array}] list`);
  }); 
  
  //For ... in iterate in properties in objects
  var person = {name: "clem", surname: "fandango", age: "27"};
      
  for (const prop in person) {
    console.log(`person.${prop} = ${person[prop]}`);
  }
  ```

- **Map** (calls given function for every item and modifies with returned value then returns modified array )

  ```js
  let cost = [100,400,300,700];
  let newCost = cost.map(function(costItem){
      return costItem / 10;
  });
  console.log(newCost); //[10,40,30,70];
  ```

- **Filter**  (calls given function for every item. If given function returns true and it puts to array that will be returned)

  ```js
  let cost = [100,400,50,40,700];
  let smallCost = cost.filter(function(costItem){
      return costItem < 200
  });
  console.log(smallCost);
  ```
  
- **Reduce** (calls given function with arguments 1:(previous returned value from given function) 2:(current item)  and returns one value)

  ```js
  nums = [1,2,3];
  nums.reduce(function(prev, current){
      return prev+current;
  },0); //6 (0 is initial value for prev)
  
  ```

- **Iterators** create an iterator for a data source (array,obj...) iterate over one by one (last item returns false)

  ```js
  var word = "hello";
  var itr1 = word[Symbol.iterator]();
  itr1.next(); //{ value: 'h', done: false }
  itr1.next();//{ value: 'e', done: false }
  ...
  itr1.next();//{ value: 'o', done: false }
  itr1.next();//{ value: 'undefined', done: true }
  ```

- **Generators** a special function that returns iterator when its called. (name starts with * when defining) `...` operator can process iterables.(last item(returned) returns true) 

  ```js
  function *main(){
      yield 1;
      yield 2;
      yield 3;
      return 4;
  }
  var itr = main(); 
  itr.next(); //{ value: 1, done: false }
  itr.next(); //{ value: 2, done: false }
  itr.next(); //{ value: 3, done: false }
  itr.next(); //{ value: 4, done: true }
  [...main()] //[1,2,3]
  ```

  - Geneator with dynamic data 

  ```js
  function *createFlow(){
   const num = 10
   const newNum = yield num //yield suspended EC and returned 10 when "next()" function run for the first time
   //when we call "next()" again, it will continue from where its left. In this case(second run), its the line above
   //The argument we pass to "next()" will be the evaluated result of previous yield.
   yield 5 + newNum
   yield 6
  }
  const returnNextElement = createFlow()
  const element1 = returnNextElement.next() // 10
  
  //evaluated result of "yield num" will be 2
  const element2 = returnNextElement.next(2) // 7
  ```

  



### Regular Expressions



### ES6 Destructuring

Get multiple values from arrays/objects with one statement

  ```js
  //ARRAYS
  var [name,surname]=["clem","fandango"] //can be used in defining and assigning
  //same as > var name = "clem";var surname = "fandango";
  
  [a, b, ...rest] = [10, 20, 30, 40, 50];
  // rest: [30,40,50]
  
  //swap values
  [a,b]=[b,a];
  
  //OBJECTS
  ({ a, b } = { a: 10, b: 20 }) parentheses are required when assigning without decleration. 
  //same > a=10; b=20;
  
  var obj = { a: 10, b: 20,c:30 } ;
  var { a, c } = obj;//extract a and c from obj and assign it to variables with same name with keys
  
  //Assigning to diffirent names
  var obj = {p: 42, q: true};
  var {p: foo, q: bar} = obj; //creates "foo=42 bar=true" variables 
  ```

  ### Functions
```js
  /* Defining 
  * Fuction name: nameImprover
  * Parameters: name, adj (vars used in definition)
  * Body: Inside of Curly Bracets */
  var nameImprover = function(name, adj){
      return "col" + name + "Mc" + adj + "pants";
  }
  
  /* Calling/Invoking
  * Arguments: person.name, person.adj (vars or values passed to function) */
  var shownName = nameImprover(person.name, person.adj);

//----------------------------------------------------------------------
//Types of declaring a function
//declare a var and assign funtion to it
var func = function(){...} //Anonymous function expression
var func2 = function MyFunc(){} //Namend Function Expression //we can access to that funncion from inside with its name
//Declare a function
var function func3(){}//Function Decleration
```

- Functions in JS are first class objects 

- `arguments` keyword can be used in function definition body. It returns all the arguments passed in as pseudo array. (Not available in arrow functions)

- Functions are objects but have its own type `typeof console.log === "function"`

- To access object part of function from its definition, we can use `arguments.callee` .(not recommended and not available on strict mode)

- Functions can  be
  - Stored as variables
  
  - Used in arrays
  
  - Assigned as object properties (methods)
  
  - Passed as arguments
  
  - Returned from other functions
  
    
  
- Method is function stored in objects.

- **Higher Order Function** : Takes a function as input and/or returns a function.

#### Binding (`this`)

Binding a context to fuction to determine what `this` corresponds

- Implicit Binding **`workshop1.ask("what")`** //this >> workshop1
- Explicit Binding **`ask.call(workshop2,"what")` ** // this >> workshop2
- Hard Binding **`setTimeout(workshop.ask.bind(workshop),100,"what")`** //this >> worksop (`this` can be lost when using function on callback)
- New Binding: **`emptyObj = new ask("what")` ** //this >> {an empty obj} (creates an empty obect and bind function to that object's context)  ~~ `ask.call({},"what")`
- Default binding `ask("what") ` // this>> global (If there is no binding specified like above, it binds to global by default if not in strict mode)

If a function called in multiple types of binding the precedence is (new > call,apply,bind > implicit > default)

Arrow functions don't have this keyword, it gets this of scope in one level up.

#### Funcions Methods (`call` `apply`, `bind`)

#### Currying 

#### Composing 





---

## Scopes & Closures

### **Scope**

* Scope is where to look for things(where variable,identifier etc. belongs to)

* JS runs in at least two passes (first pass ~compile, second pass run)

* Scoping happens in **first pass **(compilation). Looks for formal declerations (var, function etc.) and decides to which varible are in which scope). Creates a new scope for each function and looks for formal declerations inside them too. looks for each variable if it is in target position or source position.

* Executing happens in **second pass**. JS Runtime Engine executes ask for variables to Scope Manager. If It is not in that scope, ,go to one scope level up. In second pass, variables that are not declared formally (without var keyword), engine tries to find until come to global scope, it is not in there so variable declared in global (auto global) (If it is not in strict mode). 

* **`var`** creates **function** scopes (not available outside of function)

* **`let`** creates **block** scope (not available outside block (`{}` ,`for`, `while`,  `switch`, `function`, `class`,  `if`))

* Hoisting: Not a real thing. Just a metaphor to explain accesing variables that are declared after. It says, declerations are moved to the top of scope when a scope created, as if it is working in one pass. But JS is at least  double pass lang. Scoping (which var is where) happens in first pass. 

  

### **Closure**

- When a function(parent) returns a function (child fuction) . Child function accesses scope of parent. After we run perent function and assign it to a varible, variable is now ~copy of child function along with scope of parent(lexiacal scope) A bond between child function and the scope of parent (which defines child function). Normally we expect parent to be trashed after we run parent (when var assigned to child).  But when the child returned, it brings a scope called lexical scope ([[scope]]) that is the scope of parent. Every time we call parent a new lexical scope is created (for each returned child func).  

* When child function called (with the variable that parent function's return value that assigned to), It looks for variables for its local scope, then lexical scope, then the scope below in call stack.  

   
```js
  //Create a function that returns a function that alerts (alerter)
  const myAlert = () => {
      const x = "Help Me!"
      let count = 0;
      const alerter = () => {
          alert(`${x} ${++count}`);
      };
      return alerter;
  }
  
  const funcAlert1 = myAlert(); //funcAlert1 contains body of alerter function. Since alerter has access to some variables in parent func (myAlert), a lexical scope of myAlert also created. 
  const funcAlert2 = myAlert(); //same but a new lexical scope created 
  
  funcAlert1(); //creates a new scope of alerter every time but modifies parent vars (in myAlert lexical scope) count:1 
  funcAlert1(); //creates new scope of alerter but the lexical scope (myAlert) from previous is still available count:2
```

* Another closure examples (multiplier and timer)

```js
const makeMultiplyBy = function(x){
    return function(y){return x*y;};
};

var double = makeMultiplyBy(2);
var triple = makeMultiplyBy(3);

double(5);//10
triple(4);//12
```

```js
const makeTimer = function(){
    let elapsed=0;
    const stopwatch = function(){return elapsed;};
    const increase = function(){elapsed++;};
    setInterval(increase,1000);
    
    return stopwatch;
}
let timer = makeTimer(); //lexical scope created (parent) and timer started
timer();//returns seconds elapsed each time;
```

### Modules 

- Module pattern: Closures can be used to create modules. Modules are encapsulates some functionality/data, and provides(expose) some functionality/data publicly. 

- Old Style Module Pattern

  ```js
  var workshop = (function module(teacher){
      var publicAPI = {ask,}
      return publicAPI;
      
      function ask(question){
          console.log(teacher, question)
      }
  })("Kyle");
  
  workshop.ask("It is a Module right?"); //Kyle, It is a Module right?
  ```

- ES6 Modules Pattern

  ```js
  //workshop.mjs
  var teacher = "kyle";
  export default function ask(question){
  	console.log(teacher, question);
  };
  
  //importing and using on other file
  import ask from "workshop.mjs"; //import a function directly
  ask("asd");
  
  import * as workshop from "workshop.mjs"; //import whole module like namespace
  workshop.ask("asd");
  
  ```
  

---

## Runtime

* On JS runtime there are (EC:Execution Context)
  1. **`memory (variable environment)`:** each EC has own memory. At first it is global memory. When a new env created it has its own (local) memory. When the EC done, it will be deleted (garbage collected) with its local memory.
  
  2. **`call stack` :** A data structure stores the EC we are in. When the code runs, first stack has only global EC. While the code running, thread creates a new local envirenment(EC) when a function is called/run and a new EC will be pushed to call stack. When thread gets the end of EC (like return or implicit return from that func), that EC will be popped off from stack and deleted. thread goes to previous EC (the one at the top of stack).  

  3. **`thread of execution(TOE)`:** runs code line by line ( synchronously ), store data in memory of current EC, push ECs to or pops ECs from call stack...  
  
  4. **`browser API / Node background threads`:** Some collection of functionalities that browser (or an environment that our js code runs on) provides. It is outside of our TOE (JS environment). 
  
     * `timer` A functionality provided by the browser that we can interface with `setTimeout` etc. When we create a `setTimeout(printHello,0)`, our TOE interfaces (talks) Browser's timer feature.  It sends the printHello function def reference and ms to excecute that function. Browser creates a timer with these data in outside of our thread of execution. While the timer created and started, our TOE continues to run. When the timer finised, browser queues printHello to callback queue. Callback queue can only push queued items to call stack when call stack is empty. Our TOE runs line by line finishes every item in call stack. While, Event loop checks if the call stack is empty every time. When last item (it would be globalEC) finished, Event loop notifies callback queue. First item in queue can now be pushed to call stack. Now printHello function come back to our normal TOE a new EC created for it. it executes and finishes.
  
       Timer feature lets us run passed function asynchronously (nonblocking blocking) . 
  
       If setTimeut would be a function in js, we expect TOE to enter set Timeout, wait for some time then run and enter the passed function then go back... That would block our TOE.  
  
     * There are`ajax`, `events`, `read/write fs`(Node), `db operations`, interacting with device and lots of other functionalities that browser provide. Those features help us when we need asynchrnocity where the operation we want to do, block our TEO because it needs waiting. 
  
     * `xmlHttpRequest`
  
  5. **`callback/message/task queue`** A queue data structure stores items that needs to be pushed to call stack. But these items are came from things that outside of TOE(JS Env) (like timer in browser API). (Timers,...)
  
  6. **`microtask(job) queue`** : A queue to store functions in `onfullfillment`(them) property of promise object. This queue has more priority over callback queue. (Promises)
  
  7. **`Event Loop`** The event that checks that is Call Stack Empty and is there any item in callback queue to be pushed to Call Stack. If Stack is empty, items in callback queue can be pushed to call stack.
  
---

## Asynchronous

### Promise

- 
- `fetch` A browser feature to get data from servers asynchronously. it returns a Promise Object
  - `const futureData = fetch('https://twitter.com/will/tweets/1')` Returns a promise object and assigns to future data.
  - fetch do two things. one in JS and one in Web Browser
    - JS > creates a promise object that has `value` and `onfulfillment` (array) attributes. And instantly returns. 
    - Browser > makes an xmlhttprequest to server and assign value to `value` property of promise. When the value assigned, all functions in fulfillment array will be queued to `microtask queue` 
  - `futureData.then(display); ` adds display function to `onfulfillment` array in promise object that we store in `futureData` variable. 
  - `futureData.catch(err); ` adds err function to `onrejection` array in promise object that we store in `futureData` variable. 

### Async Await

- 

```js
async function createFlow(){
 console.log("Me first")
 const data = await fetch('https://twitter.com/will/tweets/1')
//await is like yield, it pauses async function (createFlow) returns back to previous scope 
// synchronous code(global) continoues to run
//when promise resolved and our sync code finished, async function continues.
 console.log(data)
}
createFlow()
console.log("Me second")
```

- The code above can be emulated with generators functions

```js
function doWhenDataReceived (value){
 returnNextElement.next(value)
}
function* createFlow(){
 const data = yield fetch('http://twitter.com/will/tweets/1')
 console.log(data)
}
const returnNextElement = createFlow()
const futureData = returnNextElement.next()
futureData.then(doWhenDataReceived)
```



---

## Object Oriented JS

- Class orianted OOP in other languages(Java, C++...) soes not fit to JS. JS has Prototypal inheritance

- Without functions we can create object like below but its repetitive

  ```js
  var user1={};//create an empty object
  //and fill it in
  user1.name='will';
  user1.score=3;
  user1.increment= function{
   	user1.score++;
  }
  //use its functionalities
  user1.increment();
  //to create new users, we should repeat the code above
  ```

### **Factory Pattern**

  We can create function that generates similar objects. (But the problem in here is we create totally same increment function for each user we create. But the function definitions are the same)

  ```js
  //declare a function that creates user objects
  function userCreator(name,score){
    let newUser = Object.create(null);
    newUser.name='will';
  	newUser.score=3;
  	newUser.increment= function{
     		 user1.score++;
  	};
      return newUser;
  };
  
  //create users
  let user1=userCreator('will',3);
  let user2=userCreator('tim',8);
  
  //use its functionalities independently
  user1.increment();
  user2.increment();
  ```

### `this`

- Whenever we create an execution context, a keyword this created in that EC's local memory that refers to that EC we are in.

For example: Let's call a function of an object like `user1.login()`. Inside login function, `this` keyword refers to `user1`, so that we don't need to know the name of the object we are in.

- this in arrow function refers to scope where arrow function is defined. 



### `Object.create()`and `__proto__`

 To solve problem above, we can use JS' prototypal nature, by storing funtions on one object bind to all new instences so they have references to them(not copies). Whatever argument you pass to`Object.create(null)`, it always creates an empty object. 

If we call `Object.create(userFunctionStore)`, it creates an object that has`__proto__` property with the value of reference to `userFunctionStore` object. Whatever object we pass to `create` function, the genereted object will have referernce (not copy) to passed object, so that  we can access data in passed object from generated object without having that data.

```js
//declare a function that creates user objects
function userCreator(name,score){
    let newUser = Object.create(userFunctionStore);//referece the functions object
    newUser.name='will';
	newUser.score=3;
    return newUser;
};

//User Functions
let userFunctionStore = {
	increment: function(){this.score++;}, //this == EC we are in
	login: function(){console.log("you are logged in")}
}

//create users
let user1=userCreator('will',3);
let user2=userCreator('tim',8);

//use its functionalities independently
user1.increment();
user2.increment();
```

**Subclassing**

```js
///...
  function paidUserCreator(paidName,paidScore,accountBalance){
      let newPaidUser = userCreator(paidName,paidScore);
      Object.setPrototypeOf(newPaidUser,paidUserFunctions)
  	  newPaidUser.accountBalance=accountBalance;
      return newPaidUser;
  };

const paidUserFunctions{
    increaseBalance: function() {...}
}
    
Object.setPrototypeOf(paidUserFunctions, userFunctions);
```



### `new` and `prototype`

**Constructor Pattern** A special keyword in JS for OOP. It automates some parts in definition of object creater function.(like `userCreator` above). 

- no need to create object (with Object.create)
- no need to return object
- previously we store our functions that we want them be referenced to in an object and pass to `object.create`, now we can define those functions and assign them to **`ObjectCreaterFunction.prototype` **,  so that they will be referenced when using `new` keyword. 
- All we need when defining our object generator function is data that we need to store. And  the functions to reference.

```js
//Object
function User(name, score){
	this.name = name;
	this.score = score;
}

//define user functions and assign to prototype of Object so that they will be referenced  
User.prototype.increment = function(){
	this.score++;
};
User.prototype.login = function(){
	console.log("login");
};
//create users
let user1 = new User(“Eva”, 9)
user1.increment();
```

- When we call a function with **`new`** keyword, these functionalities are automated in EC of that function, 

  - an empty object has been created, and labeled as `this`  

  - this object has a label `__proto__` with the value of `ourFunction.prototype`  (ourFunction is the function that we called with new keyword). 

  - this object returned

  - our object in EC of function looks like when we call with ``let user1 = new User(“Eva”, 9)` 

    ```js
    {
        name:"",
        score:9,
     	__proto__: User.prototype   
    }
    ```

- When we add functions to `prototype` property of UserCreator function,(`User.prototype.login=LoginFunction;`), we behave UserCreator function as object (functions are objects) and we can store data inside them. That data is outside of its definition. 

- This approach is good but we have to define referenced functions in outside of creator function. 

- **Subclassing**

  ```js
  ///...
    function paidUserCreator(paidName,paidScore,accountBalance){
        userCreator.call(this,paidName,paidScore);//first:context (passed by reference) in func | rest: parameters
    	  this.accountBalance=accountBalance;
    };
  
  paidUserCreator.prototype=Object.create(userCreator.prototype)
  paidUserCreator.prototype.increaseBalance = function() {...}
  ```

  

### `class`

- A keyword that makes our code look like more standard OOP languages and we don't need to define our functions outside. The code below makes the same things with the one above. When we call a `class` with new keyword, it calls the constructior function in that Class.

-  ```js
   class User {
    	constructor (name, score){
    		this.name = name;
    		this.score = score;}
    	increment (){
    		this.score++;}
    	login (){
    		console.log("logged in"); }
  }
  
  let user1 = new User("Eva", 9);
  user1.increment();
  ```

- **Subclassing**: 

  ```js
    class paidUserCreator extends userCreator{
       constructor(paidName,paidScore,accountBalance){
  //"this" is uninitialized at first
  //super > calls the parent(userCreator) object's constructor with params, 
  //assign returned object to "this" in paidUserCreator 
  //retuned object's proto will be paidUserCreator.prototype
        super(paidName,paidScore);//Reflect.construct(userCreator, [paidName,paidScore], paidUserCreator)
    	  this.accountBalance=accountBalance;
    	 }
       increaseBalance = function() {
           ...
       }
    }
  let pUser1 = new paidUserCreator("Eva", 9, 25);
  ```

  extends do extra things for us (functions are objects btw)

  1- It sets `__proto__` attribute in `paidUserCreator.prototype`  to `userCreator.prototype` 

  2- It sets `__proto__` attribute of `paidUserCreator` to `userCreator` (lets us use super)

  

### 

### OLOO (objects linked to other objects) Pattern

  ```js
var Person = {
  init: function(name) {
    this.name = name;
  },
  getName: function() {return this.name;}
};

var Student = Object.create(Person);

Student.set = function(name, school) {
  this.init(name);
  this.school = school;
};

Student.getSchool = function() {
  return this.school;
};

var giamir = Object.create(Student);
giamir.set('John', 'MU');

giamir.getName(); // John
giamir.getSchool(); // MU
  ```

## Functional JS

- Functions should return sth to use in functional programming paradigm. If it does not return anything, its called procedure.  

### Reduce

### **Function composition and Piping** 

Running a set of functions(chaining) with an input. First function's output will be the second one's input, and so on... One function's output will become another functions's input...

```js
const multiplyBy2 = x => x*2
const add3 = x => x+3
const divideBy5 = x => x/5
const reduce = (array, howToCombine, buildingUp) => {
 for (let i = 0; i < array.length; i++){
 	buildingUp = howToCombine(buildingUp, array[i])
 }
 return buildingUp
}
const runFunctionOnInput = (input,fn) => {
 return fn(input)
}
const output = reduce([multiplyBy2, add3, divideBy5], runFunctionOnInput, 11) //pipe 5
```

- **pipe** runs fuctions from left to right
- **compose**  runs fuctions from right to left

### Pure Functions and Immutability 

### Function Decoration and Partial Application 

- Decorate a function. (Making a function that makes given function runnable once)

```js
const oncify = (convertMe) => {
 	let counter = 0
 	const inner = (input) => {
 		if (counter === 0){
 			const output = convertMe(input)
 			counter++
 			return output
 		}
 		return "Sorry"
 	}
 	return inner
}
const multiplyBy2 = num => num*2
const oncifiedMultiplyBy2 = oncify(multiplyBy2)
oncifiedMultiplyBy2(10) // 20
oncifiedMultiplyBy2(7) // Sorry
```

- Making a function to that makes given function partialy applicable. 

```js
const multiply = (a, b) => a * b

function prefillFunction (fn, prefilledValue){
 	const inner = (liveInput) => {
 	const output = fn(liveInput, prefilledValue)
 	return output
 }
 return inner
}
const multiplyBy2 = prefillFunction(multiply, 2)
const result = multiplyBy2(5)
```

### Point Free

### Recursion 

Tail calls, CPS (continuation passing style), Trampolines 

### Transducing 

composing map, filter (not compatable to be composed with reduce) and reduce and make them run at the same time.

### Monad
