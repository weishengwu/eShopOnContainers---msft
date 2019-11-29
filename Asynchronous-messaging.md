**IMPORTANT NOTICE**

The [asynchronous messaging implementations used in eShopOnContainers](https://github.com/dotnet-architecture/eShopOnContainers/tree/dev/src/BuildingBlocks/EventBus) to handle integration events, are simplified versions that have value in as much as they're useful for grasping the main concepts and scenarios.

**DON'T USE THEM IN PRODUCTION**.

For production-grade messaging solutions you can take a look at the following resources:

- **Azure Service Bus** \
  <https://docs.microsoft.com/azure/service-bus-messaging/>

- **NServiceBus** \
  <https://particular.net/nservicebus>

- **MassTransit** \
  <https://masstransit-project.com/>

- **EasyNetQ** \
  <http://easynetq.com/>

You can also evaluate other messaging solutions such as:

- **Brighter** \
  <https://www.goparamore.io/>

- **CAP** \
  <http://cap.dotnetcore.xyz/>

You can also explore some asynchronous messaging implementations for eShopOnContainers in the following GitHub repos:

- Using [**NServiceBus**](https://particular.net/nservicebus): <https://github.com/Particular/eShopOnContainers/tree/archive>

- Using [**CAP**](http://cap.dotnetcore.xyz/): <https://github.com/yang-xiaodong/eShopOnContainers>
