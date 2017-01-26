## Roadmap (By March/April 2017 timeframe)

- Migrate to .csproj and Visual Studio 2017 support, including VS Docker Tooling requirements at the docker-compose.yml files

- Migrate projects to .NET 1.1 and EF 1.1 

- Implement support for Windows Containers running on Windows NanoServer using different Docker base images instead of the Linux based images (.NET Core code should be the same as it is cross-platform) - Fork or the same repo?

- INTEGRATION EVENTS: Implement Event-Driven communication between microservices/containers based on Event-Bus interfaces and any simple inter-process communication implementation (That implementation could be swapped by any more advanced Service Bus, like Azure Service Bus using Topics)
Integration Events: 

- DOMAIN EVENTS: Implement Domain Events which is related but not the same as integration events for inter-microservice-communication. Domain Events are initially intended to be used within a specific microservice's Domain, as communicating state changes between Aggregates, although they could derive to Integration Events if what happened in a microservice's domain should impact other additional microservices. See:    
Domain Events – https://docs.spine3.org/biz-model/event.html
Take 2: http://udidahan.com/2008/08/25/domain-events-take-2/ 
http://www.tonytruong.net/domain-events-pattern-example/
Reactive Extensions might be useful for events: 
http://channelsis.com/IntroToRx.pdf
http://www.slideshare.net/EPAMSystems/reactive-extensions-39691960
We should probably implement Domain Events when implementing a SAGA example plus integration events, so we should all those things altogether.

- Implement a SAGA example of a long running instance of a business process (similar to a workflow but implemented as a class with state persistence). The business process would be the "Order-Process-Saga" workflow, involving multiple mock services like PaymentGateway, StockChecking, etc. while changing the Order's state until the order is shipped. Then a background job which fakes ordre delivery and changes order states to delivered.  

- Implement "Idempotent" updates at microservices, so the same update (like a Payment or OrderCreation) cannot be executed multiple times. Server must implement operations idempotently. An operation is idempotent if it gets the same result when performed multiple times. Implementing idempotency is domain-specific. 

- Exception Handling - As middleware
Middleware from ASP.NET Core with custom implementation which records specific exceptions depending if it is in production.
Business-Exceptions + Generic-Exception-Handler (ExceptionHandlerHandler)

- API versioning Management for microservices - Techniques and things to have into account
Related to Caos-Monkey, etc.

- Solid API contracts (based probably on Swagger, but interoperable with any language and explicit per paramater)

## Roadmap (Future releases)

- Production-Ready Cloud application with Resilient microservices' design and implementation 
   - Resilient synchronous HTTP communication with retry-loops with exponential backup/circuit breakers to avoid DDoS initiated from clients
   - Gracefully shutting down a microservice instance - Implemented as an ASP.NET Core middleware in the ASP.NET Core pipeline. Drain in-flight requests before stopping the microservice/container process.
   - Implement messaging communication to ensure Commands/Updates' communication success, using queues, etc. plus providing better scalability capabilities.
   - Encrypt secrets at configuration files (like in docker-compose.yml). Multiple possibilites, Azure Key Vault or using simple Certificates at container level, etc.
   - Encrypt communication with SSL (related to the specific cloud infrastructure being used)
   - Additional topics for production-ready cloud microservices, like using an orchestrator/cluster

- (To be Confirmed) Service Fabric and Azure version
Actor model, stateful services, etc.
- (To be Confirmed) Docker Swarm version (on Azure Container Service)
- (To be Confirmed) Mesos DC/OS version (on Azure Container Service)
- (To be Confirmed) Kubernetes version (on Azure Container Service)

- (To be Confirmed) In the Windows Containers fork, implement and add an ASP.NET WebForms application (running as a Windows Container) consuming the same microservices, as an example of "lift and shift" scenario.

- (To be Confirmed) In the Windows Containers fork, implement and add a simple WCF microservice/container implementing any logic like a simulated legacy Payment Gateway, as an example of "lift and shift" scenario.

- (To be Confirmed) Build/compile process within an Integration Container (with a provided Docker Image with all SDK dependencies) instead of in local PC. This would greatly simplify the developer's installation requirements in a local machine. That integration container could also be used from a CI pipeline.

- (To be Confirmed) Semantic log - Semantic logic - Related to the Azure app version and Application Insight usage
Monitor what microservices are up/down, etc. related to App Insights, but the events are custom
ETW events and "Semantic Application Log" from P&P
Multiple implementations for the storage of the events, Azure Diagnostics, Elastic Search.
Using EventSource base class, etc.

- (To be Confirmed) Additional microservice with data stored as a No-SQL database like Azure Document DB