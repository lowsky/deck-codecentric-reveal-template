# GraphQL + Relay = data-binding 2.0 ?


# First: React
## the V of MVC
[IMG]


# React...
### Angular, Ember, Meteor...

have some data-binding,
based on some MVC concept

[IMG]


## Data-binding ... the React way:
### composition instead of templating
```javascript
fetchedData = fetch('/api/name...');
// = { world: 'enterjs'; }

ReactDOM.render(<HelloWorld worldData={ fetchedData } />, domElement);

HelloWorld = React.Component {
  render() { return <Hello name={ this.props.worldData.name } />; }
}

Hello = React.Component {
  render() { return <span>Hello, { this.props.name } </span>; }
}
```

gives

```html
<span>Hello, enterjs</span>
```


## What is wrong with using REST?
 * one resource = one request -> many requests
 * only one representation for different devices
 * all or nothing
 * n+1 / paging
 * have each end-point documented
 * custom end points for 'ad-hoc' specical data


### More problems arise:
* When the apps grow -> things getting more complex
* inter-dependencies grow
* hard to maintain
* stay backwards compatible
