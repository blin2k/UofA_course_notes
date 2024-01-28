ES6 standard
- Ecma Script
- Ecma creates a wide range of global information and communications technology standards
- Java Script adheres to Ecma's specification EcmaScript6
	- new features
		- let
			- restrict the scope of var within the block where they are declared
		- const
			- declare constants whose values cannot be changed
		- arrow functions
			- allow functions to be declared like var
			- shorter and cleaner way
			- `const sayHi = ()=> console.log("Hi")`
			- `const twoParamsWithReturn = (first, second)=>{return "this"+first+"and"+second}`
		- promise
			- represents the eventual completion of an asynchronous operation and its return value
				- invoke -> pending
				- successfully executed -> fulfilled
				- fail -> rejected
		- class
			- makes OOR feasible
			- template or blueprint for creating objects
			- are built on prototypes in JS
			- inheritance
				- `class Square extends Rec{}`

```js
let promiseArg = (resolve, reject)=>{
	setTimeout(()=>{
		let curTime = new Date.getTime();
		if (curTime % 2 === 0){
			resolve()
		}
		else{
			reject("you fail")
		}
	}, 2000)
};
let myPromise = new Promise(promiseArg);
```

this is an object function
```js
function Person(name, age){
	this.name = name;
	this.age = age;
	return this;
}
let jack = Person('jack', 23)
console.log(jack)
console.log(jack.name+"'s age is"+jack.age.toString())
```

class with a constructor
```js
class Rec{
	constructor(h, w){
		this.height = h;
		this.width = w;
		console.log("area="+(this.height*this.width).toString())
	}
}
// `new` will send the params to the constructor
let myRec = new Rec(10, 5)
```

# Front-End Frameworks
- framework for client side
- open-source libs
	- html
	- js
	- css
- AngularJS 
	- from google
	- based on html and js
	- directives to make html dynamic
- Vue.js
	- uses virtual DOM
		- document object model
	- lightweight and fast
- React
	- DOM

## DOM
![[Pasted image 20240126224242.png]]
## JavaScript XML
- JSX
- resembles HTML
- can be compiled and interpreted as JS by Babel
- is embedded inside special script tags

## Packages
- react
	- components
	- states
	- properties
- reactDOM
	- glue between react and the dom
- babel
	- compile and interpret jsx

## page
```html
class Mycomp extends React.Component{
	render(){
		return <h1>This is my own component name {this.props.name}</h1>;
	}
}
ReactDom.render(<Mycomp name="myBrandNewComp"/>, document.getElementById('comp1'));
```

---
# Creating a React App
`npx create-react-app todoapp`
- node package execute
- the app name should be in lowercase, like `todoapp`
- this creates a React app as a directory for you
- `src` folder contains the main files that you will change
	- app.js
		- contains app, which is the root react component that you add
	- index.js
		- where you add the app component to the HTML

`npm start`
- start the server on port 3000

---
# React Components
- types
	- functional
		- JS function that returns JSX
```js
function App(props){
	return {
		<div>
			<button onClick={props.clickEvent}>Click Me!</button>
		</div>
	};
}
export default App;
```

	- class
		- JS class that inherits React.Component class

```js
// import the module
import React from 'react';
// create the App class
class App extends React.Component{
	constructor(props){
		// pass the props to the superclass
		super(props)
	}
	// override the render method
	// if the "Click Me" button is clicked, it will call the onClick function, which is 'clickEvent'
	render(){
		return <button onClick={this.props.clickEvent}>Click Me!</button>;
	}
}
export default App;
```

```js
import React from 'react';
import ReactDom from 'react-dom';
import App from './App';

ReactDom.render(
	<React.StrictMode>
		// props
		<App color="blue" size="25" clickEvent={
		()=>(alert("You clicked me!"))
		}/>
	</React.StrictMode>
	document.getElementById('root')
);
```

class component states
- props
	- set from outside the class
- state
	- internal to the class 

# Passing Data and States between Components
component phases
- mounting
	- component creation
		- `constructor()`
		- `getDerivedStateFromProps()`
			- only when state depends on the changes to props
		- `render()`
		- `componentDidMount()`
			- invoked immediately after a component is mounted or inserted into the DOM tree 
- updating
	- component change
		- `getDerivedStateFrom Props()`
			- same above
		- `shouldComponentUpdate()`
			- the default is `true`
			- every time a state is changed, this method is called to check if the component should update
		- `render()`
		- `getSnapshotBeforeUpdate()`
			- invoked before the changes are rendered
			- value returned by this will be passed as a parameter to the function below
		- `componentDidUpdate()`
			- right after updating occurs
- unmounting
	- component removal
	- components
		- AppInner
			- rendered inside App with a state
			- `componentWillUnmount()`
		- App
			- `componentDidUnmount()
				- will be handled first

## Passing data
- parent to child
	- props
- child to parent
	- callbacks
- between siblings
	- redux

```js
class App extends Reacts.Component{
	// local data
	state={msg:''}
	// customized callback function
	// put the input into the state
	func1=(childData)=>{
		this.setState({msg: childData})
	}

	render(){
		return(){
			<div>
				// the child AppInner will have a prop function called parentCallback, which is actually func1
				<AppInner parentCallback={this.func1}/>
				// display this message
				<p>{this.state.msg}</p>
			</div>
		};
	}
}

class AppInner extends React.Component{
	// every 1s passed, call the callback function with current time
	// where the callback is func1: setting the state
	sendData= ()=>{
		setInterval(()=>{
			const currTime = Date();
			this.props.parentCallback(currTime);
		}, 1000);
	}
	// every time the component is ready, call the sendData()
	componentDidMount(){
		this.sendData();
	}
	render(){
		return <div></div>
	}
}
```

# Connecting React to External Services
- HTTP
	- GET / POST / UPDATE / DELETE
- promise server call