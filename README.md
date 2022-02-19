# Web-Scalability-For-Startup-Engineers
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


