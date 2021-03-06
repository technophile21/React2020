# React.js

Banuprakash C

Full Stack Architect, Corporate Trainer,

Co-founder Lucida Technologies Pvt Ltd.,

Email: banu@lucidatechnologies.com; banuprakashc@yahoo.co.in

https://www.linkedin.com/in/banu-prakash-50416019/


Github: https://github.com/BanuPrakash/React2020
-------------------------------------------------------------------------
Softwares Required:
1) Chrome Webbrowser with following extensions
	1.1) add React Developer tools
	1.2) add Redux DevTools
	1.3) Lighthouse
2) Visual Studio Code
3) NodeJS Latest LTS

-------------------------------------------------------

	Day 1: JS recap, Functional style of programming, ES 6 features, NodeJs intro Webpack

	Day 2: React : functional components, class components, props and state, ReactContext, 
					Testing using RTL and cypress
					use case

	Day 3: use case ==> React Routers, styled-components, RWD with bootstrap,...

	Day 4: React Hooks, HOC, Performance [ Core Web Vitals ] , Flux Architecture, Redux, ... , 

	JSX and not TSX 
----------------------------------------------------------------------

JavaScript:
	
	Creation Context Phase and Execution Context Phase 

	var g = 10;

	console.log(result); 

	function add(x,y) {
		console.log(this); //window
		return x + y;
	}

	var result = add(4,5);


code runs on JS engine: V8, spider monkey, chakra, Nashorn, .. 

==================================
	
	var g = 10;

	function doTask() {
		var x = 20;
		if(x > g) {
			var y = 30;
			z = 100;
		}
		console.log(g,x,y,z);
	}

	doTask();
	console.log(g,x,y,z);
====================================

	function add (x, y) {
		return
			x + y;
	}

	var res = add(5,6);

	console.log(res); // undefined

	engine starts performing AST [ semi-colon]

 =========================================

 Functional Style of Programming
 --------------------------------
 	Using High Order Functions:
 		a) functions which accept other functions as arguments
 		b) function return a function

 		==> treat function as first-class members 

 		c) not tightly coupled to state of object

 		deposit() withdraw() ==> balance of Account
 	// HOF
 	function forEach(items, action) {
 		for(var i = 0; i < items.length; i++) {
 			action(items[i]);
 		}
 	}

 	var data = [7,3,22,7,21];

 	forEach(data, console.log);
 	forEach(data, alert);
 	======================

 	commonly used HOF:
 		1) map
 		2) filter
 		3) reduce
 		4) forEach
 		5) skip
 		6) limit
 		all callbacks [ registration ]


 		filter ==> subset
 		function filter(items, predicate) {
 			create array
 				loop thro items
 					if( predicate) 
 						add to array
 				end loop
 			return array
 		}

 		==============

 		Map ==> transform
 		function map(items, transformFn) {
 			create array
 				loop thro items
 					add to array (transformFn(item))
  				end loop
 			return array
 		}

 		=============================================
 
https://rxmarbles.com/#map

===========================================

function returning a function ==> HOF

function greeting(msg, name) {
	return msg + " " + name;
}

greeting("Good morning", "Smith");
greeting("Good morning", "Peter");
greeting("Good Day", "Smith");

=================================

function greeting(msg) {
	return function(name) {
		return title + msg + " " + name;
	}
}


var gm = greeting("Good morning");

What is gm ?

gm("Smith");

// closure ==> mechanism where inner functions can access the members of outer function

===========================================================================

memoize 
getEmployee(24); ==> REST calls 

getEmployee(24);  get from cache

============================================

var obj = {
	"name": "Smith",
	"getInfo" : function() {
		return this.name;
	}
}

console.log(obj.name);
console.log(obj.getInfo());

var fn = obj.getInfo; // here context is lost [ this ]
console.log(fn()); // Should i get Smith

var prod = {
	"name": "IPhone"
}
var newFn = obj.getInfo.bind(obj);
console.log(newFn());

=======================


callback

var g = 10;

console.log(g);

setInterval(function some() {
	console.log("timeout!!!")
}, 10);

function add(x,y) {
	return x + y;
}

add(4,5);

document.addEventListener("click", function task() {
	console.log("clicked!!!");
});

===================================================================================
functions as objects:

function Product(name, price) {
	this.name = name;
	this.price;

	getName = function() {
		return this.name;
	}

	getPrice = function () {
		return this.price;
	}
}

var p1 = new Product("a", 33);
var p2 = new Product("b", 313);
p1.getName(); ...



function Product(name, price) {
	this.name = name;
	this.price;
}
Product.prototype.getName = function() {
		return this.name;
	}
Product.prototype.getPrice = function () {
		return this.price;
}
var p1 = new Product("a", 33);
var p2 = new Product("b", 313);

===========================================


ES2015 ==> ES 6 version 

ECMAScript
-----------
ES 6 Features:
1) block level variable
prior to ES 6 we had only global scope and function scope

var g = 10; // global scope

function doTask() {
	var x = 50; // function scope
	if(x > g) {
		let y = 22; // block scope variable
		const PI = 3.14159; // block scope constant
	}
}

2) arrow functions

function add(x,y) {
	return x + y;
}

let add = (x,y) => {
	return x + y;
}

let sub = (x,y) => x - y;

// default arguments
let add = (x = 0, y = 0, z = 0) => x + y + z;

Note: arrow functions doesn't have its own context: [this used within arrow function will use the enclosing context]

3) Deconstructing arrays

	let colors = ["red", "green", "blue", "pink"];

	old way:

	var red  = colors[0];

	New way:

	let [r,g,...others] = colors;

4) Deconstructing objects

	let p = {
		"name": "iPhone 11",
		"price" : 98000,
		"company" : "apple"
	};

	let {name, price, company} = p;

	let {name:x, price:y} = p;

=================================================
 Arrow functions gets the "context ==> this" from enclosing scope
 whereas the functon gets "global context"

var age = 10;  
function Person() {
  this.age = 42;  
  setTimeout(function () { 
    console.log("this.age", this.age); // yields "10"  
  }, 100);
}

var p = new Person();

===========

var age = 10;  
function Person() {
  this.age = 42;  
  setTimeout(() => {  
    console.log("this.age", this.age); // yields "42"  
  }, 100);
}

var p = new Person();
============================================

5) Template Variable using String literal [ tick marks]

let name = "Smith";

let content = ` 
	<p>first line 
	Name is ${name}
	Good Day
	</p>
`;

content = "<p>first line <br /> Name is " + name + " <br /> Good Day";

====================================

6) Promise API for asynchronous functions

Synchronous functions

function doTask() {
	..
}

let res = doTask();
console.log(res);
console.log("end");

=============
asynchronous functions : assume doTask is async operations
[ making an HTTP call to server or code executing after timeout, click button, ..]

function doTask() {
	..
}

//doTask(); // promise 

doTask().then( (res) => {
		// resolved operation
},
(rej) => {
	// rejected operation
})

console.log("end");


================

doSomeTask().
	then( res => ...).
	then( secres => ....).
	then( third => ...).
	catch(err => console.log(err));

fetch('https://jsonplaceholder.typicode.com/posts/1')
.then( response => response.json() )
.then( body => console.log(body));

===========================================
7) async and await
==================================

8) Generators

	function* doTask() {
		code
		code
		yield "first result";
		code
		code
		yield "second result";
		...
	}


	let iter = doTask(); // iterator

	iter.next();

	iter.next(); {"done": false, "value": "second result"}

	==========

	function* doTask() {

		yield "one";
		yield "two";
		yield "three";

	}

	var iter = doTask()


	iter.next()
	iter.next()
=========================

let p = {"name" : "HP", "price": 135000}

let r = p; // reference
r.price = 54322
p 
{name: "HP", price: 54322}

============

copy instead of reference:
let obj = {...p}

old way:
let obj = Object.clone(p);

=======================================

ES 6 / 7 ==> most of JS engines don't understand them
we need to convert them into ES 5 or lower version
Transpiler ==> Transcompiler
a) Babel
c) Tracuer
==========

9) class 

class Person {
	constructor(name = "", age = 0) {
		this.name = name;
		this.age = age;
	}

	getName() {
		return this.name;
	}
}

let p = new Person("Tim", 23);

internally it is prototype
function Person() {
	this.name =...
}

Person.prototype.getName = function () {
	
}

=============================

10) ES 6 Module system

time.js
export class Time {
	
}

export const add = (x,y) => x + y;

other.js

import {Time, add} from './time';

let t = new Time();

==========


time.js
export default class Time {
	
}
export const add = (x,y) => x + y;

other.js
import Time, {add} from './time';
let t = new Time();

========================

Node.js LTS

Node modules, Webpack after the TEA Break
==============================================

Node.js ==> JavaScript environment built on top of V8 engine

Where can i use node.js
1) server side code ==> APIs
2) Real time application [ chat bot]
3) Streaming 
4) Anyting which is async operations
*** 5) as an environment for building web application ***

=========

simple application

NPM ==> Node package manager

Node installation comes with many pre-defined modules [ http, fs, repl, url, cluster,..]

NPM helps to manage dependencies

npm init -y

creates package.json
==> information about your application 
	==> dependencies [ dependenciies required in production]
	==> devDependencies [ required only for development stage ==> like testing]
==> scripts

===============

package.json ==> maven pom.xml

npm install -D mocha chai request

mocha ==> unit testing
chai ==> assertion library
request ==> to make HTTP calls for testing

Node,js uses Common Module system and not ES 6 module system

========================

Unit testing JS:
 Different librariries / frameworks
 a) Jasmine [ comes with assertion librarires]
 b) JEST [ comes with assertion librarires]
 c) Mocha [ doesn;t have assertion library]

 AAA ==> Assemble Action Assert
 chai --> Assertion library

====================================================

NodeJs as an environmet for buidling web application 

1) we have many "js" / "ts" / "jsx" / "tsx" files 

legacy way of using JS files:
	index.html

	<script src="a.js"> </script>
	<script src="b.js"> </script>
	<script src="c.js"> </script>
	<script src="d.js"> </script>

	problem: many network hits; order should be mainitened

2) we need to do "testing", "linting" "minify" , "uglify" , "code coverage"

3) we need to bundle them "bundle.js"
	
	<script src="bundle.js" > </script>
4) we need to make our code compatable with browser [ typescript, ES6/7]
	transcompiler ==> babel or tsc

JavaScript build tools: Grunt, Gulp, Webpack
===============================================
function Course(config:any) { 
    return function (target:any) {
      Object.defineProperty(
          target.prototype,
          'course',
          {value: () => config.course} 
      )
    }
  }
   "cypress": "cypress open",
    "cypress-test": "cypress run"
  
    "devDependencies": {
    "@cypress/code-coverage": "^3.8.2",
    "@cypress/instrument-cra": "^1.4.0",
    "cypress": "^5.5.0"
  }

=============

 state = {
        "customers" :[{
            "id": 1,
            "firstName": "Rachel",
            "lastName": "Green ",
            "gender": "female",
            "address": "Blore"
        },
        {
            "id": 2,
            "firstName": "Chandler",
            "lastName": "Bing",
            "gender": "male",
            "address": "West Street"
        },
        {
            "id": 3,
            "firstName": "Joey",
            "lastName": "Tribbiani",
            "gender": "male",
            "address": "Kattegat"
        },
        {
            "id": 4,
            "firstName": "Monica",
            "lastName": "Geller",
            "gender": "female",
            "address": "some address"
        },
        {
            "id": 5,
            "firstName": "Ross",
            "lastName": "Geller",
            "gender": "male",
            "address": "some address "
        },
        {
            "id": 6,
            "firstName": "Phoebe",
            "lastName": "Buffay",
            "gender": "female",
            "address": "some address"
        }
    ],
    };

=============

Day 2:
------
	Functional style of programming ==> HOF ==> Closure
	prototype ==> adding methods to our class / objects
	ES 6 features
	Node.js environment for building web application
	Webpack ==> babel for transcompiler

	Java:

	class Person {
		private String name;
		Person() { }

		public String getName() {

		}
	}

	JS:
	FUNCTION CONSTRUCTOR:
	function Person(name, age) {
		this.name = name; // state
	}

	Person.prototype.getName = function () { return this.name; }
	new Person("..", 31);
	=======

	ES 6:
	class Person {
		constructor(name, age) {
			this.name = name;
			this.age = age;
		}

		 getName() {
		 	return this.name
		}
	}

==================================================

 "sourceMap": true

 a.ts  ==> a.map.js ===> a.js [ executed on Browser ]


"module": "es6" [ export and import]

"module": "commonjs", [ module.exports and require]

====================

TypeScript ==> layer on JS ==> introduces concept of data types to JavaScript

ts --> tsc --> js [ executes on JS engine]


typeof x


data types in typescript:

1) boolean

	var flag:boolean = false;

	flag = "1"; // tsc will throw an error on this line

2) string

	var name:string = 'Raj';

	name = 100; //error

3) number
	var x: number = 10;

4) any

	var data: any;

	data = 200;

	data = [4,6,7,2];

	data = "test";

5) array

	let elems:number[] = [4,6,2,7,1];

6) enum
	
	enum Priority {
		LOW,
		MED,
		HIGH
	}

	let high:Priority = Priority.HIGH;

==============================================================================

functions in typescript
-----------------------

function add(x:number, y: number) : number {
	return x + y;
}

add(4,5); // valid

add("a", 10) ; // tsc error


function add(x,y) { } // valid in typescript

function add(x:number, y: number) : void {
	console.log( x + y );
}

=======================================

interfaces

for shape

interface Person {
	id:number,
	name:string,
	address?:string //optional
}

function addPerson(person:Person) {
	// code
}

addPerson( { "id": 55, "name": "sam"});

===========================

interface Timer {
	setTimer(no: number) : void
}


class Game implements Timer {
	
	setTimer(no:number) {
		// code 
	}
}

====================================

classes in typescript

class Person {
	private name:string;
	private age: number;

	constructor(name, age) {
		this.name = name;
		this.age = age;
	}

	public getName() : string {
		return this.name;
	}
}


let p:Person = new Person("a", 22);

p.getName(); 

p.name; // error

-------------------

class Person {
	 
	constructor(private name:string, private age:number) {
		this.name = name;
		this.age = age;
	}

	public getName() : string {
		return this.name;
	}
}

-----------

class x extends y {
	
}

---------------------------------------------------

Decorators: @decoratorName


@Component({
	styles: ...
	template: ...
})
class AppComponent {
	product
}

@Component({
	styles: ...
	template: ...
})
class CardComponent {
	row
}


class Person {
	
	@Upper()
	private firstName:string;

	@Valid()
	private getEmail(): string {

	}
}

npm i -D typescript ts-loader

============================

codepen.io

15 min tea break

npx create-react-app customerapp

===============================================================================

React.js v17

data ==> rendered ==> view

Server side rendering 	==> to the client it sends view [ html]
	JSP, ASP.NET, PHP, EJS, JADE , PUG, 

Client side rendering
	data is fetched to client machine [ Browser] and converted into views

	JavaScript: jQuery , Mustache, Handlebars, underscore ==> view templates

	issues with handling single page applications: SPA

	1) we need to have different views for different url

		http://amazon.com/mobiles/iphone

		http://amazon.com/mobiles/pixel

		http://amazon.com/cart

	2) Data binding [ JSON ==> placeholder ]. don;t need to refersh entire screen

	3) Dependency Injection

===========
Model View Controller

Backbone.js, React.js, Angular, Vue, ...

Angular Framework 								
	1) MVC
	2) builtin Dependency Injection container

React is just a view library ( view part; no controller and no model)

===============================================================

let Welcome = React.createElement("h1",{style:{'color':'red'}}, "Welcome to React 17");

ReactDOM.render(Welcome, document.getElementById("app"))

Virtual DOM

Welcome = {
	tagName : "h1",
	style : ...
	textcontext : "Welcome to ..."
}

========================================

functional components and class components

Functional components returns JSX [ JavaScript + XML]
it should have one root element

function Welcome() {
  return <div>
        <h1>
          Welcome to React.js
        </h1>
    </div>
}

ReactDOM.render(<Welcome />, document.getElementById("app"))


props : mechanism using which parent component passes data to child 

function Welcome(props) {
  return <div>
        <h1>
           {props.title} in {props.name}
        </h1>
    </div>
}

ReactDOM.render(<Welcome title="Welcome to programming" name="Adobe"/>, document.getElementById("app"));

function Welcome({title, name}) {
  return <div>
        <h1>
           {title} in {name}
        </h1>
    </div>
}

ReactDOM.render(<Welcome title="Welcome to programming" name="Adobe"/>, document.getElementById("app"))

==========

class Welcome extends React.Component {
	 // instance varaibels

  constructor(props) {
    super(props);
  }
  render() {
    let {title, name} = this.props;
    return <div>
        <h1>
           {title} in {name}
        </h1>
    </div>
  }

  handleClick() {

	}

  handleSubmit() {

	}
}

ReactDOM.render(<Welcome title="Welcome g" name="Adobe"/>, document.getElementById("app"));

Preference : use class component if we have state and behaviour

const data =[  
   {  
      "name":"Baked Salmon",
      "ingredients":[  
         {  
            "name":"Salmon",
            "amount":1,
            "measurement":"l lb"
         },
         {  
            "name":"Pine Nuts",
            "amount":1,
            "measurement":"cup"
         },
         {  
            "name":"Butter Lettuce",
            "amount":2,
            "measurement":"cups"
         },
         {  
            "name":"Yellow Squash",
            "amount":1,
            "measurement":"med"
         },
         {  
            "name":"Olive Oil",
            "amount":0.5,
            "measurement":"cup"
         },
         {  
            "name":"Garlic",
            "amount":3,
            "measurement":"cloves"
         }
      ],
      "steps":[  
         "Preheat the oven to 350 degrees.",
         "Spread the olive oil around a glass baking dish.",
         "Add the salmon, garlic, and pine nuts to the dish.",
         "Bake for 15 minutes.",
         "Add the yellow squash and put back in the oven for 30 mins.",
         "Remove from oven and let cool for 15 minutes. Add the lettuce and serve."
      ]
   },
   {  
      "name":"Fish Tacos",
      "ingredients":[  
         {  
            "name":"Whitefish",
            "amount":1,
            "measurement":"l lb"
         },
         {  
            "name":"Cheese",
            "amount":1,
            "measurement":"cup"
         },
         {  
            "name":"Iceberg Lettuce",
            "amount":2,
            "measurement":"cups"
         },
         {  
            "name":"Tomatoes",
            "amount":2,
            "measurement":"large"
         },
         {  
            "name":"Tortillas",
            "amount":3,
            "measurement":"med"
         }
      ],
      "steps":[  
         "Cook the fish on the grill until hot.",
         "Place the fish on the 3 tortillas.",
         "Top them with lettuce, tomatoes, and cheese."
      ]
   }
];

<Recipe ... />

ReactDOM.render(<Menu title="Delicious recipes" recipes={data} />, document.getElementById("app"))

Post lunch ==> 2:00

npx create-react-app customerapp

===========================================


code of Ashish:
function Menu({recepies}) {
  return <div> 
      recepies.map (r =>  <h1> {r.name} </h1>    );

    </div>
}

function Recepie({recepie}) {
  return (<li>{recepie.name}</li>)
}

ReactDOM.render(<Menu title= "Delecious recipes" recepies={data}/>, document.getElementById("app"));

Rishab:
const data =[  
   {  
      "name":"Baked Salmon",
      "ingredients":[  
         {  
            "name":"Salmon",
            "amount":1,
            "measurement":"l lb"
         },
         {  
            "name":"Pine Nuts",
            "amount":1,
            "measurement":"cup"
         },
         {  
            "name":"Butter Lettuce",
            "amount":2,
            "measurement":"cups"
         },
         {  
            "name":"Yellow Squash",
            "amount":1,
            "measurement":"med"
         },
         {  
            "name":"Olive Oil",
            "amount":0.5,
            "measurement":"cup"
         },
         {  
            "name":"Garlic",
            "amount":3,
            "measurement":"cloves"
         }
      ],
      "steps":[  
         "Preheat the oven to 350 degrees.",
         "Spread the olive oil around a glass baking dish.",
         "Add the salmon, garlic, and pine nuts to the dish.",
         "Bake for 15 minutes.",
         "Add the yellow squash and put back in the oven for 30 mins.",
         "Remove from oven and let cool for 15 minutes. Add the lettuce and serve."
      ]
   },
   {  
      "name":"Fish Tacos",
      "ingredients":[  
         {  
            "name":"Whitefish",
            "amount":1,
            "measurement":"l lb"
         },
         {  
            "name":"Cheese",
            "amount":1,
            "measurement":"cup"
         },
         {  
            "name":"Iceberg Lettuce",
            "amount":2,
            "measurement":"cups"
         },
         {  
            "name":"Tomatoes",
            "amount":2,
            "measurement":"large"
         },
         {  
            "name":"Tortillas",
            "amount":3,
            "measurement":"med"
         }
      ],
      "steps":[  
         "Cook the fish on the grill until hot.",
         "Place the fish on the 3 tortillas.",
         "Top them with lettuce, tomatoes, and cheese."
      ]
   }
];

function Menu({title, recipes}) {
  return <div> 
    <h1>
      {title}
      </h1>
     {
      recipes.map(m =>   <Recipes recipe={m}/>) 
     
    </div>
}

function Recipes({recipe}) {
  return <div>
         <h2>
          {recipe.name}
         </h2>
          { 
            recipe.ingredients.map(r => <Ingredients ingredient={r}/>)
          }
          <h3>
            Steps:
         </h3>
          { 
            recipe.steps.map(r => <Steps step={r}/>)
          }
        </div>
}

function Ingredients({ingredient}){
  return <div>
          *
          {ingredient.name}
        </div>
}

function Steps({step}){
  return <div>
    {step}
  </div>
}
ReactDOM.render(<Menu title="Delicious Recipes" recipes={data}/>, document.getElementById("app"));

============================================================================================

npx create-react-app customerapp

create-react-app is an npm executable module which generates a scaffolding code with webpack config and babel

=======

npx create-react-app customerapp --typescript

================


npm i -g create-react-app

create-react-app customerapp

==========


webpack ==> entry ==> index.js

index.js ==> includes App.js

webapck creates a bundle.js and adds it at runtime into index.html

index.html

<div id="root"></div> // <App/> is rendered here

 <div className="App">

without react:  <div class="App">

=============================================

props ==> mechaism ==> data from parent to child

state ==> Object will have state and behaviour

Button 
	caption, color, size, enabled ==> state
	onclick, onmouseover ==> actions ==> behaviour



 class Sample extends Component {

 state = {
		 "name" : "A",
 		 "age" : 22
	}


	...

	task() {

		// async operation
		this.setState({
				"age" : 99
		}, () => {
				// push to server, make an api call, log updates
		});
	}
}



 this.state.customers.map(c => <CustomerRow customer={c} delEvent={this.deleteCustomer.bind(this)} key={c.id} />)
 this.state.customers.map(c => <CustomerRow customer={c} delEvent={(id) => this.deleteCustomer(id)} key={c.id} />)
                
 ============================

 React Testing Library [ RTL] is a wrapper on top of JEST ==> additional assertion apis to test components

 container.querySelector('input[type=text]')

 Angular TestBED ==> Jasmine

getByXXXX() ==> throws exception if not found

queryByXXX() ==> returns null if not found

findByXXX() ==> for Promise based component creation


getByRoleName("button")
getByText(/text/i);
getByPlaceHolderText(...);
getByTestId(..); 

<div data-testid="12"></div>

====================

code Coverage:

npm test -- --coverage

===============

componentDidMount() ==> Life cycle method

component constructor ==> render() [ FCP] ==>  componentDidMount() ==> render();

Any API calls should be done componentDidMount()

=============

react-router-dom ; styled-components; React Context; bootstrap; font awesome

npx create-react-app phoneapp

==============================

while (eventLoop.waitForTask()) {
  const taskQueue = eventLoop.selectTaskQueue()
  if (taskQueue.hasNextTask()) {
    taskQueue.processNextTask()
  }
  const microtaskQueue = eventLoop.microTaskQueue
  while (microtaskQueue.hasNextMicrotask()) {
    microtaskQueue.processNextMicrotask()
  }
}

The job of the event loop is to constantly monitor the message queue (for tasks) and the execution stack and to push the first callback function in-line onto the execution stack, as soon as the stack is empty.


All tasks are not created the same inside message queue. There are macro-tasks and micro-tasks.

Examples of macro-tasks are setInterval, setImmediate, setTimeout, I/O tasks.

Examples of micro-tasks are Promises, process.nextTick.

For each of the ???event loop???, one macro-task is completed out of the macro-task queue. After the respective 
macro-task is complete, the event loop visits the micro-task queue and the entire queue is completed before moving on to the next.
============

class Child extends React.Component {
  render() {
  	console.log("re-render child component.");
  	return (
    	<div>
      		<p>child component which has nothing to do with parent count</p>
    	</div>
  	);
  }
};

class Parent extends React.Component {
  state = {
  count: 0
 };
  
  increment() {
  	this.setState({
  	count: this.state.count + 1
  })
 }
 
  render() {
  	console.log("re-render parent component");
  	return (
    	<>
      		<p>Count: {this.state.count}</p>
      		<button onClick={() => this.increment()}>Increment</button>
      	<Child />
    	</>
  	);
  }
}

ReactDOM.render(<Parent />, document.getElementById('app'));


========================
Day 3:

npx create-react-app phoneapp

customerapp> npm i -D cypress @cypress/instrument-cra

=====================================================

Recap:
	1) createElement, functional components, class components
	2) props and state
	3) React Testing Library [getByXXX, queryByXXX, findByXXX methods of screen]
	using container to access DOM elements using DOM api
	Unit testing
	also mocking the callback [ testing in isolation]

	class Parent  extends Component {
		state = { count : 100}

		render() {
			return <Child value={this.state.count} />
		}

	}

	class Child extends Component {
		render() {
			return <h1> {this.props.value} </h1>
		}
	}
----------------------------

How does event loop work in JavaScript with respect to Browser


event loop

while(true && condition) {
	if(macroTask.getTask()) {

		execute macroTask
	}

	while(microTask.getTasks()) {
		iterate thro all microtsask and push it to call stack
	}
}
=========================================
 
RTL ==> JEST DOM

cypress ==> E2E ==> testing on Browser

angular ==> Protractor [ Seleinum ]

=================================

npx create-react-app phoneapp

phoneapp$ npm i bootstrap styled-components react-router-dom

======================================================================

React Context ==> central store of state and behaviour ==> introduced in version 16.x

Before ReactContext ==> props was the only way data could pass from parent to child

===========

api.js ==> REST calls

redux ==> state managenent ==> single store

context ==> pulls approporiate state from redux and shares with set of components
	product related; user related; cart related ==> Productcontext; UserContext; CartContext ==> state & business logic
====================================

  	let PersonContext = React.createContext();

	class PersonProvider extends React.Component {
		 
    componentDidMount() {
      this.setState({
				"name" : "Arya",
				"email" : "someemail",
				"updateEmail" : this.updateEmail.bind(this)
			});
    }

		updateEmail(email) {
			this.setState({
				"email": email
			});
		}

		render() {
			return <PersonContext.Provider value={{...this.state}}>
					{this.props.children}
			</PersonContext.Provider>
		}
	}


	class App extends React.Component {
		render() {
			return <PersonProvider>
				<First />
				</PersonProvider>
		}
	}

	function First() {
		return <> <h1> I am First !!! <Second /> </h1> </>
	}


	class Second extends React.Component {
		render() {
			return <PersonContext.Consumer>
				{
					value => {
						return <>
							Name : {value.name} <br />
							Email : {value.email} <br />
							<button onClick={()=> value.updateEmail("me@gmail.com")} type="button"> Change </button>

						</>
					}
				}

			</PersonContext.Consumer>
		}
	};

ReactDOM.render(<App/>, document.getElementById("app"))


class App

render () {
	
	return <div> {this.props.children} </div>
}


<App>
	<A/>
	<B/>
	<C/>

</App>

function udpdate() {
	
}
let PersonContxt = React.createContext({"name": "Sam", "update": update})


PhoneApp:
	a) using Context
	b) Routers [ react-router-dom ]
		Why Router?
		SPA ==> different views for different URI

		http://amazon.com/mobile/iPhone11

		http://amazon.com/cart		


		a) for SEO
 
		http://amazon.com/mobile/iPhone11
		http://adobe.com/products

		b) Bookmark
		c) History API [ Prev and Back ] ==> will traverse between views instead of pages

			http://amazon.com/mobile/iPhone11
			http://amazon.com/mobile/pixel3
	c) RWD ==> Responsive web design ==> bootstrap ==> 12 column system
	d) REST calls

========

steps:
1) copy "data.js" from share.zip into "src" folder
2) overwrite "App.css" from share.zip 
3) copy "img" folder into "public"

components:
1) Navbar
2) ProductList
3) Product
4) Cart
5) CartList
6) Details
7) Default

one root element can be returned by jsx

function App() {
  return (
    <div>
    	...
    </div>
  );
}

-----------
function App() {
  return (
    <React.Fragment>
    	<h2></h2>
    	<p></p>
    	<div></div>
    </React.Fragment>
  );
}

-----------------
function App() {
  return (
    <>
    
    </>
  );
}


==========

copy "Button.js" and "Context.js" into "components" folder
replace "Navbar.js" with the one share.zip
 
 full page refresh
 <a href="/"> Adobe </a>

Router: instead of a href use "Link"
 <Link to="/">
                    <i className="navbar-brand">
                        Adobe
                    </i>
 </Link>

Navbar.js ==> styled-compnent button ; bootstrap navbar ; Link for Router  links instead of <a href ="">

=================

 React Developer Tools extension in Chrome
 Redux Developer Tools


==================================================================

Task:

	In Product.js
	clicking on image Details page is rendered
	display title, image, company and info

==========
 
  npx json-server --watch data.json --port 1234

  http://localhost:1234/products

  http://localhost:1234/products/2
============

React ==> 3rd party library ==> http call

fetch()
axios

=======================================================

productApi.js
	will have all our http calls
	getProducts() {
		http
	}

	getProductById(id) {
		http
	}

customerApi.js

=====================================================



class Child extends React.Component {
  render() {
  	console.log("re-render child component.");
  	return (
    	<div>
      		<p>child component which has nothing to do with parent count</p>
    	</div>
  	);
  }
};

class Parent extends React.Component {
  state = {
  count: 0
 };
  
  increment() {
  	this.setState({
  	count: this.state.count + 1
  })
 }
 
  render() {
  	console.log("re-render parent component");
  	return (
    	<>
      		<p>Count: {this.state.count}</p>
      		<button onClick={() => this.increment()}>Increment</button>
      	<Child />
    	</>
  	);
  }
}

ReactDOM.render(<Parent />, document.getElementById('app'));


child component already has props prev sent by parent

when the parent state / props change it will pass then to child [ nextState and nextProps]

============
class Child extends React.Component {
  
  shouldComponentUpdate(nextProps, nextState) {
    console.log(this.props, nextProps);
    if(JSON.stringify(this.props) === JSON.stringify(nextProps)) {
      return false;
    }
    return true;
  }

  render() {
  	console.log("re-render child component.");
  	return (
    	<div>
      		<p>child component which has nothing to do with parent count { this.props.name }</p>
    	</div>
  	);
  }
};

class Parent extends React.Component {
  state = {
  count: 0,
  name : 'Peter'
 };
  
  increment() {
  	this.setState({
  	count: this.state.count + 1
  })
 }
 
  render() {
  	console.log("re-render parent component");
  	return (
    	<>
      		<p>Count: {this.state.count}</p>
      		<button onClick={() => this.increment()}>Increment</button>
      	<Child name={this.state.name}/>
    	</>
  	);
  }
}

ReactDOM.render(<Parent />, document.getElementById('app'));

=================

class Child extends React.PureComponent {
   
  render() {
  	console.log("re-render child component.");
  	return (
    	<div>
      		<p>child component which has nothing to do with parent count { this.props.name }</p>
    	</div>
  	);
  }
};

if props is primitive and not array or object

===============================================
function Child(props) {
   	console.log("re-render child component.");
  	return (
    	<div>
      		<p>child component which has nothing to do with parent count { props.name }</p>
    	</div>
  	);
 };

let MemoChild = React.memo(Child); // PureComponent

class Parent extends React.Component {
  state = {
  count: 0,
  name : 'Peter'
 };
  
  increment() {
  	this.setState({
  	count: this.state.count + 1
  })
 }
 
  render() {
  	console.log("re-render parent component");
  	return (
    	<>
      		<p>Count: {this.state.count}</p>
      		<button onClick={() => this.increment()}>Increment</button>
      		<MemoChild name={this.state.name}/>
    	</>
  	);
  }
}

ReactDOM.render(<Parent />, document.getElementById('app'));

================================================================================
Here is a simple break down of main concepts
Stores form your data sources. A store is basically a simple ES6 class. Eventually state is derived from data sources automagically by MobX through ES6 decorators.
Store exposes observable fields, to which an observer reacts.
Store additionally can expose derived observable fields as well. They are pure functions on observable fields. MobX calls them computed fields.
Store can change values of observable fields via actions. This is the only way MobX allows you to change state.


import { observable, action } from "mobx";
export default class CounterStore {
  @observable count = 0;
  @action increment() {
    this.count += 1;
  }
  
  @action decrement() {
   this.count -= 1;
  }
}

import { observable, action, computed } from "mobx";
export default class UserStore {
  @observable firstName = "Banu";
  @observable lastName = "Prakash";

  
  @action data(data: Object) {
    if (data.firstName) {
      this.firstName = data.firstName;
    }
    if (data.lastName) {
      this.lastName = data.lastName;
    }
  }
 
  @computed get fullName(): string {
    return `${this.firstName} ${this.lastName}`;
  }
}


import { Provider } from "mobx-react";
export default class App extends Component {
  render() {
    return (
      <Provider {counterStore: new CounterStore(), userStore: new UserStore()}>
        <Home />
      </Provider>
    );
 }
}

import { observer, inject } from "mobx-react";
@inject("counterStore")
@observer
class Counter extends Component {
  render() {
    return <>Count: {this.props.counterStore.count}</>;
  }
}

@inject("userStore")
@observer
class FullName extends Component {
   render() {
     return <>FullName: {this.props.userStore.fullName}</>;
   }
}

+++++++++++++++++++++++++++++++++++++++++++++++++++++

let Child = (props) =>   {
  console.log("re-render child component.")
  return (
    <div>
      <p>child component which resets count</p>
      <button onClick={props.reset}>Reset Count</button>
    </div>
  );
}

const MemoChild = React.memo(Child);


const Parent = () => {
  const [count, setCount] = React.useState(0);
  console.log("re-render parent component");

  const resetCount = React.useCallback(() => {
    setCount(0);
  }, [setCount]);
  return (
    <main>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count=>(count+1))}>Increment</button>
      <MemoChild reset={resetCount} />
    </main>
  )
}

ReactDOM.render(<Parent />, document.getElementById('app'));

===========


Day 4:
======
Day 3: Context, router, lifecycle methods, PureComponent, React.memo()

HOC, Rerefernce, React Hooks, State Management, Performance profile


SampleComponent

render() {
	return (
	<Parent>
		{this.props.children}
	</Parent>
	);
}

usage :
	<SampleComponent title="Hello">
			<A/>
			<B/>
	</SampleComponent>

use case 2:

	<SampleComponent>
			<C/>
			<D/>
	</SampleComponent>
=====================================

High Order Component : HOC ==> HOF

function Child() {
	
}
MemoChild = React.memo(Child);

Why HOC?
 cross-cutting concern ==> code scattering and code tangling


 class ProductList extends Component {
 	...
 	render() {
 		if(this.props.isLoading) {
 			return <img src="loader.gif" />
 		} else {
 			this.props.products.map ...
 		}
 	}
}

 class OrderList extends Component {
 	...
 	render() {
 		if(this.props.isLoading) {
 			return <img src="loader.gif" />
 		} else {
 			this.props.orders.map ...
 		}
 	}
}

AppComponent {
	productloading: false
	products 
	orders
	componentDidUpdate() {
			async call to server axios
	}

	render() {
		<ProductList isLoading={productloading} products={products} />

	}
}

=================
// HOC

const withCounter = (WrappedComponent) => {
	return class extends React.Component {
		constructor(props) {
			super(props);
			this.state = {
			count : 0
		  }
		}
		increment = () => {
				this.setState( {
					count : this.state.count + 1;
				})
		}
		render() {
			return {
				<WrappedComponent count={this.state.count} increment={this.increment} />
			}
		}
	}
}

class DivComponent extends React.Component {
	render() {
		return <>
				{this.props.count}
				<button type="button" onClick={() => this.props.increment}>move</button>
				</>
			}
	}
}


class ImageComponent extends React.Component {
	render() {
		return <>
				{this.props.count}
				<img src="" onMouseover={() => this.props.increment}>move</button>
				</>
			}
	}
}


let WrappedDiv = withLoader(withCounter(DivComponent));
function App() {
	return <>
		<WrappedDiv/>
	</>
}
=================
const withCounter = (WrappedComponent) => {
	return class extends React.Component {
		constructor(props) {
			super(props);
			this.state = {
			count : 0
		  }
		}
		increment = () => {
				this.setState( {
					count : this.state.count + 1
				})
		}
		render() {
			return <WrappedComponent count={this.state.count} increment={this.increment} />
			 
		}
	}
}

class DivComponent extends React.Component {
	render() {
		return <>
				{this.props.count}
				<button type="button" onClick={() => this.props.increment()}>move</button>
				</>
			}
}
class ImgComponent extends React.Component {
	render() {
		return <>
				{this.props.count}
				<div  onMouseOver={() => this.props.increment()}> image move</div>
				</>
			}
}



let WrappedDiv =  withCounter(DivComponent);
let WrappedImg =  withCounter(ImgComponent);
function App() {
	return <>
		<WrappedDiv/>
    <WrappedImg />
	</>
}

ReactDOM.render(<App/>, document.getElementById("app"))

==========================================================================

React Reference:

class App extends React.Component {
	emailRef = React.createRef(); // reference

	render() {
		return (
			<>
				<input type="text" ref={this.emailRef} />
				<button onClick={() => this.doTask()}> Click </button>
			</>
		)
	}

	doTask() {
		console.log(this.emailRef.current.value);
		this.emailRef.current.focus();
	}
}
ReactDOM.render(<App/>, document.getElementById("app"))
==================

React Reference:


class App extends React.Component {
	render() {
		return (
			<>
				<input type="text" ref={input => this.emailRef = input} />
				<button onClick={() => this.doTask()}> Click </button>
			</>
		)
	}

	doTask() {
		console.log(this.emailRef.current.value);
		this.emailRef.current.focus();
	}
}
ReactDOM.render(<App/>, document.getElementById("app"));

========================

Forward Reference:

const EmailInput = React.forwardRef((props, ref) => {
	<input type="text" ref={ref} {...props} />
});


class App extends React.Component {
	emailRef = React.createRef(); // reference
	render() {
		return (
			<>
				<EmailInput  ref={this.emailRef} />
				<button onClick={() => this.doTask()}> Click </button>
			</>
		)
	}

	doTask() {
		console.log(this.emailRef.current.value);
		this.emailRef.current.focus();
	}
}
ReactDOM.render(<App/>, document.getElementById("app"));

==========================================================================

React Hooks: Available from React 16 version onwards

functional components vs class components
	state, behaviour, life cycle methods ==> class components

	class components are heavy ==> extends React.Component

React Hooks to be used in Functional components as an alternate to using Class Component

class App extends Component {
	state = {
		count : 0,
		user : ""
	}

	setCount() {
		//	
	}
}

React Hooks:
1) useState


function App() {
	let [count, setCount] = React.useState(0);
	let [user, setUser] = React.useState("Peter");
	return (
		<>
		Count {count} {user}<br />
		<button onClick={() => setCount(count + 1)}> Click </button> <br />
		</>
	)
}
ReactDOM.render(<App/>, document.getElementById("app"));

=================

2) useReducer
	if state is complex object and conditional mutations

	let initalState = {count : 0};

	let countReducer = (state, action) => {

		switch(action.type) {
			case "INCREMENT" : return {count : state.count + action.payload};
			case "DECREMENT" : return {count : state.count -1};
			default : return state;
		}
	}


function App() {
	let [state, dispatch] = React.useReducer(countReducer, initalState);
	 
	 function handleIncrement() {
	 	let action = {"type": "INCREMENT", payload : 10};
	 	dispatch(action);
	 }
	return (
		<>
		Count {state.count}  <br />
		<button onClick={handleIncrement}> Click </button> <br />
		</>
	)
}
ReactDOM.render(<App/>, document.getElementById("app"));

===============

let initalState = {cart : [], total: 0};

let countReducer = (state, action) => {
		switch(action.type) {
			case "ADD_TO_CART" : return {cart : state.cart.push(action.payload), total : state.total};
			case "DECREMENT" : return {count : state.count -1};
			default : return state;
		}
	}

====================
 
3) useContext()
let productContext = React.useContext();

4) useEffect()


function App() {
	let [count, setCount] = React.useState(0);
	
	setInterval(() => {
		setCount(count + 1);
	}, 100);
	return (
		<>
			Count {count} <br />
		</>
	)
}
ReactDOM.render(<App/>, document.getElementById("app"));

every 100 ms a new timer is started.

setInterval , REST call, any promise based api ==> side effects

any side effect code should be used in useEffect()

----



function App() {
	let [count, setCount] = React.useState(0);
	
	let [user, setUser] = React.useState("");

	// componentDidUpdate
	React.useEffect(() => {
		console.log("called effect 1 ", count)
	}); 

	// componentDidMount
	React.useEffect(() => {
		console.log("called effect 2", count)
	}, []); 

	// called only on user change
	React.useEffect(() => {
		console.log("called effect 3", count)
	}, [user]); 

	 function handleIncrement() {
	 	 setCount(count + 1);
	 }

	return (
		<>
			Count {count} <br />
			<button onClick={handleIncrement}> Click </button> <br />
		</>
	)
}
ReactDOM.render(<App/>, document.getElementById("app"));
==================


let Child = (props) =>   {
  console.log("re-render child component.")
  return (
    <div>
      <p>child component which resets count</p>
      <button onClick={props.reset}>Reset Count</button>
    </div>
  );
}

const MemoChild = React.memo(Child);


const Parent = () => {
  const [count, setCount] = React.useState(0);
  console.log("re-render parent component");

  const resetCount =  () => {
    setCount(0);
  };

  return (
    <main>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count=>(count+1))}>Increment</button>
      <MemoChild reset={resetCount} />
    </main>
  )
}

ReactDOM.render(<Parent />, document.getElementById('app'));

===========

5) useCallback
	is to memoize a function


let Child = (props) =>   {
  console.log("re-render child component.")
  return (
    <div>
      <p>child component which resets count</p>
      <button onClick={props.reset}>Reset Count</button>
    </div>
  );
}

const MemoChild = React.memo(Child);


const Parent = () => {
  const [count, setCount] = React.useState(0);
  console.log("re-render parent component");

  const resetCount = React.useCallback( () => {
    setCount(0);
  }, [setCount]);

  return (
    <main>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count=>(count+1))}>Increment</button>
      <MemoChild reset={resetCount} changed={changed}/>
    </main>
  )
}

ReactDOM.render(<Parent />, document.getElementById('app'));

======

6) useMemo() to memoize a variable

=======================

Errorboundary:

class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false, error: null, errorInfo : null };
  }
   componentDidCatch(error, errorInfo) {
     this.setState({
     	hasError: true,
     	error,
     	errorInfo
     })
  }
  render() {
    if (this.state.hasError) {
      return <h1>Something went wrong.</h1>;
    }
    return this.props.children; 
  }
}

function App() {
	return (
		<ErrorBoundary>
			<Navbar />
			<First />
			<List />
		</ErrorBoundary>
	)
}

=============================================================
"prop-types": "^15.7.2",

import PropTypes from 'prop-types';

ShoppingList:
 <List
              items={items}
              removeListItem={this.removeListItem}
              removeAllListItems={this.removeAllListItems}
            />


List:
List.propTypes = {
  removeListItem: PropTypes.func.isRequired,
  removeAllListItems: PropTypes.func.isRequired,
  items: PropTypes.array.isRequired,
};

=============

State management with React Context

State management using Flux architecture
=================

1) npm i

2) npm start

test your application
go thro the code

3) stop the server

4) 

npm i flux

npm i object-assign

==================

Resume @ 2:00




