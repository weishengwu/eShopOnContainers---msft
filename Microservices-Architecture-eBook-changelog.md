## eBook -  .NET Microservices: Architecture for Containerized .NET Applications

### Release 3.1.3 (2020-11-10)

*Reference commits :* [182fe95](https://github.com/dotnet/docs/commit/182fe95571393d39e0ad212c1e46acfacd7db8db), [a3789be](https://github.com/dotnet/docs/commit/a3789bebfb63217822a6ad795b6cdd3bb2f7f16e), [153df0e](https://github.com/dotnet/docs/commit/153df0eaf4f6acd340e77818c6b617d9e554f004), [a7dfe75](https://github.com/dotnet/docs/commit/a7dfe75ff89818f789a975435ccc5f0070c9e802), [9eb4479](https://github.com/dotnet/docs/commit/9eb44793999083daad6984cb37600c48e441b33d), [1d89b18](https://github.com/dotnet/docs/commit/1d89b18e15c33be746ba917485c1f53f8cf43c5a), [5f89393](https://github.com/dotnet/docs/commit/5f89393b25287a945033197474ac0a9540013853), [b77b615](https://github.com/dotnet/docs/commit/b77b615d4b45334905c6e9dfa6b165abbcabc7d5), [7fb1d2a](https://github.com/dotnet/docs/commit/7fb1d2a37828076c628607c43a7cabb58de9c343), [500c1d9](https://github.com/dotnet/docs/commit/500c1d90ffa18783bb0ab9f0494922a36bdfc1b8), [c81b647](https://github.com/dotnet/docs/commit/c81b647359dc9dd42b6a1d71b0ccf1caf113bb77), [6d4ae6b](https://github.com/dotnet/docs/commit/6d4ae6bd7055b3fe2ba3fe975db922c42a0c0c93), [26ac253](https://github.com/dotnet/docs/commit/26ac25314bfa8e2dc478484d6fbe7d44034e3672), [cc64143](https://github.com/dotnet/docs/commit/cc64143cb9e691d7668621429a96a167cf022214), [74844f0](https://github.com/dotnet/docs/commit/74844f077d685edd64a62ff8b6046f0cdb0299be), [47c1701](https://github.com/dotnet/docs/commit/47c17014d387be519cb5ab261b5db479263b7c0a), [d686801](https://github.com/dotnet/docs/commit/d68680132dade062859e052c4841ac422139c82f)

- Fixes typo in the following pages : 
    - `Containerizing monolithic applications`
    - `Development workflow for Docker apps`
    - `Implementing event-based communication between microservices (integration events)`
    - `Implementing reads/queries in a CQRS microservice`
    - `Implementing API Gateways with Ocelot`
    - `Creating a simple data-driven CRUD microservice`
    - ` Implementing a microservice domain model with .NET Core`
    - `Domain events. design and implementation`
    - `Using NoSQL databases as a persistence infrastructure`
    - `Handling partial failure`
    - `Testing ASP.NET Core services and web apps`
    - `Securing .NET Microservices and Web Applications`


- Fixes the code block annotation in the following pages :
    - `Development workflow for Docker apps`
    - `Use a database server running as a container`
    - `Defining your multi-container application with docker-compose.yml`
    - `Implementing API Gateways with Ocelot`
    - `Defining your multi-container application with docker-compose.yml`

- Fixes broken link in the following pages :
    - `Asynchronous message-based communication`
    - `Development workflow for Docker apps`
    - `Using Azure Key Vault to protect secrets at production time`
    - `Use IHttpClientFactory to implement resilient HTTP requests`
    - `Testing ASP.NET Core services and web apps`

- Changes docs prefix (https://docs.microsoft.com) in the following pages :
    - `Asynchronous message-based communication`
    - `Communication in a microservice architecture`
    - `The API gateway pattern versus the direct client-to-microservice communication`
    - `Challenges and solutions for distributed data management`
    - `State and data in Docker applications`
    - `Resiliency and high availability in microservices`
    - `Orchestrate microservices and multi-container applications for high scalability and availability`    
    - `Development workflow for Docker apps`
    - `Use IHttpClientFactory to implement resilient HTTP requests`
    - `Domain events. design and implementation`
    - `Implementing value objects`
    - `Implementing the infrastructure persistence layer with Entity Framework Core`
    - `Designing the microservice application layer and Web API`
    - `Implementing a microservice domain model with .NET Core`
    - `Using NoSQL databases as a persistence infrastructure`
    - `Creating a simple data-driven CRUD microservice`
    - `Implementing event-based communication between microservices (integration events)`
    - `Designing a microservice-oriented application`
    
*Contributions :* 

We’d like to acknowledge and thank the following community members for their valuable contributions !

[@zakaria-c](https://github.com/zakaria-c), [@nschonni](https://github.com/nschonni) , [@DCtheGeek](https://github.com/DCtheGeek), [@Youssef1313](https://github.com/Youssef1313)

### Release 3.1.2 (2020-09-02)

Reference commits : [6317237](https://github.com/dotnet/docs/pull/19901/commits/63172377dfad02406ff73dd83bf4c709ee2985c6), [add8374](https://github.com/dotnet/docs/pull/20332/commits/add8374835f7dff4569ddd8301261b727e54b839), [05f6d3f](https://github.com/dotnet/docs/pull/20359/commits/05f6d3f4240684c53ae4ddabded2fae1c1aaed52), [540ff78](https://github.com/dotnet/docs/pull/19315/commits/540ff78fe7e94aad24eae90d2e14acf9176bb94a), [0e1e2bb](https://github.com/dotnet/docs/pull/20006/commits/0e1e2bb0f48b469deaba882fb695e9d86f812c8f), [b0f28cb](https://github.com/dotnet/docs/pull/20131/commits/b0f28cb9204ba982b1b022359946edc80b042daf), [ce794ce](https://github.com/dotnet/docs/pull/19980/commits/ce794ce5f18592a5f5a3e8b8f4d475b7c4fb6b7b), [09db01f](https://github.com/dotnet/docs/pull/20412/commits/09db01f7d02c52dbeac15aa4888a599d94d99dc7)

- Updates MediatR related content. Page : `Implement the microservice application layer using the Web API`
- Adds the right `DbContext` object and rephrases sentences to make it more meaningful. Page: `Creating a simple data-driven CRUD microservice`
- Refactors ValueObject's Equals() method. Page : `Implement value objects`
- Rephrases few sentences for a better understanding of the context. Page : `Use IHttpClientFactory to implement resilient HTTP requests`
- Inclusion of `Ocelot v16.0.0` related breaking change note in the important section. Page : `Implement API Gateways with Ocelot`
- Updates `Ocelot API Gatway image`. Page : `Implement API Gateways with Ocelot`
- Fixes the following issues :
    - Typo in the configuration code snippet. Page: `Make secure .NET Microservices and Web Applications`
    - Additional closing curly brace in the code snippet. Page: `Health monitoring`
    - Additional resource links. Page : `Testing ASP.NET Core services and web apps`
    - Broken additional resource links. Page : `Testing ASP.NET Core services and web apps`
    - Repetitive definition of `IHostedService interface`. Page: `Creating a simple data-driven CRUD microservice`
    - Obsolete SQL server image name in `docker-compose.yml`. Page: `Development workflow for Docker apps`

