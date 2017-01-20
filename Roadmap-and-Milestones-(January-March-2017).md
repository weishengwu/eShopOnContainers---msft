## Roadmap (January-March timeframe)

- Migrate to .csproj and Visual Studio 2017 support, including VS Docker Tooling requirements at the docker-compose.yml files

- Migrate projects to .NET 1.1 and EF 1.1 

- Implement Event-Driven communication between microservices/containers based on Event-Bus interfaces and any simple inter-process communication implementation (That implementation could be swapped by any more advanced Service Bus, like Azure Service Bus using Topics)

- Fork repo and implement support for Windows Containers running on Windows NanoServer using different Docker base images instead of the Linux based images (.NET Core code should be the same as it is cross-platform)

- Implement a SAGA example of a long running instance of a business process (similar to a workflow but implemented as a class with state persistence). The business process would be the "Order-Process-Saga" workflow, involving multiple mock services like PaymentGateway, StockChecking, etc. while changing the Order's state until the order is shipped. Then a background job which fakes ordre delivery and changes order states to delivered.  

- (To be Confirmed) In the Windows Containers fork, implement and add an ASP.NET WebForms application (running as a Windows Container) consuming the same microservices, as an example of "lift and shift" scenario.

- (To be Confirmed) In the Windows Containers fork, implement and add a simple WCF microservice/container implementing any logic like a simulated legacy Payment Gateway, as an example of "lift and shift" scenario.

- (To be Confirmed) Build/compile process within an Integration Container (with a provided Docker Image with all SDK dependencies) instead of in local PC. This would greatly simplify the developer's installation requirements in a local machine. That integration container could also be used from a CI pipeline.
