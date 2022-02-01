This page contains links to README files about deploying Azure resources, see [Using Azure resources](Using-Azure-resources) for details on using them with eShopOnContainers.

All related information is in the folder [**deploy/azure on the eShopOnContainers repo](https://github.com/dotnet-architecture/eShopOnContainers/tree/dev/deploy/azure/az).

## Pre-requisites

1. [Azure CLI 2.0 Installed](https://docs.microsoft.com/cli/azure/install-azure-cli)
2. Azure subscription created

Login into your azure subscription by typing `az login` (note that you maybe need to use `az account set` to set the subscription to use). Refer to [this article](https://docs.microsoft.com/cli/azure/authenticate-azure-cli) for more details

## Deploying using CLI

See the [README for Azure resource creation scripts](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/deploy/az/readme.md).

### Azure resources used by the services

1. [Deploying SQL Server and databases](https://github.com/dotnet-architecture/eShopOnContainers/tree/dev/deploy/azure/az/sql/readme.md)
2. [Deploying Azure Service Bus](https://github.com/dotnet-architecture/eShopOnContainers/tree/dev/deploy/azure/az/servicebus/readme.md)
3. [Deploying Redis Cache](https://github.com/dotnet-architecture/eShopOnContainers/tree/dev/deploy/azure/az/redis/readme.md)
4. [Deploying CosmosDb](https://github.com/dotnet-architecture/eShopOnContainers/tree/dev/deploy/azure/az/cosmos/readme.md)
5. [Deploying Catalog Storage](https://github.com/dotnet-architecture/eShopOnContainers/tree/dev/deploy/azure/az/storage/catalog/readme.md)
