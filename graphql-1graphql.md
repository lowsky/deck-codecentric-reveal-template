# GraphQL
Since 2013:

"Any user of the native facebook iOS or Android app in the last 3 years has used an app powered by GraphQL."


# What is it?
## Schema definition. Type system:
```json
{
  "name": "GithubUser",
  "fields": [
    {
      "name": "id",
      "type": {
        "name": "Int",
        "description": "The `Int` scalar type represents non-fractional signed whole numeric values. Int can represent values between -(2^31) and 2^31 - 1. "
      },
    },
    {
      "name": "company",
      "type": {
        "name": "String",
        "description": "The `String` scalar type represents textual data, represented as UTF-8 character sequences. The String type is most often used by GraphQL to represent free-form human-readable text."
      },
    },
    {
      "name": "repos",
      "type": {
        "kind": "LIST",
      },
    }
  ]
}
```
(part of graphql schema...)


## a "Query Language for the web"
Similar to JSON, but without 'values'

```javascript
{
     githubUser(id: 'lowsky') {
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

```
{
    githubUser: {
      "login": "lowsky",
      "name": "Robert Hostlowsky",
      "company": "codecentric AG",
      "location": "Munich, Germany",
      "created_at": "2010-03-07T20:50:06Z"
    }
}
```


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
}
```
results in ...


```javascript
{
    "github": {
      "user": {
        "login": "lowsky",
        "repos": [
          {
            "name": "graphql-relay-talk",
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
          },
        ]
      }
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

[screen shot...](image)


## Structured, Arbitrary Code
 (queries backed by any code not only SQL)
 e.g. Hello 'cat':

```
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
```
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
```
const GithubUserType = new GraphQLObjectType({
  name : 'GithubUser',
  fields : {
    login : { type : GraphQLString }
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
