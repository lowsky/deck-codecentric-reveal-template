# GraphQL
![GraphQL logo](./images/graphqlLogo.png)



![](./images/graphql-everywhere.jpg)
Since 2013:
"As a user of the native facebook iOS or Android app, you are using an app powered by GraphQL."


# What is it?
**Centralized data provider**

![REST-GraphQL](./images/rest-graphql-arch.png) <!-- .element: style="height:10em" -->

(from https://medium.com/apollo-stack/how-do-i-graphql-2fcabfc94a01)
Jonas Helfer


![REST-GraphQL](./images/rest-graphql-arch.png)
> https://cdn-images-1.medium.com/max/1600/1*f_XvFD7FvliMM74WHJ0vRQ.png)
(from https://medium.com/apollo-stack/how-do-i-graphql-2fcabfc94a01)


## a "Query Language for the web"
Similar to JSON, but without 'values'

```javascript
{
     githubUser(id:"lowsky") {
       login
       name
       company
       location
       created_at
   }
}
```
results in ...


## Query result:
Simple JSON

```json
{
    "githubUser": {
      "login": "lowsky",
      "name": "Robert Hostlowsky",
      "company": "codecentric AG",
      "location": "Munich, Germany",
      "created_at": "2010-03-07T20:50:06Z"
    }
}
```


## Schema definition. Type system:
```json
{
  "name": "GithubUser",
  "fields": [
    {
      "name": "id",
      "type": {
        "name": "Int",
        "description": "the user login name. "
      }
    },
    {
      "name": "name",
      "type": {
        "name": "String"
      }
    },
    {
      "name": "repos",
      "type": {
        "kind": "LIST"
      }
    }
    ...
  ]
}
```
(part of graphql schema...)



## *Graph*-QL
Aka. "Nested rpc", hierachical

```javascript
{
  github {
    user(username: "lowsky") {
      login
      repos {
        name
        commits(limit: 1) {
            message date
            author {
                login
            }
        }
      }
      issues(limit: 1) {
        title user {
            id
        }
      }
    }
  }
}
```
results in ...


```json
{
    "github": {
      "user": {
        "login": "lowsky",
        "repos": [
          {
            "name": "deck-graphql-relay-talk",
            "commits": [
              {
                "message": "Initial commit",
                "date": "2016-05-06T15:49:05Z",
                "author": {
                  "login": "lowsky"
                }
              }
            ],
            "issues": []
          },
          {
            "name": "dashboard",
            "commits": [
              {
                "message": "Merge branch 'master' of https://github.com/lowsky/dashboard",
                "date": "2016-05-13T15:59:11Z",
                "author": {
                  "login": "lowsky"
                }
              }
            ],
            "issues": [
              {
                "title": "react-dom@15.1.0 breaks build 🚨",
                "user": {
                  "id": 14790466
                }
              }
            ]
          },
          {
            "name": "updtr",
            "commits": [
              {
                "message": "Update package.json",
                "date": "2015-12-08T23:29:19Z",
                "author": {
                  "login": "matthaias"
                }
              }
            ],
            "issues": []
          }
        ]
      }
    }
}
```


## GraphQL Features
* _Hierarchical_ (embedding sub queries)
* _Strongly-typed_ (schema definition)
* Introspective (tools can look into the schema)
* Product-centric (driven by view, "fetch only what is needed")
* Client-specified queries ("only what the client needs")
* Backwards Compatible
* Structured, Arbitrary Code (queries backed by any code not only SQL)
* Application-Layer Protocol (independend of http/any...)


### Schema inspection:
Graph*i*QL hands-on / demo

[DEMO/screen shot...](image)


## Structured, Arbitrary Code
 (queries backed by any code not only SQL)
 e.g. Hello 'cat':

```javascript
import {
  graphql,
  GraphQLSchema,
  GraphQLObjectType,
  GraphQLString,
  GraphQLNonNull
} from 'graphql';

const schema = new GraphQLSchema({
  query: new GraphQLObjectType({
    name: 'RootQueryType',
    fields: {
      search: {
        type: GraphQLString,
        args: {
          text: { type : new GraphQLNonNull(GraphQLString) }
        },
        resolve(root, args) {
          return 'Hello, ' + args.text;
        }
      }
    }
  })
});
```


### run query
```javascript
const query = `
  {
    search(text: "world")
  }
`;

graphql(schema, query).then(result => {
  console.log(result);
});
```
results in
```
Hello, world
```


## Creating a custom type
```javascript
const GithubUserType = new GraphQLObjectType({
  name : 'GithubUser',
  fields : {
    login : { type : GraphQLString },
    repos : {
        type : new GraphQLList(RepoType),
        resolve(user) {
          // could call any other library
          return githubClient.getReposForUser(user.login);
        }
    },
  }
});
```


## Queries
TBD


## Mutations
TBD


## Product-centric (driven by view, "fetch only what is needed")
TBD


## Backwards Compatible
TBD


## Fragments
TBD


## More (slides) about...
Different server implementations

For many more details, see specification.

[graphql.org](graphql.org)

TBD
