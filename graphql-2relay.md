# What is Relay?
![https://raw.githubusercontent.com/facebook/relay/master/website/src/relay/img/logo.svg](./images/relayLogo.svg)  <!-- .element: style="height:12em" -->


> "A **framework** for building data-driven React applications"
> [facebook.github.io/relay](http://facebook.github.io/relay)


## What is it for?

* Data-fetching
* Caching
* Pagination
* Optimistic UI


## Main features
* **Co-location**

* **Declarative style**

* **Mutations handling**


# Co-locating
```javascript
class MailUser extends React.Component {
    render() {
        let {name, email} = this.props.user;  // fragment's name
        return (<li>
            { name } <a href={ 'mailto:' + email }>send mail</a>
          </li>);
    }
}
export default Relay.createContainer(MailUser, {
    fragments: {
        user: () => Relay.QL`
          fragment on User {
            name
            email
          }
        ` // ES6 template String
    }
});
```


### DEMO: spotify client

<a href="http://localhost:3000/playlists" data-preview-link="true">Spotify Client</a>


Note:
### DEMO: github branch ci status
https://github.com/lowsky/dashboard/tree/graphql-relay
![Dashboard-Demo-Screenshot](images/dashboard-branches.png)
