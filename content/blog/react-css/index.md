---
title: React CSS
date: "2015-05-28T22:40:32.169Z"
description: It's different but not too much!
---

##### Inline Styling

The inline style attribute, the value must be a JavaScript object:
Here `color`, `textAlign` are called properties.Notice that they are camelCased.

Example:

```
class Example extends React.Component {
  render() {
    return (
      <div>
      <h1 style={{color: "red", textAlign:"center"}}>Welcome</h1>
      </div>
    );
  }
}
```

##### Javascript object

Create an object with styling information, and refer to it in the style attribute.

Example:

```
class JSObjectExample extends React.Component {
  render() {
    const yourStyle = {
      // comma seperated property and value pairs
      color: "Green",
      textAlign: "center,
      backgroundColor: "lightBlue",
      padding: "10px",
      fontFamily: "Arial"
    };
    return (
      <div>
      <h1 style={yourStyle}>Hello. Isn't this easy...</h1>
      <p>A B ..... Y Z</p>
      </div>
    );
  }
}

ReactDOM.render(<JSObjectExample />, document.getElementById('root'));
```

Before learning further types, know that,
to specify a CSS class, we use the `className` attribute for styling JSX unlike how we use `class` attribute for styling HTML.

##### CSS stylesheets

**App.css**

```
// switch to your normal css - you are free now. No camelCase here!
body {
  background-color: #282c34;
  color: white;
  padding: 40px;
  font-family: Arial;
  text-align: center;
}
```

---

```
import React from 'react';
import ReactDOM from 'react-dom';
import './App.css'; //importing is important you know

class Example extends React.Component {
  render() {
    return (
      <div>
      <h1>Hello</h1>
      <p>Style is a way to say who you are without having to speak.</p>
      <img src="" alt="" />
      </div>
    );
  }
}

ReactDOM.render(<Example />, document.getElementById('root'));
```

##### CSS modules

CSS Modules are regular stylesheets using the `[name].module.css` file naming convention.

_CSS Modules let you use the same CSS class name in different files without worrying about naming clashes._

**MovieDetails.module.css**

```
//this is a css module file

.card {
  background-color: red;
  color: white;
  text-align: center;
}

...so on..
```

---

**regular-stylesheet.css**

```
//this is a normal css file

body{
  background-color: lighblue;
  matgin:0 auto;
}
.card {
  color: red;
}
```

---

**MovieDetail.js**

```
//this is a component file

import React, { Component } from 'react';

import styles from './Button.module.css';
import './another-stylesheet.css';

class MovieDetails extends Component {
  render() {
    // reference as a js object
    return (
    <div className={styles.card}>
      <img src="..." className="card-img-top" alt="...">
      <div className="card-body">
        <h5 className="card">Card title</h5>
        <p className="card-text">Some quick example text to build on
        the card titleand make up the bulk of the card's content.</p>
        <a href="#" className="btn btn-primary">Go somewhere</a>
      </div>
    </div>
    );
  }
}
```

**Results**
The `styles.card` is referenced to the main div in render function and hence the properties mentioned in module will be applied.

So.... what will be the color of the card title? Red or White?
