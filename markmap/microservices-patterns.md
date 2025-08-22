# Microservices Patterns 

## Chapter 01 : Escaping Monolithic Hell
### Monolithic architecture pattern 
- Structures the deployment as a single deployable unit
- Good choice for simple applications 
### Microservice architecture pattern 
- Decomposes a system into a set of independently deployable services, each with its own db
- Usually a better choice for large, complex applications
- Accelerates the velocity of sw development by enabling small autonomous teams to work in parallel
- Not a silver bullet, there are significant drawbacks including complexity
- Microservice architecture pattern language 
  - is a collection of patterns that help you architect an application using the microservice architecture.
  - helps decide if whether to use the microservice architecture
  - and helps apply it effectively
- More than microservice architecture needed to accelerate sw development
  - Also requires DevOps and small autonomous teams

## Chapter 02: Decomposition Strategies
- Architecture determines your applications
  - maintainability
  - testability
  - deployability 
- Microservice architecture is an architecture style that gives an application 
  - high maintainability
  - high testability 
  - high deployability
- Services in a microservice architecture are organized around 
  - business concerns/business capabilities or subdomains
  - rather than technical concerns
- 2 patterns for decomposition
  - Decompose by business capability (which has origins in business architecture)
  - Decompose by sub-domain (based on concepts from domain-driven design)
- You can eliminate god classes which cause tangled dependencies that prevent decomposition,
  - by applying DDD and defining a separate domain model for each service.

## Chapter 03: Interprocess communication
- Microservice architecture is a distributed architecture, so interprocess communication plays a key role
- Essential to carefully manage the evolution of a service's API 
  - Backward compatible changes are easiest to make as they do not impact clients.
  - If a breaking change needs to be made to a service's API, 
    - it will typically need to support both old and new versions until its clients have been upgraded.
- There are numerous IPC technologies each with different trade-offs.One Key design decision is to choose either
  1. Synchronous remote procedure invocation pattern
     - e.g. REST (Note: While the underlying HTTP protocol used by REST is a request-response model that can be perceived 
     as synchronous, the client-side implementation determines whether the interaction with the REST API is handled 
     synchronously or asynchronously.)
     - easier to use
  2. Asynchronous messaging pattern
     - increases availability
- To prevent cascading failures, service client that uses a synchronous protocol must be designed to handle partial 
failures 
  - which could be 
    - the invoked service is down 
    - or exhibiting high latency
  - It must 
    - use timeouts when making requests
    - limit the number of outstanding requests
    - use circuit breaker pattern to avoid making calls a failing service
- An architecture that uses Synchronous protocols must include a _Service Discovery_ mechanism.
  - Service Discovery approaches
    1. Use service discovery mechanism implemented by the deployment platform 
       - Server-side discovery & 3rd party registration patterns
    2. Implement service discovery at the application level
       - Client side discovery and self registration patterns
         - More work but handles the scenario where services are running on multiple deployment platforms
- Good way to design a messaging based architecture is to use the messages and channels model, which abstracts the 
details of the underlying messaging system. You can then map that design to a specific messaging infrastructure which is
typically message broker based.
- One key challenge when using messaging is 
  - To atomically update the db & publish the message.
  - Good solution is to use the Transactional outbox pattern that is
    1. Write the message to the db as a part of db transaction.
    2. A separate process then retrieves the message from the db using either
       - Polling publisher pattern or
       - Transaction log trailing pattern
    3. Publish the message to the message broker.
