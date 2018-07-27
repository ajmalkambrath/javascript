# javascript

### Values & References

JavaScript has 5 data types that are copied by value: Boolean, null, undefined, String, and Number. We’ll call these primitive types.

JavaScript has 3 data types that are copied by having their reference copied: Array, Function, and Object. These are all technically Objects, so we’ll refer to them collectively as Objects.

### Function 

There are two way to write a function. 
 ##### function expression
 JavaScript expressions is that they return values.
 ```
 var fn = function() {
    // do something...
}
 ```
 
  ##### function declaration
  ```
  function fn() {
    // do something...
}
  ```

### understanding Scope:

Scope is the accessibility of variables, functions, and objects in some particular part of your code during runtime. In other words, scope determines the visibility of variables and other resources in areas of your code.

### higher order function

### Currying
Currying is a technique of evaluating function with multiple arguments, into sequence of function with single argument.

In other words, when a function, instead of taking all arguments at one time, takes the first one and return a new function that takes the second one and returns a new function which takes the third one, and so forth, until all arguments have been fulfilled.

consider below example code:

```
var add =   function (a){
                 return function(b){
                       return function(c){
                              return a+b+c;
                              }        
                        }
                  }
console.log(add(2)(3)(4)); //output 9
console.log(add(3)(4)(5)); //output 12
```




### Hoisting

Hoisting is a JavaScript mechanism where variables and function declarations are moved to the top of their scope before code execution.


##### variable Hoisting
only the variable declaration, not the assignment, is hoisted. 
A variable that is not declared using var will not be hoisted. 
JavaScript only hoists declarations, not initialisation.



##### Function Hoisting


A function expression gets hoisted just like a normal variable. The variable goes to the top of the scope and gets the value undefined, later being set to the function itself at the expected place in the code.

A function declaration, on the other hand, gets hoisted in its entirety. The variable gets moved to the top and immediately is equal to the function. It even gets hoisted higher than normal variable initializations.

```
Example1:

fnDeclaration(); // -> This works!
fnExpression(); // -> Uncaught TypeError: fnExpression is not a function

function fnDeclaration() {
    console.log('This works!');
}

var fnExpression = function() {
    console.log("This won't work :(");
}
```

```
Example 2 :

var a = 123;
var b = 'abc';

var fnExpression = function() {
    var c = 456;
    var d = 'def';
}

function fnDeclaration() {
    var e = 789;
}
```
The final version of this code that the compiler will run looks more like this.
```


function fnDeclaration() {
    var e;
  
    e = 789;
}

var a;
var b;
var fnExpression;

a = 123;
b = 'abc';

fnExpression = function() {
    var c;
    var d;
  
    c = 456;
    d = 'def';
}



```

### IIFE 

IIFE (Immediately Invoked Function Expression) is a JavaScript function that runs as soon as it is defined.

```
(function (){
// logic here 
})();

```
The primary reason to use an IIFE is to obtain data privacy. Because JavaScript’s var scopes variables to their containing function, any variables declared within the IIFE cannot be accessed by the outside world.

```
(function () 
{ var foo = “hello”;
console.log(foo);
 })
();
console.log(foo); //Error: foo is not defined
```

### Closures 

A closure is an inner function that has access to the outer function’s variables — scope chain.The inner function will have access to the variables in the outer function scope, even after the outer function has returned. 

The closure has three scope chains: 
 - it has access to its own scope (variables defined between its curly brackets)
 - it has access to the outer function’s variables, 
 - it has access to the global variables.
also
- outer functions parameters 
- inner function parameters

In JavaScript doesn’t have private keyword but we can achieve private methods and properties using closures.

```
var myModule = (function() {
    'use strict';
 
    var _privateProperty = 'Hello World';
     
    function _privateMethod() {
        console.log(_privateProperty);
    }
     
    return {
        publicMethod: function() {
            _privateMethod();
        }
    };
}());
  
myModule.publicMethod();                    // outputs 'Hello World'   
console.log(myModule._privateProperty);     // is undefined      
protected by the module closure
myModule._privateMethod();                  // is TypeError protected by the module closure
```


### The Module pattern:


In JavaScript, the word “modules” refers to small units of independent, reusable code. They are the foundation of many JavaScript design patterns and are critically necessary when building any non-trivial JavaScript-based application.


Why we need to use Module?

There are a lot of benefits to using modules :
 >> maintainablity
 >> reusability
 >> Namespacing
 
```
var myModule = (function() {
    'use strict';
 
    var _privateProperty = 'Hello World';
     
    function _privateMethod() {
        console.log(_privateProperty);
    }
     
    return {
        publicMethod: function() {
            _privateMethod();
        }
    };
}());
  
myModule.publicMethod();                    // outputs 'Hello World'   
console.log(myModule._privateProperty);     // is undefined      
protected by the module closure
myModule._privateMethod();                  // is TypeError protected by the module closure
```
 
 these modules can have export to the other JS files using export keyword,


```
//myMOdule.js file
export default myModule;
```
 
 modules can import to another JS file

  ```
  //second.js file 
import myModule from ‘./myModule’;

  ```
  
 ### Memoization
 
Memoization is a programming technique which attempts to increase a function’s performance by caching its previously computed results. Because JavaScript objects behave like associative arrays, they are ideal candidates to act as caches. Each time a memoized function is called, its parameters are used to index the cache. If the data is present, then it can be returned, without executing the entire function. However, if the data is not cached, then the function is executed, and the result is added to the cache.

Function is an integral part of the programming,they help to modularity and reusable to our code, as per above definition memoization is an optimising our code

```
const memoizedAdd = () => {
  let cache = {};
 return (value) => {
  if (value in cache) {
   console.log('Fetching from cache');
   return cache[value];
  }
  else {
   console.log('Calculating result');
   let result = value + 10;
   cache[value] = result;
   return result;
  }
 }
}
// returned function from memoizedAdd
const newAdd = memoizedAdd();
console.log(newAdd(9)); //output: 19 calculated
console.log(newAdd(9)); //output: 19 cached
from above code you can understand memoization.


```



### Callback Function

```
callback function is a function passed into another function as an argument, which is then invoked inside the outer function to complete some kind of routine or action.
```

### The apply, call, and bind methods:

1.Call method:

consider below code,obj have the property of num, using call method we can bound obj to add function,
```
var obj={
   num : 2
}
var add = function(num2,num3,num4){
   return this.num + num2 + num3 + num4;
}
var arr=[3,4,5];
//Call method 
console.log(add.call(obj,3,4,5));  //Output : 14
//Apply method
console.log(add.apply(obj,arr));   //Output : 14
//bind Method
var bound = add.bind(obj);
console.log(bound(3,4,5));         //output : 14 
```
2.Apply Method

The same way Apply method also works but the only difference is using apply method the passing arguments could be an array, refer below code.

3.Bind Method:

In bind method returns a method instance instead of result value ,after that need to execute bound method with arguments.


### Synchronous  /  Asynchronous  / defer


Browser JS Engine parse Html file and executes JavaScript by three patterns,

1. synchronous
2. Asynchronous
3. defer

```
index.html
<script src='index.js'>           //default Synchronous
<script async src='index.js'>      //parse as Asynchronously
<script defer src='index.js'>      //parse as deferred
```

while browser JS Engine parsing html file if <Script > tag occurs means there will be a blocking ,so how its get execute JavaScript Code for that above three patterns.

>> If synchronous <script > tag occurs, JS engine will download the code and execute that code and after that only parsing the below html code,generally Synchronous is a blocking script execution.
>> If Asynchronous <script async> tag occurs, while downloading the code JS engine will parse the html and once If JS code get’s downloaded pause the parsing and back into the JS Code Execution,generally Asynchronous is an Non-blocking script execution.
>> If Asynchronous <script defer> tag occurs, JS Engine will parse the all html code and after that only executes the JS Code,
 
 
 ### Async & Await
 
 async & await basically just syntactic sugar on top of Promises, these two keywords alone should make writing asynchronous code in Node much more bearable.

```
ES5 -> Callback
ES6 -> Promise
ES7 -> async & await
```
async/await is a great syntactic improvement for both nodejs and browser programer. Comparing to Promises, it is a shortcut to reach the same destination. It helps developer to implement functional programming in JavaScript, and increases the code readability, making JavaScript more enjoyable.



Reference From:

https://medium.com/@madasamy/15-javascript-concepts-that-every-nodejs-programmer-must-to-know-6894f5157cb7
