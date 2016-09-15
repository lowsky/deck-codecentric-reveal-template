# Introduction

## So, what is wrong with REST?


## What is wrong with REST?
Nothing.
 
```
// todo: add slide here with kudos to Roy T. Fielding ...
```
 
but ....
Note:
* Architectural Styles and the Design of Network-based Software Architectures,
* Fielding's doctoral dissertation, describes Representational State Transfer (REST)
* http://www.anchor.com.au/blog/2013/02/how-everyone-is-doing-rest-wrong/

## So - What is wrong with REST

![](./images/githubPage.png)


![](./images/githubPageMarked.png)


![](./images/rest-github-user.png)


![](./images/rest-github-apis.png)


## What is wrong with using REST
 * one resource = one request + many extra requests
 * only *one* representation for different devices
 * no easy paging
 * have to *document* each end-point separately 
 * *all* or *nothing*: over-fetching
 * workaround: custom end points -> more stuff to code + maintain

Note:
### More problems arise:
* When the apps grow 
* -> things getting more complex
* -> inter-dependencies grow
* hard to maintain on server and client - dependencies
* backward compatibility
 
