# Vert.x





## Contents at a Glance.
* [About.](#about)
* [Documentation.](#documentation)
* [Asynchronous Programming.](https://github.com/descriptions-of-it-technologies/asynchronous-programming)
* [Reactive Programming.](https://github.com/descriptions-of-it-technologies/reactive-programming)
* [Functional Reactive Programming.](https://github.com/descriptions-of-it-technologies/functional-reactive-programming)  
* [Event Loop.](#event-loop) 
* [Event Driven.](#event-driven)
* [Event Bus.](#event-bus)
* [Vertical.](#vertical)
* [Vertx Modules.]()
* [Pattern.](#pattern)
* [Commands.](#commands)
* [Articles.](#articles)
* [Conferences.](#conferences)
* [Conference Speakers.](#conference-speakers)
* [Help.](#help)





## About.





## Documentation.
* [VERT.X](https://vertx.io/)
* [Cluster Manager.](https://vertx.io/docs/vertx-hazelcast/java/)



## The Vert.x instance.
* The Vert.x instance is being shared by multiple verticles, and there is generally only one instance of Vertx per JVM process.




## Verticles.
* Put simply, a verticle is the fundamental processing unit in Vert.x. The role of a verticle is to encapsulate a 
  technical functional unit for processing events, such as exposing an HTTP API and responding to requests, providing 
  a repository interface on top of a database, or issuing requests to a third-party system. Much like components in 
  technologies like Enterprise JavaBeans, verticles can be deployed, and they have a life cycle.
  Asynchronous programming is key to building reactive applications, since they have to scale, and verticles are 
  fundamental in Vert.x for structuring (asynchronous) event-processing code and business logic.
* verticles have private state that may be updated when receiving events, they can deploy other verticles, and they 
  can communicate via message-passing (more on that in the next chapter). Verticles do not necessarily follow the orthodox 
  definition of actors, but it is fair to consider Vert.x as being at least inspired by actors.
* Standard
  * Son aquellos que son asincronos
* Worker
  * creado especificamente para ejecutar operaciones sincronas
* Multithread worker
  * es semilar que 'worker' pero permite ejecutar las instancias concurrente
* An each verticle receives its unique deployment ID. This is a string object and the deployment ID is represented in a UUID v4 format.





## The life cycle of any Vertx verticle has following stages:
1. The Vertx instance calls the init() method of a verticle. This method is already implemented in the AbstractVerticle 
   class, although you have to provide your own implementation, if you use the Verticle interface, you have to provide 
   your own implementation). It provides to the verticle references to Vertx and Context instances. Please note, that 
   by default, there is one Vertx instance per JVM.
2. The Vertx instance calls the start() method to execute its startup logic. Based on the Promise object’s result, it 
   can either be successfully completed (which means, that the verticle is ready to deploy), either it can fail (which 
   means, that the verticle would not be deployed)
3. The Vertx instance deploys the verticle. An each verticle receives its unique deployment ID. This is a string object 
   and the deployment ID is represented in a UUID v4 format.
4. The Vertx instance calls the stop() method to execute a termination callback. This means, that this is a place to do 
   work that is required before closing, for example, save data or clean used resources.
5. The Vertx instance undeploys a verticle.





## Event Loop. 
* Handler callbacks are run from event-loop threads. It is important that code running on an event loop takes as little 
  time as possible, so that the event-loop thread can have a higher throughput in the number of processed events. 
  This is why no long-running or blocking I/O operations should happen on the event loop.
* That being said, it may not always be easy to spot blocking code, especially when using third-party libraries. 
  Vert.x provides a checker that detects when an event loop is being blocked for too long.
* CONFIGURING THE VERT.X BLOCKED THREAD CHECKER
  The time limit before the blocked thread checker complains is two seconds by default, but it can be configured to a 
  different value. There are environments, such as embedded devices, where processing power is slower, and it is normal 
  to increase the thread-checker threshold for them.
  You can use system properties to change the settings:
    * `-Dvertx.options.blockedThreadCheckInterval=5000` changes the interval to five seconds.
    * `-Dvertx.threadChecks=false` disables the thread checker.
  Note that this configuration is global and cannot be fine-tuned on a per-verticle basis.
* By default, Vert.x creates twice the number of event-loop threads as CPU cores. If you have 8 cores, then a Vert.x 
  application has 16 event loops. The assignment of verticles to event loops is done in a round-robin fashion.
* It is possible to tweak how many event loops should be available, but it is not possible to manually allocate a given 
  verticle to a specific event loop. This should never be a problem in practice, but in the worst case you can always 
  plan the deployment order of verticles.
* The basic rule when running code on an event loop is that it should not block, and it should run “fast enough.”
* Vert.x provides two options for dealing with blocking code: worker verticles and the executeBlocking operation.




## Workers.
* Worker verticles are a special form of verticles that do not execute on an event loop. Instead, they execute on worker 
  threads, that is, threads taken from special worker pools. You can define your own worker thread pools and deploy 
  worker verticles to them.
* Worker verticles can be used to process blocking I/O and long-running operations.    





## Worker thread pool. 





## Context. 
* Context data
* It is possible to mix code with both Vert.x and non-Vert.x threads by using event-loop contexts.







## Event Driven. 





## Event Bus.
* Point to point (single publisher and a single consumer)
* Request/Response 
* publish/subscribe ('broadcasting', 'single publisher to many consumers')
* разпределонная комуникационная шына





## Vertical. 





## Cluster Manager.
* [Hazelcast(default)](https://github.com/descriptions-of-it-technologies/hazelcast)
* [Apache Zookeeper.](https://github.com/descriptions-of-it-technologies/zookeeper)
* [Apache Ignite.](https://github.com/descriptions-of-it-technologies/apache-ignite)
* [Infinispan.](https://github.com/descriptions-of-it-technologies/infinispan)





## Cluster HA.





## Pros.
* Embedded event bus
* Abstraction over Java Concurrency
* Reactive
* Polyglot





## Cons.
* 





## Vert.x Modules
* [Vertex Core.](vertx-core.md)
* [Vertex Web.](vertx-web.md)





## Pattern.
* [Multi-Reactor.](https://www.google.com/search?q=multi+reactor+pattern&oq=pattern+multi-re&aqs=chrome.1.69i57j0.14644j0j7&sourceid=chrome&ie=UTF-8)





## Books.





## Articles.
* [Vert.x microservices: an (opinionated) application](https://medium.com/@victorgil_91367/vert-x-microservices-an-opinionated-application-56e44c0b45b4)
* []()




## Conferences.
* [Curso Vert.x - Paradigma Digital](https://www.youtube.com/playlist?list=PL2yjEVbRSX7WuD06zFOXmW_o2CPvCrf7t)





## Conference Speakers.





## Useful Links.
* [What's the difference between the send and publish methods of Vertx's EventBus?](https://stackoverflow.com/questions/56715200/whats-the-difference-between-the-send-and-publish-methods-of-vertxs-eventbus)
* [Vert.x microservices: an (opinionated) application](https://medium.com/@victorgil_91367/vert-x-microservices-an-opinionated-application-56e44c0b45b4)
* []()





## 
* 


## Help.
