## Let's talk about REST!

Note:
## What is wrong with REST?
Nothing.
But, ...
 
* Architectural Styles and the Design of Network-based Software Architectures,
* Fielding's doctoral dissertation, describes Representational State Transfer (REST)
* http://www.anchor.com.au/blog/2013/02/how-everyone-is-doing-rest-wrong/


Let's build a web client

![](./images/githubPage.png)


Every component need some data
![](./images/githubPageMarked.png)


GitHub API example
![](./images/rest-github-user.png)

Note:
![](./images/rest-github-apis.png)


## Issues when using REST
 * one resource => one request + **many extra requests**
 * only **one representation** - for different devices
 * **paging**
 * **documentation** for each end-point
 * *all* or *nothing*: **over-fetching**
 
 * workaround: **custom end points** -> more stuff to code + maintain

Note:
### More problems arise:
* When the apps grow 
* -> things getting more complex
* -> inter-dependencies grow
* hard to maintain on server and client - dependencies
* backward compatibility
 
