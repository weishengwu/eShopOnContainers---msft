These are candidate features to consider for the [roadmap](Roadmap).

- [Create an issue to add a feature to this list](https://github.com/dotnet-architecture/eShopOnContainers/issues/new).

## API handling

- Implement a more advanced versioning system based on [aspnet-api-versioning](https://github.com/Microsoft/aspnet-api-versioning) or comparable system. Current API versioning is very basic, simply based on the URLs. \
  <https://github.com/Microsoft/aspnet-api-versioning>

## Integration event messaging

- Azure Event Grid: Implement an additional Event Bus implementation based on Azure Event Grid.

## Diagnostics and monitoring

- Monitoring/Diagnostics of microservices based on Application Insights with custom perfkeys.

- Semantic log - Semantic logic - Related to the Azure app version and Application Insight usage Monitor what microservices are up/down, etc. related to App Insights, but the events are custom ETW events and "Semantic Application Log" from P&P Multiple implementations for the storage of the events, Azure Diagnostics, Elastic Search. Using EventSource base class, etc.

- Create a new "ServerProblemDetails" response that conforms with RFC 7807, check [issue #602](https://github.com/dotnet-architecture/eShopOnContainers/issues/602) for details.

## Orchestrators

- Service Fabric Stateful Service implementation in the SF branch

## Front-end

- Support for .NET Core 2.0 Razor Pages as additional client app.

- Composite UI based on microservices. Including the “UI per microservice”.

  - Composite UI using ASP.NET (Particular’s Workshop) \
    <http://bit.ly/particular-microservices> 

  - The Monolithic Frontend in the Microservices Architecture \
    <http://blog.xebia.com/the-monolithic-frontend-in-the-microservices-architecture/>

  - The secret of better UI composition \
    <https://particular.net/blog/secret-of-better-ui-composition>

  - Including Front-End Web Components Into Microservices \
    <https://technologyconversations.com/2015/08/09/including-front-end-web-components-into-microservices/>

  - Managing Frontend in the Microservices Architecture \
    <http://allegro.tech/2016/03/Managing-Frontend-in-the-microservices-architecture.html>

- Revamp the whole UI to a more modern look, with a CSS framework/template like [CoreUI](https://coreui.io/)

- Explore [Micro Frontends](https://micro-frontends.org/)

## Security

- Encrypt secrets at configuration files (like in docker-compose.yml). Multiple possibilities, Azure Key Vault or using simple Certificates at container level, Consul, etc.

- Other "secure-code" practices

- Encrypt communication with SSL (related to the specific cloud infrastructure being used)

- Implement security best practices about app's secrets (conn-strings, env vars, etc.)
  (However, this subject depends on the chosen orchestrator...)
  See when using Swarm: https://blog.docker.com/2017/02/docker-secrets-management/

- Support "multiple redirect urls" for the STS container based on Identity Server 4, check [issue #113](https://github.com/dotnet-architecture/eShopOnContainers/issues/113).

- Add social login to MVC and SPA apps, check [issue #475](https://github.com/dotnet-architecture/eShopOnContainers/issues/475) for details.

- Encrypt sensitive information, such as credit card number, along the ordering process, check [issue #407](https://github.com/dotnet-architecture/eShopOnContainers/issues/407)

## Resiliency

- Refactor/Improve Polly's resilient code, check [issue #177](https://github.com/dotnet-architecture/eShopOnContainers/issues/177) for details.

- Add a Jitter strategy to the Retry policy, check [issue #188](https://github.com/dotnet-architecture/eShopOnContainers/issues/188) for details.

## Domain Driven Design

- Enhance the domain logic for Order Root-Aggregate.

  - Already implemented item stock validation (cancels order when quantity is not enough), but could add additional features, check [issue #5](https://github.com/dotnet-architecture/eShopOnContainers/issues/5).

- Handle validation results from MediatR's pipeline.

## Testing

- Include some guidance on testing in CI/CD pipelines, check [issue #549](https://github.com/dotnet-architecture/eShopOnContainers/issues/549) for details.

- Create load testing alternative that's not dependent on the about-to-be-deprecated load testing feature of VS Enterprise, see [issue #950](https://github.com/dotnet-architecture/eShopOnContainers/issues/950) for more details.
## Other

- Azure Functions integrated with Azure Event Grid: Additional event-driven Azure Function microservice (i.e. grabbing uploaded images and adding a watermark and putting it into Azure blobs) - The notification would come from Azure Event Grid when any image is uploaded into a BLOB storage.

- Gracefully stopping or shutting down microservice instances - Implemented as an ASP.NET Core middleware in the ASP.NET Core pipeline. Drain in-flight requests before stopping the microservice/container process.

- Create a building block to handle Idempotency in a generic way ([Issue 143](https://github.com/dotnet/eShopOnContainers/issues/143))

- Implement example of Optimistic Concurrency updates and optimistic concurrency exceptions

- Nancy: Add a Nancy based microservice, also with DocDB, etc.

- Support other DataProtection providers such as AspNetCore.DataProtection.ServiceFabric

- In the Windows Containers fork, implement and add a simple WCF microservice/container implementing any logic like a simulated legacy Payment Gateway, as an example of "lift and shift" scenario.

- Consider using Bash instead of PowerShell scripts, check [issue #228](https://github.com/dotnet-architecture/eShopOnContainers/issues/228) for details.

- Fix naming inconsistency in EventBus projects and namespaces, they should be EventBus.RabbitMQ" and "EventBus.ServiceBus", check [issue #943](https://github.com/dotnet-architecture/eShopOnContainers/issues/943)

- Keep in mind incompatibilities between RabbitMQ and AMQP 1.0 when considering migration. See [issue docs # 5672](https://github.com/dotnet/docs/issues/5672).