---
title: Component lifecycle - The First Phase.
date: "2021-06-06T23:46:37.121Z"
---

React components get created, rendered, added to the DOM, updated, and removed. All of these steps are part of a component’s lifecycle.

The _first phase_ of a component’s lifecycle is the **Mounting phase**. This is when a component is created and inserted into the DOM - _for the first time_.
The order of the methods that are run during this phase are as below.

##### 1. Constructor

If a component is never mounted, you’d never see it!!.The constructor is the first thing called when the component instance is mounted.

- It is always called with `props` as arguments.
- `super(props)` is always called first.

  Example:

```
constructor(props) {
    super(props);
    this.state = {favoritecolor: "red"};
  }
```

- Yes, it is necessary to call super() inside a constructor, if you need to set a property or access 'this' keyword.

  Eample:

```
class App extends Component {
    constructor(props){
        this.firstName = "XYZ"; // 'this' is not allowed before super(props)
    }
    render () {
        return (
            <div> Your name is: { this.props.name }</div>
        );
    }
}
```

- No, it is not necessary to have a constructor in every component.

_In React, constructors are mainly used for two purposes:_

- It used for initializing the local state of the component by assigning an object to this.state.

- It used for binding event handler methods that occur in your component.

Example:

```
import React, { Component } from 'react';

class App extends Component {
  constructor(props){
    super(props);

    // initializing the local state
    this.state = {
         name: 'Jack'
      }

    // binding event handler method
    this.handleEvent = this.handleEvent.bind(this);
  }

  // event handler
  handleEvent(){
    console.log(this.props);
  }


  render() {
    return (
      <div className="App">
        <h2>Constructors</h2>
        <input type ="text" value={this.state.name} />
        <button onClick={this.handleEvent}>Please Click</button>
      </div>
    );
  }
}
export default App;
```

##### 2. render Function

It is the method that actually outputs the HTML to the DOM.

Let's see the simple example first.

Say you have `<div id="root"></div>` somewhere in your HTML file.
Now, see the element below which has h1 is stored in it.

```
const element = <h1>Hello, world</h1>;
ReactDOM.render(element, document.getElementById('root'));
```

In practice, most React apps only call ReactDOM.render() once.

Example: A simple component
Here, you are rendering a `h1` of `YourName` inside `<div id="root"></div>` .

```
class YourName extends React.Component {
  render() {
    return (
      <h1>Your name is: XYZ</h1>
    );
  }
}

ReactDOM.render(
  <YourName />, // the component you wish to render
 document.getElementById('root') // where you want to render it.
 );
```

##### 3. componentDidMount Function

It is the method called after the component is rendered. OR
`componentDidMount()` is invoked immediately after a component is mounted (inserted into the DOM tree).

Example:
Initially my favourite is `chocolate`, but wait! .....after a second or two my choice would be `icecream`.
Are you also one who can't decide??!.

```
class FavouriteOne extends React.Component {
  constructor(props) {
    super(props);
    // I like chocolate
    this.state = {favorite: "chocolate"};
  }
  componentDidMount() {
    setTimeout(() => {
      this.setState({favorite: "icecream"})
    }, 1000) //just after a second!
  }
  render() {
    return (
      <div><h1>My Favorite among chocolate/icecream is - {this.state.favorite}
      </h1></div>
    );
  }
}

ReactDOM.render(<FavouriteOne />, document.getElementById('root'));

```

> Remember: We use this.state inside constructor and this.setState inside all other functions to set/update the state.

<!-- ([Wikipedia Link](https://en.wikipedia.org/wiki/Salted_duck_egg)) -->
