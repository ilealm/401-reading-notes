[ HOME ](README.md)
# Read 37 - ES6 and React 1

# Sources
- [ES6 Syntax and Feature Overview](https://www.taniarascia.com/es6-syntax-and-feature-overview/)
- [React](https://reactjs.org/docs/hello-world.html)



# ES6 Syntax and Feature Overview (AKA ECMAScript 2015)

**Variable declaration**

ES6 introduced the **let** keyword, which allows for block-scoped variables which cannot be hoisted or redeclared.
`let x = 0`


**Constant declaration**

ES6 introduced the **const** keyword, which cannot be redeclared or reassigned, but is not immutable.
`const CONST_IDENTIFIER = 0 // constants are uppercase by convention`

**Arrow functions**

The arrow function expression syntax is a shorter way of creating a function expression. Arrow functions do not have their own this, do not have prototypes, cannot be used for constructors, and should not be used as object methods.
```
let func = (a) => {} // parentheses optional with one parameter
let func = (a, b, c) => {} // parentheses required with multiple parameters
```

**Template literals**

Concatenation/string interpolation
```
let str = `Release Date: ${date}`
```


**Multi-line strings**

Using template literal syntax, a JavaScript string can span multiple lines without the need for concatenation.
```
let str = `This text
            is on
            multiple lines`
```


**Implicit returns**

The return keyword is implied and can be omitted if using arrow functions without a block body.

`let func = (a, b, c) => a + b + c // curly brackets must be omitted`

**Key/property shorthand**


ES6 introduces a shorter notation for assigning properties to variables of the same name.
```
let obj = {
  a,
  b,
}
```

**Method definition shorthand**

The function keyword can be omitted when assigning methods on an object.
```
let obj = {
  a(c, d) {},
  b(e, f) {},
}
obj.a() // call method a
```

**Destructuring (object matching)**
Use curly brackets to assign properties of an object to their own variable.
`let { a, b, c } = obj`

**Array iteration (looping)**
A more concise syntax has been introduced for iteration through arrays and other iterable objects.
```
for (let i of arr) {
  console.log(i)
}
```

**Default parameters**
Functions can be initialized with default parameters, which will be used only if an argument is not invoked through the function.
```
let func = (a, b = 2) => {
  return a + b
}
func(10) // returns 12
func(10, 5) // returns 15
```
**Spread syntax**
Spread syntax can be used to expand an array.

```
let arr1 = [1, 2, 3]
let func = (a, b, c) => a + b + c

console.log(func(...arr1)) // 6
```

**Classes/constructor functions**
ES6 introducess the class syntax on top of the prototype-based constructor function.

```
class Func {
  constructor(a, b) {
    this.a = a
    this.b = b
  }

  getSum() {
    return this.a + this.b
  }
}

let x = new Func(3, 4)
x.getSum() // returns 7
```

**Inheritance**
The extends keyword creates a subclass.
```
class Inheritance extends Func {
  constructor(a, b, c) {
    super(a, b)

    this.c = c
  }

  getProduct() {
    return this.a * this.b * this.c
  }
}

let y = new Inheritance(3, 4, 5)
y.getProduct() // 60
```

**Modules - export/import**
Modules can be created to export and import code between files.
```
<script src="export.js"></script>
<script type="module" src="import.js"></script>
```

**Promises/Callbacks**
Promises represent the completion of an asynchronous function. They can be used as an alternative to chaining functions.

```
let doSecond = () => {
  console.log('Do second.')
}

let doFirst = new Promise((resolve, reject) => {
  setTimeout(() => {
    console.log('Do first.')

    resolve()
  }, 500)
})

doFirst.then(doSecond)
```

___
# React
___

> React is a JavaScript library

### Hello World
```
ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('root')
);
```

### Introducing JSX
- SX produces React “elements”.
- React separates concerns with loosely coupled units called “components” that contain both.
- React doesn’t require using JSX, but most people find it helpful as a visual aid when working with UI inside the JavaScript code. It also allows React to show more useful error and warning messages.
- Since JSX is closer to JavaScript than to HTML, React DOM uses camelCase property naming convention instead of HTML attribute names.

`const element = <h1>Hello, world!</h1>;`

This funny tag syntax is neither a string nor HTML.

It is called JSX, and it is a syntax extension to JavaScript. We recommend using it with React to describe what the UI should look like. 

#### Specifying Children with JSX
If a tag is empty, you may close it immediately with />, like XML:

`const element = <img src={user.avatarUrl} />;`
JSX tags may contain children:
```
const element = (
  <div>
    <h1>Hello!</h1>
    <h2>Good to see you here.</h2>
  </div>
);
```

#### JSX Prevents Injection Attacks
By default, React DOM escapes any values embedded in JSX before rendering them. Thus it ensures that you can never inject anything that’s not explicitly written in your application.

It is safe to embed user input in JSX:
```
const title = response.potentiallyMaliciousInput;
// This is safe:
const element = <h1>{title}</h1>;
```


## Rendering Elements
- An element describes what you want to see on the screen

Let’s say there is a <div> somewhere in your HTML file:

`<div id="root"></div>`

We call this a “root” DOM node because everything inside it will be managed by React DOM.
To render a React element into a root DOM node, pass both to ReactDOM.render():

#### React Only Updates What’s Necessary
React DOM compares the element and its children to the previous one, and only applies the DOM updates necessary to bring the DOM to the desired state.

## Components and Props (which stands for properties) 

Components let you split the UI into independent, reusable pieces, and think about each piece in isolation.

Props are Read-Only.

The simplest way to define a component is to write a JavaScript function:
```
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

#### Rendering a Component
When React sees an element representing a user-defined component, it passes JSX attributes and children to this component as a single object. We call this object “props”.

For example, this code renders “Hello, Sara” on the page:
```
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```

#### Composing Components
Components can refer to other components in their output. This lets us use the same component abstraction for any level of detail. A button, a form, a dialog, a screen: in React apps, all those are commonly expressed as components.

```
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

function App() {
  return (
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
  );
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

#### Extracting Components
Don’t be afraid to split components into smaller components.
```
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <img className="Avatar"
          src={props.author.avatarUrl}
          alt={props.author.name}
        />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

## State and Lifecycle



#### Converting a Function to a Class
You can convert a function component like Clock to a class in five steps:

Create an ES6 class, with the same name, that extends React.Component.
1. Add a single empty method to it called render().
1. Move the body of the function into the render() method.
1. Replace props with this.props in the render() body.
1. Delete the remaining empty function declaration.
```
class Clock extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.props.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```
In applications with many components, it’s very important to free up resources taken by the components when they are destroyed.

Whenever something is rendered to the DOM for the first time. This is called “mounting” in React, We also want to clear that whenever the DOM produced when something is removed. This is called “unmounting” in React. These methods are called “lifecycle methods”.

The **componentDidMount()** method runs after the component output has been rendered to the DOM.

### Using State Correctly
There are three things you should know about setState().

1. Do Not Modify State Directly
1. State Updates May Be Asynchronous
1. State Updates are Merged

### Handling Events

React events are named using camelCase, rather than lowercase.
```
<button onClick={activateLasers}>
  Activate Lasers
</button>
```

Another difference is that you cannot return false to prevent default behavior in React. You must call preventDefault explicitly. 
```
<a href="#" onclick="console.log('The link was clicked.'); return false">
  Click me
</a>
```

#### Passing Arguments to Event Handlers
Inside a loop, it is common to want to pass an extra parameter to an event handler. For example, if id is the row ID, either of the following would work:
```
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
```


