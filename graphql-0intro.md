# Introduction

* "My experience with a monolithic frontend web app..."
* "Be creative, again!"


# First: React basics
## the V of _M V C_
[IMG]
!(./images/reactLogo.png)

# What is React...?
* composition
* props / state
* higher-order/just a function


## What is data binding
Angular, Ember, Meteor ... - MVC


 [docs.angularjs.org/guide/databinding](https://docs.angularjs.org/guide/databinding)

 > ["Data binding code in 9 JavaScript frameworks"](http://engineering.paiza.io/entry/2015/03/12/145216)


## Data-binding ... the React way:
### composition instead of templating
```javascript
Hello = React.Component {
  render() { return <span>Hello, { this.props.name } ! </span>; }
}

HelloWorld = React.Component {
  render() { return <Hello name={ this.props.world.name } />; }
}

data = fetch('/api/name...'); // = { world: 'enterjs'; }

ReactDOM.render(<HelloWorld world={ data } />, domElement);
```

gives

```html
<span>Hello, enterjs</span>
```


## What is wrong with REST?


![](./images/rest-github-apis.png)


![](./images/rest-github-user.png)


## What is wrong with using REST?
 * one resource = one request -> many requests
 * only *one* representation for different devices
 * n+1 / paging
 * have each end-point *documented*
 * *all* or *nothing*
 * custom end points for 'ad-hoc' special data


### More problems arise:
* When the apps grow -> things getting more complex
* inter-dependencies grow
* hard to maintain
* stay backwards compatible
