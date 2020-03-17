# ReactJS Notes and stuff

***NOTE*** This repo contains [git submodules](https://git-scm.com/book/id/v2/Git-Tools-Submodules) for each of the projects that I have worked on while doing the course. To clone, push, and all the other git stuff you'll have to consider those directories.

## Table of Contents

[React Key Concepts](#react-key-concepts)

[React Basics](#react-basics・３月６日・３月１３日・３月１５日)

- [Create React App](#6-7---create-react-app)
- [Class Components](#10---class-components)
- [Single Page Applications](#14---single-page-applications)
- [Fetching Content](#15---fetching-content)
- [Card List Component](#18---card-list-components)
- [Card Component](#19---card-component)
- [Breaking into Components](#20---breaking-into-components)
- [State vs Props](#21---state-vs-props)
- [Search Field](#22---search-field)
- [React Events](#-23---react-events)
- [Filtering State](#24---filtering-state)
- [Search Box Component](#26---search-box-component)
- [Where to put state](#27---where-to-put-state)
- [Class Methods and Arrows](#28---class-methods-and-arrow-functions)
- [Exercise Event Binding and this](#29---exercise-even-binding)

## React Key Concepts

### 1-2 - React Concepts, Birth of React

Before React (2013) <
Just JS, HTML, CSS  Basic, Browser compatibly issues
jQuery API that let devs interact and modify the DOM
SPA: Single Page Application

AngularJS Angular container-fied javascript models
AngularJS became Angular (sans JS)

### 3 - Declare vs. Imperative

- Imperative

> React modifies DOM so devs don’t have too.
DOM: Document Object Model
What the browser uses to render website/app
Tree rep of webpage
Prior to react interaction with the DOM was left to the dev or libraries (Ajax and such)
Imperative programing is where you directly modify the app in response to user events
Becomes difficult to see differences between relationships and edge cases

- Declarative

> React says DOM manipulation is resource intensive. Requires 2 large operations: Repaint (change element and add) Reflow (recalculate position of elements).
In React dev states what the page should look like and React manages the DOM.
Dev ‘declares’ the page and React manages DOM

### 4 - Component Architecture

Components allow for higher code reusability with the use of custom HTML-like elements
To use the react dev tools - have to be using FF/Chrome and be on react based website

### 5 - One way data flow

Unidirectional data flow
Virtual DOM
  React creates a virtual Dom which is essentially just a phat java script obj that contains all the data on how the website should look. Can be visualized to looks like a Dom but really its just a JS object
  Data only flows one way; away from the app ‘state’. This means the state has to change first in order for the application to change.
  State changes can only flow ‘down’ ie: away from the ‘state’ that changed.

### 6 - UI Library

React is essentially just a UI library which means the concepts are limited to managing Dom interactions. It is unbiased to which toolset you use. You can use it any where too.

### 7 - How to be a good react dev

*Basic shit*

## React Basics・３月６日・３月１３日・３月１５日

### 6-7 - Create React App

> The first few vids were just basic garbage stuff.

#### Create react app

React commands are run off the npx command which comes bundled with node. One of the commands is the create react app which creates at startup template for react apps.

Also, it handles javascript version translations for browser compatibility. Babel/webpack...

#### yarn-npm common translations

``` txt
  Install dependencies from package.json: npm install == yarn

  Install a package and add to package.json: npm install package --save == yarn add package

  Install a devDependency to package.json: npm install package --save-dev == yarn add package --dev

  Remove a dependency from package.json: npm uninstall package --save == yarn remove package

  Upgrade a package to its latest version: npm update --save == yarn upgrade

  Install a package globally: npm install package -g == yarn global add package
```

#### Basic flow of React's architecture

`App.js` -> `index.js` -> `index.html`

`App.js` is where the heart of the project lives. Most of the functionality of the webapp will be somehow coupled to this file. Contains a `function App() {...}` that returns a single `<div>`.

`index.js` imports the `App()` function from `App.js` and invokes the function by passing it as an argument into its single line: `ReactDom.render(...)`. This function takes two arguments: `<App />, document.getElementById('root')`. The first one is the `App(...)` function and the second one is a call to a function that'll pull from the DOM the element *root*.

`index.html` is where this *root* element can be found. Within the `<body>` of this file React will replace the element with the contents that is returned from the `App.js` `App()` function.

``` html
<body>
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div> <!-- This is where react injects stuff too -->
    <!--
      This HTML file is a template.
      If you open it directly in the browser, you will see an empty page.

      You can add webfonts, meta tags, or analytics to this file.
      The build step will place the bundled scripts into the <body> tag.

      To begin the development, run `npm start` or `yarn start`.
      To create a production bundle, use `npm run build` or `yarn build`.
    -->
  </body>
```

`React from 'react'`: React lets us write JSX (HTML) like syntax.

`ReactDOM from 'react-dom'`: Interacts with HTML DOM.

#### Babel & webpack

Babel converts current javascript into more common versions.

webpack lets us write modularized javascript code.

Running `yarn build` from within react app dir runs all of this.

### 10 - Class Components

```JavaScript
function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}
```

``` JavaScript
/**
 * Classes can be created that are inherit from Component.
 * These have render function which will define how the component
 * will be rendered.
 * We can just copy paste the return(...) from above and have the
 * class' render(...) return the same data and it will function
 * in pretty much the same manner.
 */
class App extends Component {
  render () {
    return (
      <div className="App">
        <header className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <p>
            Edit <code>src/App.js</code> and save to reload.
          </p>
          <p>
            Test
          </p>
          <a
            className="App-link"
            href="https://reactjs.org"
            target="_blank"
            rel="noopener noreferrer"
          >
            Learn React
        </a>
        </header>
      </div>
    );
  }
}
```

``` JavaScript
/**
   * React components have a state value which describes some
   * current status of the current environment.
   *
   * It exists in the Component class and it is inherited.
   *
   * The state value can be modified by using the setState(...)
   * which is also inherited from parent Component class.
   *
   * You CANNOT modify the state value directly. You MUST use
   * the .setState(...) function to modify the state. Gotta keep
   * that unidirectional dataflow.
   */
  constructor() {
    super();

    this.state = {
      string: 'This is test from state'
    };
  }
```

Within JSX {...} indicate JavaScript code.

All HTML elements within react have `onClick` attribute.

``` JavaScript
<p>
  { this.state.string }
</p>
<button onClick={ () => this.setState( { string: 'buby' } )}>
  click me plz
</button>
```

### 11 - JSX

HTML like syntax for JavaScript. It is really just JavaScript. eg: HTML - `onclick` JSX - `onCLick`.

### 12 - Dynamic Content

It is a good idea to have some sort of unique key for attributes that you might update. Keeps updating costs low.

``` JavaScript
constructor() {
  super();

  this.state = {
    string: 'This is test from state',
    people: [
      {
        name: 'Bill',
        id: '1'
      },
      {
        name: 'Jim',
        id: '2'
      },
      {
        name: 'Jane',
        id: '3'
      }
    ]
  };
}

render() {
  return (
    <div className='App'>
      {
        this.state.people.map( person => {
          return (
            <h1 key={ person.id }> {person.name} </h1>
          );
        })
      }
    </div>
  )
}
```

### 14 - Single Page Applications

Foreshadowing...

### 15 - Fetching Content

Life cycle methods are functions that are called at different stages
of an application's render (automatically).

``` JavaScript
async componentDidMount() {
  const resp = await fetch('https://jsonplaceholder.typicode.com/users'); // fetch
  let usrs = await resp.json(); // [returned promise].json() also returns promise as body not 100 to be loaded.
  console.log(usrs);

  await this.setState({ people: usrs });
}
```

Above code can also be written as:

``` JavaScript
componentDidMount() {
  fetch('...').then(
    resp => {
      resp.json();
    }).then(usr =>
      this.setState({ people: usr });
    })
}
```

*Following taken from [here](https://stackoverflow.com/questions/32721850/why-is-the-response-object-from-javascript-fetch-api-a-promise)...*

> If your question is "why does response.json() return a promise?" then @Bergi provides the clue in comments: "it waits for the body to load". If your question is "why isn't response.json an attribute?", then that would have required fetch to delay returning its response until the body had loaded, which might be OK for some, but not everyone. This polyfill should get you what you want:

``` JavaScript
var fetchOk = api => fetch(api)
  .then(res => res.ok ? res : res.json().then(err => Promise.reject(err)));
then you can do:
```

``` JavaScript
fetchOk(API)
  .then(response => response.json())
  .catch(err => console.log(err));
The reverse cannot be polyfilled.
```

### 17 - Architecting App

Components can be built in 2 ways: functions or Classes.

``` text
-
|-- src
  |-- components
    |-- card
        |-- card.component.jsx
        |-- card.component.css
  |--...
```

Basic folder architecture is up to personal preference but JavaScript/TypeScript files can have ***x*** appended to their extension to indicate that they contain JSX.

After running a react build all files are smushed together in the end.

### 18 - Card list components

Components (functional?) have accept a *`props`* param. This param is what ever argument is called with the component is being invoked. Eg: `<SomeComponent BackGround='somePick.jpg'>` invokes the **SomeCompont** with the argument BackGround. This means the component's props will be BackGround with value of somePick.jpg.

Component's props also have child objects. All props have children, but if no children are init when the component is being used the value will be null. Children are whatever will be called inside of a given component. Eg:

``` JavaScript
<CardList name='billy'> // <--- CardList component will have name be param
  <h1>BudBuh</h1> // <-- Will have child of H1 object with value of BudBuh
</CardList>

// ...usage...
export const CardList = (props) => {
  console.log("dank: " + props);

  return <div>{ props.children } </div>
}

```

This idea of children can be really useful when applying styes to a particular component. You can take some data pass it to a component and then have the component apply a style. The usage below passes a map of data to a component...

``` Java Script
<div className='App'>
  <CardList name='billy'>
    {
      this.state.people.map(person => {
        return (
          <h1 key={person.id}> {person.name} </h1>
        );
      })
    }
  </CardList>
</div>
```

and then the component uses it's own CSS to apply a defined style to the data; displaying it in a nice fashion.

``` JavaScript
export const CardList = (props) => {
  return <div className='card-list'> { props.children } </div>
}
```

### 19 - Card component

- card-list.component.jsx

``` JavaScript
export const CardList = (props) => {
  return <div className='card-list'>
    {
      props.people.map(person => {
        console.log(person)
        return (
          <Card key={person.id} person={person}/> // This is using the Card com
        );
      })
    }
  </div>
}

```

- card.component.jsx

``` JavaScript
export const Card = (props) => ( // TODO what is diff between ( and {
  <div className='card-container'>
    <img
      alt="person"
      src={`https://robohash.org/${props.person.id}?set=set2180x180}`}
    />
    <h2> {props.person.name} </h2>
    <p> {props.person.email} </p>
  </div>
)
```

The Following is taken from [here](https://stackoverflow.com/questions/49895339/difference-between-arrow-functions-with-parentheses-or-brackets):
> The "basic" form is with curly braces, just like regular functions:
>() => {
>...
>}
>However, arrow functions allow one special case shorthand:
>
>() => plain expression
>If you don't use curly braces, you may use one plain expression instead, with an implicit return. I.e. these two are equivalent:
>
>() => { return 42; }
>() => 42
>So your version using parentheses counts as the single expression version and the return value of console.log will be returned (which is undefined either way though), whereas it won't on the version using curly braces.

I was getting this error `Line 6:3:  Expected an assignment or function call and instead saw an expression  no-unused-expressions` when I was using `{}` instead of `()`.

``` JavaScript
export const Card = (props) => ( // <--- this is para not bracket
  <div className='card-container'>
  ...
```

The error would go away when I explicitly stated a return value:

``` JavaScript
export const Card = (props) => ( // <--- this is para not bracket
  return <div className='card-container'>
  ...
```

This is because in javascript, when using arrow syntax to define functions you can use a shorthand imply a return value. This can be done by either omitting brackets/para or you can wrap it with `()` and the statement inside the function will be the return value. Functions need an expression.

### 20 - Breaking into Components

Abstraction allows for reuse and better debug. Lower coupling and higher cohesion.

### 21 - State vs Props

The state of the application passes down the state into the rest of the components as props.

Where the state lives has lots of implications render's efficiency.

### 22 - Search Field

`<input type='search' placeholder='People search?' onChange={ (event) => this.setState({ searchField: event.target.value }) } />`

`this.setState(...)` is an async function and can accept a callback as a second argument.

You can also use vanilla html elements alongside reactjs components.

### 23 - React Events

`<input type='search' placeholder='People search?' onChange={ (event) => this.setState({ searchField: event.target.value }) } />`

The `onChange` event is ***NOT*** the same as `onchange`.

React has [synthetic events](https://reactjs.org/docs/events.html) which are wrappers for native browser events.

You should not call `this.setSate(...)` within `render()`. It is also async.

### 24 - Filtering State

This is same as `const people = this.state.people`:
`const { people, searchField } = this.state;`
This is called destructuring; more can be found [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#Object_destructuring).

``` JavaScript
render() {
  const { people, searchField } = this.state;
  const filteredPeople = people.filter( person =>
    person.name.toLowerCase().includes(searchField.toLowerCase())
  );
```

``` JavaScript
  return (
    <div className='App'>
      <input type='search' placeholder='People search?' onChange={ (event) => this.setState({ searchField: event.target.value }) } />
      <CardList people={ filteredPeople } />
    </div>
  )
}
```

### 26 - Search Box Component

Functional components and class components don't have access to `state` and life-style methods because they are not classes and don't inherit from Component parent class.

Functional components pretty much handle just one job and most of the time that job is to define some HTML or something like that. Example below is a functional component for a search box:

``` JavaScript
export const SearchBox = ({ placeholder, changeHandler }) => (
  <input
    className='search'
    type='search'
    placeholder= { placeholder }
    onChange= { changeHandler }
  />
)
```

All it does it define how the box should look and that it should call the function that is passed to the function (using destructuring).

### 27 - Where to Put state

State needs to be in a location where it can be accessed by what ever needs it. This is called *Lifting State Up*.

### 28 - Class Methods and Arrow functions

Because of javascript's strange `this` behavior binding it to the correct object is important.

`this.changeHandler = this.changeHandler.bind(this);` creates a bond to the `this` value that is defined with in the constructor. It would be the same as `const self = this` and then calling off of `self`.

Rather than verbosely binding `this` to the class you can instead use arrow functions to create a reference between a the named and the anonymous function that will be defined when the object is instantiated. This has to deal with lexical scoping.

``` JavaScript
changeHandler = (e) => {
  this.setState({ searchField: e.target.value });
}
```

### 29 - Exercise even binding

``` JavaScript
constructor () {
  .
  .
  .
  this.handleClick2 = this.handleClick1.bind(this);
}

handleClick1() {
  console.log('button 1');
}

handleClick3 = () => console.log('button 3');

<button onClick={ this.handleClick1() }> // (1)
<button onClick={ this.handleClick1 }> // (2)
<button onClick={ this.handleClick2 }> // (3)
<button onClick={ this.handleClick3 }> // (4)

```

1. The `..()` syntax means that the function is actually going to be invoked when the link of code is evaluated.
2. Will invoke `handleClick1() {...}` but the scope within the function will be bound to itself not the class that contains it.
3. Will call the `handleClick1() {...}` function because of the bind that is made within the constructor. The bind makes it so the the scope within the function will be bound to the class that contains it.
4. This will call `handleClick3 = () => console.log('button 3');` thanks to the lexical scoping that was done when the object was instantiated, eg: the scope within the function is that of the class that contains it.

More on this can be explained in the ReactJS docs [here](https://reactjs.org/docs/handling-events.html).

###