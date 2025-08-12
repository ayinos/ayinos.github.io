# Reliable, Scalable & Maintainable Applications
## Thinking about dta systems
- Dbs, queues, caches have some similarity but very different access patterns which means different performance 
characteristics thus very different implementations.
- Some boundaries between these categories are becoming blurred
  - For e.g. 
    - datastore used as message queues (Redis)
    - message queue with db like durability guarantees (Apache Kafka)
- Many apps have wide range of requirements which are broken down into tasks that can be performed efficiently on a 
single tool and those different tools are stitched together using application code.
  - For e.g. normally application codes responsibility to keep caches & indexes in sync with the db.
## Application requirements
### Functional requirements
- e.g. allowing data to be stored, retrieved, searched & processed in various ways
### Non-functional requirements
- security
- reliability
- compliance
- scalability
- compatibility 
- maintainability
## Reliability
- Making systems work correctly even when faults occur.
  - Faults vs Failure
    - Fault : One component of the system is deviating from the specs
    - Failure : system as whole stops 
    - best to design _fault tolerant systems_ that prevent faults from causing failures.
      - Faults can be in 
        - Hardware
          - Typically random & uncorrelated 
          - e.g. Hard disk crash, faulty RAM 
          - There is a move toward systems that can tolerate loss of entire machines by using software fault tolerance 
          techniques in preference or in addition to hardware redundancy.
        - Software
          - Typically systematic and hard to deal with
          - Examples
            - Bug that causes server to crash. LEap second on June 30 2012, causes many apps to hang simultaneously due 
            to a bug in the Linux kernal.
            - A process that uses up some shared resource CPU time, memory, disk space or bandwidth
            - External service that the app depends on slows down or becomes unresponsive.
            - Cascading failure, small fault in one component triggers fault in another and so on.
        - Humans 
          - e.g. configuration errors.
          - Solutions
            - minimize opportunity or errors
            - provide sandbox envs to explore & experiment
            - test thoroughly
            - allow for quick & easy recovery e.g. make it fast to rollback.
            - setup detailed & clear monitoring
- Fault tolerance techniques can hide certain type of faults from the end user
## Scalability
- Means having strategies to keep performance good even when load increases.
- Describing Load
  - can be descried with a few numbers which we call _load parameters_
    - could be requests per second to a web server
    - ratio of reads to writes in db
    - number of simultaneously active users in a chat room
    - hit rate on a cache
- Describing performance
  - In a batch processing system we usually care about _throughput_
  - In online systems usually _response time_ is more important
  - Latency & response time
    - Response time = Time to process request + n/w delay + queuing delays
    - Latency = duration that a request is waiting to be handled.
  - Response time percentiles is a way of measuring performance
    - for e.g. if median response time (50th percentile) is 200ms means half requests return in < 200ms and half > 200ms
    - Higher percentiles (95th 99th 99.9th) may directly affect users performance because customers with teh the slowest 
    request may have the most data i.e. most purchases.
  - 
- In a scalable system you can add processing capacity in order to remain reliable under high load.
- 
## Maintainability
- Many facets but in essence its about making like easier for the engineering & operations teams 
- Good abstractions can help reduce complexity and make system easier to modify & adapt for new use cases.
- Good operability means having good visibility int the systems healths and having effective ways of managing it.


