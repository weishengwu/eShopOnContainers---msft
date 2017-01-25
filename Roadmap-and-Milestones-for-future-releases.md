## Roadmap (By March/April 2017 timeframe)

- Migrate to .csproj and Visual Studio 2017 support, including VS Docker Tooling requirements at the docker-compose.yml files

- Migrate projects to .NET 1.1 and EF 1.1 

- Implement Event-Driven communication between microservices/containers based on Event-Bus interfaces and any simple inter-process communication implementation (That implementation could be swapped by any more advanced Service Bus, like Azure Service Bus using Topics)

- Implement "Idempotent" concept in communication/updates between microservices, so the same update (like a Payment or OrderCreation) cannot be executed multiple times. Decide if that is Application logic or Domain logic

- Fork repo and implement support for Windows Containers running on Windows NanoServer using different Docker base images instead of the Linux based images (.NET Core code should be the same as it is cross-platform)

- Implement a SAGA example of a long running instance of a business process (similar to a workflow but implemented as a class with state persistence). The business process would be the "Order-Process-Saga" workflow, involving multiple mock services like PaymentGateway, StockChecking, etc. while changing the Order's state until the order is shipped. Then a background job which fakes ordre delivery and changes order states to delivered.  

- Resilient synchronous communication for queries- Like when using Circuit Breaker

- Exception Handling - As middleware
Middleware from ASP.NET Core with custom implementation which records specific exceptions depending if it is in production.
Business-Exceptions + Generic-Exception-Handler (ExceptionHandlerHandler)

- Version Management of microservices - Techniques and things to have into account
Caos-Monkey term, etc.

## Roadmap (Future releases)

- (To be Confirmed) In the Windows Containers fork, implement and add an ASP.NET WebForms application (running as a Windows Container) consuming the same microservices, as an example of "lift and shift" scenario.

- (To be Confirmed) In the Windows Containers fork, implement and add a simple WCF microservice/container implementing any logic like a simulated legacy Payment Gateway, as an example of "lift and shift" scenario.

- (To be Confirmed) Build/compile process within an Integration Container (with a provided Docker Image with all SDK dependencies) instead of in local PC. This would greatly simplify the developer's installation requirements in a local machine. That integration container could also be used from a CI pipeline.

- (To be Confirmed) Semantic log - Semantic logic - Related to the Azure app version and Application Insight usage
Monitor what microservices are up/down, etc. related to App Insights, but the events are custom
ETW events and "Semantic Application Log" from P&P
Multiple implementations for the storage of the events, Azure Diagnostics, Elastic Search.
Using EventSource base class, etc.

- (To be Confirmed) Service Fabric and Azure version
Actor model, stateful services, etc.

- (To be Confirmed) Docker Swarm version (on Azure Container Service)
- (To be Confirmed) Mesos DC/OS version (on Azure Container Service)
- (To be Confirmed) Kubernetes version (on Azure Container Service)

- (To be Confirmed) Additional microservice with data stored as a No-SQL database like Azure Document DB