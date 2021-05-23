---
title: Know about the Effect Hook.
date: "2020-05-01T22:12:03.284Z"
description: "Hello World"
---

Usually, function components were only used to accept data in the form of props and return some JSX to be rendered.

And then Hooks came into picture.
_A Hook is a special function that lets you “hook into” React features._

> Note: If you are new to class component lifecycle methods visit this [link](https://reactjs.org/docs/react-component.html#the-component-lifecycle) and know/understand the simple defnitions for a few minutes.
> It's enough if you know the defnitions of componentDitMount() and componentDidUpdate() to understand further facts below.

First let's see the two types of components which are trying to render same output.

- Find out which is easier to maintain and read.

##### The Class Component

Observe, logic for setting the name is split in two lifecycle methods.

```
import React, {Component} from 'react';

export default class NameItAnything extends Component {
constructor(props) {
super(props);
this.state = {
name: ''
};
}

componentDidMount() {
document.title = this.state.name;
}

componentDidUpdate() {
document.title == `Hi, ${this.state.name}`;
}

render() {
return (
    <div>
        <p>Give any input to name to your page</p>
        <input
        onChange={({target}) => this.setState({ name: target.value })}
        value={this.state.name}
        type='text' />
    </div>
        );
    }
}
```

##### The Functional Component

Now, observe the logic being written in one place.

```
import React, { useState, useEffect } from 'react';

export default function NameItAnything() {
  const [name, setName] = useState('');

 useEffect(() => {
    document.title = `Hi, ${name}`;    //side effect
  }, [name]);

  return (
    <div>
      <p>Give any input to name to your page</p>
      <input
        onChange={({target}) => setName(target.value)}
        value={name}
        type='text' />
    </div>
  );
}
```

- Oh! so found out which is easier?
  The functional component? you're right!

> Tip: If you’re familiar with React class lifecycle methods, you can think of useEffect Hook as componentDidMount, componentDidUpdate, and componentWillUnmount combined.

##### Let's see how to use the Effect hook.

> `useEffect(callback,dependencies)`

1. First import the hook from react library like so: `import { useEffect } from 'react';`

2. The hook doesn't return anything but calls an other function(annoymous) which has some logic.

3. `() => { document.title = name; }` is the first argument a `callback` function.

4. `,[name]` is the second argument a `dependency` that controls when you want to run the side effect.

##### Know more about dependencies:

| if dependency/ies            | ~the useEffect                                                                                |
| :--------------------------- | :-------------------------------------------------------------------------------------------- |
| 1. are not provided          | Runs everytime                                                                                |
|                              |                                                                                               |
| 2. is an empty array []      | Runs ONCE after initial rendering                                                             |
|                              |                                                                                               |
| 3. Has props or state values | Runs ONCE after initial rendering and after every rendering ONLY IF `prop` or `state` changes |

---

##### Know these facts:

1. By using this Hook, you tell React that your component needs to do something after render.

2. React will remember the function you passed (we’ll refer to it as our “effect”), and call it later after performing the DOM updates.

3. By default, it runs both after the first render and after every update.
