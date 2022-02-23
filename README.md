# 📗 Web-Scalability-For-Startup-Engineers
Repository to take notes while read the book Web Scalability For Startup Engineers



# Chapter 1  

## Core Concepts
To build a success startup you must be as flexible as possible, and need to be resourceful and adapt quickly to changing conditions.  
Three main pillars of scalability: whats it is, how it evolves, what it looks like in a large-scale application, and what its application architecture looks like.

_Scalability_ is an ability to adjust the capacity of the system to costefficitly fulfill the demands. Scalability usually means an ability to handle more users, clients, data, transactions, or requests whitout affecting the UX. Should allow us to scale downd as much as scale up abd that scaling should be relatively cheap and quick to do.

Is related to performance, but is not the same thing. _Performance_ measures how long it takes to preocess request or to perform a certain task, whereas **scalability measures how much we can grow(or shrink);**

_Measure of Scalability_: the ability to scale is measure in different dimensions, as we may need to scale in different ways.
Most Scalability issues can be boiled down to just a few measurements:  
1. `Handling More Data`: the one of the most common challenges. Processing more data puts pressure on your system, as data needs to be sorted, searched through, read from disks, written to disks, and sent over the network.  
2. `Handling higher concurrency levels`: concurrency measures how many clients your system can serve at the same time, how many users can use yout app at the same time without affecting their UX. Higher concurrency means more open connections, more active threads, more messages beign processed at the same time, and more CPU context switches.  
3. `Handling higher interaction rates`: rate of interactions between your system and your clients. It is related to concurrency, but is a slightly different dimension. Measures how often your clients exchange informations with your servers. The main challenge related to the interaction rate is latency. As your interactions rate grows, you need to be able to server responses quicker, which requires faster reads/writes and often drives requirements for higher concurrency levels.

The scalability of your system will usually be defined by the combination of these three requirements.

Hint: Try to assume a more business-oriented perspective. Ask yourself "What are the constraints that could be prevent our business from growing?" it is not just about raw throughtput; it involves development process, teams, and code structure.

Most of time, a system is designed and born in a particular evolution stage and remains in it for its lifetime, or manages to move up one or two steps on the ladder before reaching its architectural limits.

Virtual private server is a term used by hosting providers to describe a virtual machine for rent. VPS instance, it is hosted together with other VPS instances on a shared host machine. VPS behaves as a regular server—you have your own operating system and full privileges. VPS is cheaper than a dedicated server, as multiple instances can exist at the same time on the same physical machine. VPS is a good starting point, as it is cheap and can usually be upgraded instantly (you can add more random access memory [RAM] and CPU power with a click of a button).

For sites with low traffic, a single server configuration may be enough to handle the requests made by clients. But There are many reasons, though, why this
configuration is not going to take you far scalability-wise:

▶ Your user base grows, thereby increasing traffic. Each user creates additional load on the servers, and serving each user consumes more resources, including memory, CPU time, and disk input/output (I/O).
▶ Your database grows as you continue to add more data. As this happens, your database queries begin to slow down due to the extra CPU, memory, and I/O requirements.
▶ You extend your system by adding new functionality, which makes user interactions require more system resources.
▶ You experience any combination of these factors.

### Making the Server Stronger: Scaling Vertically
Once your application reaches the limits of your server (due to increase in traffic, amount of data processed, or concurrency levels), you must decide how to scale.   

Vertical scalability is accomplished by upgrading the hardware and/or network throughput. It is often the simplest solution for shortterm scalability, as it does not require architectural changes to your application.  
**Vertical scalability** is a great option, especially for very small applications or if you can afford the hardware upgrades. The practical simplicity of vertical scaling is its main advantage, as you do not have to rearchitect anything. Unfortunately, vertical scaling comes with some serious limitations, the main one being cost. Vertical scalability becomes extremely expensive beyond a certain point.
The second biggest issue with vertical scalability is that it actually has hard limits.

There are a number of ways to scale vertically:
▶ Adding more I/O capacity by adding more hard drives in Redundant Array of Independent Disks (RAID) arrays    
▶ Improving I/O access times by switching to solid-state drives (SSDs).   
▶ Reducing I/O operations by increasing RAM.   
▶ Improving network throughput by upgrading network interfaces or installing additional ones.     
▶ Switching to servers with more processors or more virtual cores.

_Locks_ are used to synchronize access between execution threads to shared resources like memory or files

### Isolation of Servers
Vertical scalability is not the only option at this early stage of evolution. Another simple solution is moving different parts of the system to separate physical servers by installing each type of service on a separate physical machine. Isolating services to separate servers is just a slight evolution from a single-server setup. It does not take you very far, however, as once you deploy each service type on a separate machine, you have no room to grow. Isolation of services is a great next step for a single-server setup.

`Cache`: Cache is a server/service focused on reducing the latency and resources eeded to generate the result by serving previously generated content. Caching is a very important technique for scalability. 

Hint: The core concept behind isolation of services is that you should try to split your monolithic web application into a set of distinct functional parts and host them independently. The process of dividing a system based on functionality to scale it independently is called functional partitioning.

**The more flexibility we have in scaling each part of the system, the better.**

### Content Delivery Network: Scalability for Static Content

A content delivery network is a hosted service that takes care of global distribution of static files like images, JavaScript, CSS, and videos. It works as an HTTP proxy.s. If the CDN server does not have the requested content yet, it asks your server for it and caches it from then on. Once the file is cached by the CDN, subsequent clients are served without contacting your servers at all.

Round-robin DNS is a DNS server feature allowing you to resolve a single domain name to one of many IP addresses. The regular DNS(ingle domain to         single IP address. round-robin DNS allows you to map the domain name to multiple IP addresses, each IP pointing to a different machine. 

▶  you can significantly reduce the amount of bandwidth your servers need. CDN would serve static content from the closest data center   
▶ DNS is not the only way to distribute traffic among multiple web servers;  

### Distributing the Traffic: Horizontal Scalability

**Horizontal scalability**, on the other hand, is much harder to achieve and in most cases it has to be considered before the application is built.  Systems that are truly horizontally scalable do not need strong servers—quite the opposite; they usually run on lots and lots of cheap “commodity” servers rather than a few powerful machines.   
Horizontal scalability is considered the holy grail of scalability, as it overcomes the increasing cost of capacity unit associated with scaling by buying ever-stronger hardware —you never reach a hard limit, as is the case with vertical scalability

Initially they tend to cost more because they are more complex and require more work. Sometimes they cost more because you need more servers for the most basic setup, and other times it is because you need more experienced engineers to build and operate them. Using horizontal scalability, you avoid the high prices of top-tier hardware and you also avoid hitting the vertical scalability ceiling (where there is no more powerful hardware).

Scaling horizontally using third-party services like CDN is not only cost effective, but often pretty much transparent. The more traffic you generate, the more you are charged by the provider, but the cost pe capacity unit remains constant. That means that doubling your request rate will just cost you twice as much.

horizontally scalable systems from the previous evolution stages is that each server role in our data center can be scaled by adding more servers. Therefore, systems should start by scaling horizontally in areas where it is the easiest to achieve, like web servers and caches, and then tackle the more difficult .areas

### Scalability for a Global Audience

Once you serve millions of users spread across the globe, you will require more than a single data center.

Having more than one data center will also allow you to plan for rare outage events(disaster recovery).
Scaling for a global audience requires a few more tricks and poses a few more challenges. One of the additions to our configuration is the use of geoDNS service.

`GeoDNS`: s a DNS service that allows domain names to be resolved to IP addresses based on the location of the customer. The goal is to direct the customer to the closest data center to minimize network latency.

Another extension of the infrastructure is to host multiple edge-cache servers located around the world to reduce the network latency even further. The use of edge-cache servers depends on the nature of your application. Edge-cache servers are most efficient when they act as simple reverse proxy servers caching entire pages, but they can be extended to provide other services as well.  

Edge cache is a HTTP cache server located near the customer, allowing the customer to partially cache the HTTP traffic. Requests from the customer’s browser go to the edge-cache server. The server can then decide to serve the page from the cache, or it can decide to assemble the missing pieces of the page by sending background requests to your web servers. It can also decide that the page is uncacheable and delegate fully to your web servers. Edge-cache servers can serve entire pages or cache fragments of HTTP responses.  

### Overview Data Center Infrastructure Flow

overview of the communication flow starting from the user’s machine and continuing all the way throughout different layers of the infrastructure; 

Many of the components shown serve a specialized function and can be added or removed independently. However, it is common to see all of the components working together in large-scale applications. Let’s take a closer look at each component.

[imagem]

#### 1. The Front Line

* It is a set of components that users’ devices interact with directly. 
* Parts of the front line may reside inside of our data center or outside of it, depending on the details of the configuration and third-party services used.
* do not have any business logic, and their main purpose is to increase the capacity and allow scalability
* DNS decides which data center is the closest to the client and responds with an IP address of a corresponding load balancer
* Front cache servers 

`Load Balancer`: is a software or hardware component that distributes traffic coming to a single IP address over multiple servers. Load balancers are used to share the load evenly among multiple servers and to allow dynamic addition and removal of machines. Since clients can only see the load balancer, web servers can be added at any time without service disruption.It is common to use third-party services as load balancers, CDN, and reverse proxy servers; in such cases this layer may be hosted entirely by third-party providers.

Web traffic from the Internet is usually directed to a single IP address of a  strong hardware load balancer. It then gets distributed evenly over to front cache  servers (3) or directly over front-end web application servers (4). Front cache servers are optional; they can be deployed in remote locations outside of the data center or skipped altogether. In some cases it may be beneficial to have a layer of front-end cache servers to reduce the amount of load put on the rest of the infrastructure.
 
 #### 2. Web Application Layer
 
 * It consists of web application servers  responsible for generating the actual HTML of our web application and handling clients’ HTTP requests
 * with a minimal amount of business logic, since the main responsibility of these servers is to render the user interface.
 * By pushing most of your business logic to web services, you allow more reuse and reduce the number of changes needed, since the presentation layer is the one that changes most often.
 * are usually easy to scale since they should be completely stateless. 

 #### 3. Web Services Layer
 
 * It is a critical layer, as it contains most of our application logic.
 * By creating web services, we also make it easier to create functional partitions.
 * The communication protocol used between front-end applications and web services is usually Representational State Transfer (REST) or Simple Object Access Protocol (SOAP) over HTTP.
 * Depending on the implementation, web services should be relatively simple to scale. As long as we keep them stateless, scaling horizontally is as easy as adding more machines to the pool, as it is the deeper data layers that are more challenging to scale
 * let’s think of web services as the core of our application and a way to isolate functionality into separate subsystems to allow independent development and scalability. 
 
 #### 4. Additional Components
 
 Since both front-end servers (2) and web services (3) should be stateless, web applications often deploy additional components, such as object caches and
message queues. 
`Object cache servers` are used by both front-end application servers and web services to reduce the load put on the data stores and speed up responses by storing partially precomputed results.
`Messages Queues`  are used to postpone some of the processing to a later stage and to delegate work to queue worker machines

#### 5. Data Persistence Layer

This is usually the most difficult layer to scale horizontally

#### 6. Conclusion

_The layered structure of the components is deliberate and helps to reduce the load on the slower components_

It is very important to remember that it is not necessary to have all of these 
components present in order to be able to scale. Instead, use as few technologies 
as possible, because adding each new technology adds complexity and increases 
maintenance costs. Having more components may be more exciting, but it makes 
releases, maintenance, and recovery procedures much more difficult.


### Overview Application Architecture

Architecture should evolve around the business model. domain-driven design and software 
architecture1–3 that can help you get familiar with best practices of software 
design. Without the right model and the right business logic, our databases, message 
queues, and web frameworks are useless.  
A `domain model` is created to represent the core functionality of the 
application in the words of business people, not technical people.The domain model is a tool to create our 
mental picture of the business problems that our application is supposed 
to solve.  


##### 1. Front End

The front end should have a single responsibility of becoming the user interface. In general, the front end should stay as “dumb” as possible. 

By keeping the front end “dumb,” we will be able to reuse more of the business logic. Since the logic will live only in the web services layer, we avoid the risk of coupling it with our presentation logic. We will also be able to scale front-end servers independently, as they will not need to perform complex processing or share much state, but may be exposed to high concurrency challenges.

 By hiding that within the front-end layer, we can keep our services layer simpler and focused solely on the business logic, not on the presentation and web-specific technologies.

_HINT: You can think of a front-end application as a plugin that can be removed, rewritten in a different programming language, and plugged back in. You should also be able to remove the “HTTP”- based front-end and plug in a “mobile application” front end or a “command line” front end. This attitude allows you to keep more options open and to make sure you decouple the front end from the core of the business logic._

Projects that allow business logic in the front-end code suffer from low code reuse and high complexity. Whenever we can cache an entire HTML page or an HTML fragment, we save much more processing time than caching just the database query that was used to render this HTML. 

##### 2. Web Services

* the place where most of the business logic should live
* `Service-oriented architecture (SOA)`:  is architecture centered on loosely 
coupled and highly autonomous services focused on solving business 
needs. In SOA, it is preferred that all the services have clearly defined 
contracts and use the same communication protocols. I don’t consider 
SOAP, REST, JSON, or XML in the definition of SOA, as they are 
implementation details. It does not matter what technology you use or 
what protocols are involved as long as your services are loosely coupled 
and specialized in solving a narrow set of business needs. 

_HINT: Watch out for similar acronyms: SOA (service-oriented architecture) and SOAP (which originally was an acronym of Simple Object Access Protocol). Although these two can be seen together, SOA is an architecture style and SOAP is a set of technologies used to define, discover, and use web services. You can have SOA without SOAP, and you can also use SOAP in other architecture styles_

SOA is not an answer to all problems and other architecture styles exist, including `layered architecture, hexagonal architecture, and event-driven architecture`.

Layers enforce structure and reduce coupling as components in the lower layers become simpler and less coupled with the rest of the system


_HINT: Web services may depend on each other, but the less they depend on each other, the better. A higher level of abstraction provided by services allows you to see the entire system and still understand it. Each service hides the details of its implementation and presents a simplified, high-level API._

. Such a service would not require Mostuser data or assistance from any other services; it would be fully independent. times, there will be some dependencies between different services. No matter what the implementation of your web services, don’t forget their main purpose: to solve business needs.

 Because they are third-party technologies, they can be treated as black boxes in the context of architecture. From the application architecture point of view, the data store is something that lets us write and read data.
 
 _HINT: Think of the data store as you think of caches, search engines, and message queues—as plugand-play extensions, you should be able to do it by replacing the connectivity components, leaving the overall architecture intact._
 
 Third-party services are outside of our control, so they are put outside of our system boundary. Since we do not have control over them, we cannot expect them to function well, not have bugs, or scale as fast as we would wish.
 
 ### Summary Chapter 1
 
* Architecture is the perspective of the software designer; infrastructure is the perspective of the system engineer
*  scalability is not an easy topic. It touches on many aspects of software design and architecture
*  Scalability can only be tamed once you understand how all the pieces come together, what their roles are, and what their strong points and weak points are.

# Chapter 2 - Principles of Good Software Design


