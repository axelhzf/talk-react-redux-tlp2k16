title: React + Redux - A better way to build javascript apps
author:
  twitter: axelhzf
  url: http://axelhzf.com
output: index.html
controls: false
theme: ./theme

-- cover

![](images/react-redux-logo.png)

# REACT + REDUX

## A BETTER WAY TO BUILD JAVASCRIPT APPS

--

## The best way to learn a new technology is building something

http://axelhzf.com/gifux

--

## React

--

## React is a library to build user interfaces

--

## React is all about modular and composable components

--

```js
import React from "react";
import ReactDOM from "react-dom";

export default class HelloWorld extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello World</h1>
      </div>
    );
  }
}

ReactDOM.render(<HelloWorld />, document.getElementById('container'));
```

--

## Is this html inside JS?

--

## It's JSX.

--

## JSX is compiled to something like

```js
React.createElement("div",null,
  React.createElement("h1",null,"Hello World")
);
```

--

## But, where is the separation of concerns?

--

## React: rethinking best practices

https://www.youtube.com/watch?v=x7cQ3mrcKaY

--

## Templates encourages a poor separation of concerns.

--

## Templates separates technologies, not concerns.

--

## JSX benefits

* Fails at compile time
* Line number provided
* Debuggable

--

## Angular 2 continues to put “JS” into HTML. React puts “HTML” into JS.

--

### To read Angular: Learn a long list of Angular-specific syntax.

### To read React: Learn JavaScript.

--

## Render a list in Angular 2

```js
<ul>
  <li *ngFor="#hero of heroes">
    {{hero.name}}
  </li>
</ul>
```

--

## Render a list in React

```js
<ul>
  { heroes.map(hero => <li key={hero.id}>{hero.name}</li>) }
</ul>
```

--


# Props

Data passed in from a parent component is available as a 'property' on the child component. These 'properties' are accessed through `this.props`.

```js
export default class Hello extends React.Component {
  render() {
    const {name} = this.props;
    return <h1>Hello {name}</h1>;
  }
}
```

```js
<HelloWorld name="Treexor"/>;
```

--

# State

Components can have it's own private mutable state `this.state`. The state can be changed by calling `this.setState()`.

--

```js
import React from "react";

export default class HelloWorld extends React.Component {
  state = { counter: 0};
  increment = () => this.setState({counter: this.state.counter + 1})
  render() {
    const {counter} = this.state;
    return (
      <div>
        <h1>Counter {counter}</h1>
        <button onClick={this.increment}>Increment</button>
      </div>
    );
  }
}
```

--

# Redux

--

##  Redux is a predictable state container for JavaScript apps.

--

![](http://s2.quickmeme.com/img/d9/d9f01f01d19cd39d7bd57e5b9570210758d545eb7583477689d29f113276c7b1.jpg)

--

# State

* Applications needs to store complex state
* State from server responses
* State from UI (selected tab, spinners, pagination)
* Share state between independent components

--

# MVC

![](http://axelhzf.com/talk-new-ideas-web-app/2fd134f491b9a8c56a4fddf422ea8237.svg)

--

# Real world MVC

![](http://axelhzf.com/talk-new-ideas-web-app/68132677d59dfe921c41d6f34afb2091.svg)

--

> When a system is opaque and non-deterministic, it’s hard to reproduce bugs or add new features.

--

> Mutation and asynchronicity create a mess. We need to find a way to make our state more predictable.

--

## Introducing Redux

https://www.youtube.com/watch?v=xsSnOQynTHs

--

## Redux
* Inspired on flux and elm
* Minimal api
* Completely predictable behaviour
* Not react specific, it's just an event and state management library

--

## Redux Principles

--

## SINGLE SOURCE OF TRUTH

* The state of the whole application is stored in an object tree within a single store
* Easy to share information across components
* Easy to debug
* We can easily save and restore the state of the whole application
* Undo/redo, hot reloading, trace production error

--

```js
var state = {
  visibilityFilter: 'SHOW_ALL',
  todos: [
    { text: 'Consider using Redux', completed: true},
    { text: 'Keep all state in a single tree', completed: false}
  ]
};
```

--

## State is read-only

* The only way to mutate the state is to emit and action, an object describing what happened.
* Views or http callbacks don't modify the state, instead they express the intention to mutate the state.
* Actions can be logged for debugging or stored for testing purposes

--

```js
store.dispatch({
  type: 'COMPLETE_TODO',
  index: 1
});

store.dispatch({
  type: 'SET_VISIBILITY_FILTER',
  filter: 'SHOW_COMPLETED'
});
```

--

## Changes are made with pure functions

* These pure functions are called reducers

```js
(previousState, action) => newState
```

--

```js
function reducer(state, action) {
  switch (action.type) {
    case 'SET_VISIBILITY_FILTER':
      var newState = _.clone(state);
      newState.filter = action.filter;
      return newState;

    case 'SET_COMPLETE_TODO':
      var newState = _.clone(state);
      newState.todos[action.index].completed = true;
      return newState;

    default:
      return state
  }
}
```

--

![](http://axelhzf.com/talk-new-ideas-web-app/629f6ef5231273ca1f2114b0ea2cf1d1.svg)

--

--


# Optimizing our application

--

# How React works?

* Every time props or state change the render method is called.
* `render` creates a `virtual dom` representation of our view.
* Rect compute the diff between the new and the old tree.
* Creates a batch of DOM updates

--

![](http://axelhzf.com/talk-new-ideas-web-app/c980e98d9fb1e693e7198eb4b641e462.svg)

```js
f(Do) = Vo
```

--

![](http://axelhzf.com/talk-new-ideas-web-app/0ad9b87a0281ef269223fcdb17fd09a9.svg)

```js
f(D1) = V1
diff(V0, V1) = CHANGES
```

--

## Om

* ClojureScript interface to Facebook's React
* Om has better performance out of the box than React.
* Because ClojureScript data is immutable data, React's reconciliation process has to do less work.

--

Persistent data structures

https://www.youtube.com/watch?v=mS264h8KGwk&app=desktop
https://www.youtube.com/watch?v=I7IdS-PbEgI

--





--

<script async src="http://platform.twitter.com/widgets.js" charset="utf-8"></script>
<script type="text/javascript">
    var _gaq = _gaq || [];
    _gaq.push(['_setAccount', 'UA-31904298-1']);
    _gaq.push(['_trackPageview']);

    (function() {
        var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
        ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'http://www') + '.google-analytics.com/ga.js';
        var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
    })();
</script>