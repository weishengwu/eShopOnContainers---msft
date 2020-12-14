> **CONTENT**

- [2020-12-14 - Release 3.1.0](#2019-11-26---release-300)
  - [Highlights](#highlights)
  - [Details](#details)
    - [Changes](#Changes)
    - [Bug Fixes](#Bug-Fixes)
  - [Contributions](#Contributions)
- [2019-11-26 - Release 3.0.0](#2019-11-26---release-300)
  - [Highlights](#highlights---300)
  - [Details](#details---300)
    - [New folder structure](#new-folder-structure)
    - [Retired deployment scenarios](#retired-deployment-scenarios)

## 2020-12-14 - Release 3.1.0

The latest [3.1.0 release](https://github.com/dotnet-architecture/eShopOnContainers/releases/tag/3.1.0) contains multiple changes and bug fixes:

### Highlights

1. Updates to .NET Core 3.1.0
2. Refactors code for few of the code modules
3. Fixes few important bugs

### Details

  #### Changes

  - Removes unused using from different classes.
  - Updates Readme with relevant information.  
  - Updates app manifest to support helm 3.x+ and Kubernetes version 1.16.x+
  - Updates different npm package versions in WebSPA
  - Changes docker host DNS default value to `host.docker.internal`
  - Changes `OpenIdConnect` string literal to `OpenIdConnectDefaults.AuthenticationScheme`
  - Changes ReadAllBytes to ReadAllBytesAsync in PicController
  - Updates Solution file 

  #### Bug Fixes

  - Fixes SignalR 401 Unauthorized error.
  - Fixes different `typo` in the main `Readme` file.
  - Fixes Firewall specific rule check in the script.
  - Fixes disposing of direct instantiated objects in calalog service
  - Fixes typo in `Readme` and `appsetting.json` file. 
  - Fixes unit test cases
  - Fixes parameter error in multiarch job
  - Fixes WebSPA build error after updating sha hashes in `packages-lock.json`
  - Fixes missing claimsType for load testing
  - Fixes PurchaseUrl port in WebSPA `appsettings.json`
  - Fixes spelling mistake in code comment.
  - Fixes k8s manifest deployment error `invalid type for io.k8s.api.core.v1.ConfigMap.data` from macOS environment.

### Contributions

We’d like to acknowledge and thank the following community members for their valuable contributions !

@vishipayyallore, @markharwood101, @hfz-r, @smholvoet, @InstanceFactory, @EdmondShtogu, @nsedoud, @H3RSKO, @MajidAliKhanQuaid, @fjvela, @jeremiahflaga, @zakaria-c, @wojciechrak , @anjoy8, @m-knet, @n-stefan, @synercoder , @Rosenberg96

## 2019-11-26 - Release 3.0.0

The latest [3.0.0 release](https://github.com/dotnet-architecture/eShopOnContainers/releases/tag/3.0.0) contains a **LOT** of changes and new features:

### Highlights - 3.0.0

1. Update to .NET Core 3.0
2. Use of gRPC for microservice-to-microservice communication
3. Use of Envoy Proxy for BFF
4. Repo cleanup
5. Initial Service Mesh support
6. Revise deployment scenarios

### Details - 3.0.0

- Migrate solution from ASP.NET Core 2.2 to 3.0 and update all projects to use the latest .NET Core 3.0 templates.

- Implement the new .NET Core 3.0 WorkerService in Ordering.API and other background processes.

- Improve Ordering.API
  - Group order items
  - apply discounts from Marketing.API

- Handle two deployment scenarios
  - Basic deployment, better for learning:
    - [Visual Studio (F5 experience)](https://github.com/dotnet-architecture/eShopOnContainers/wiki/Windows-setup#optional---use-visual-studio)
    - [Docker compose on windows](https://github.com/dotnet-architecture/eShopOnContainers/wiki/Windows-setup)
    - [Docker compose on macOS](https://github.com/dotnet-architecture/eShopOnContainers/wiki/Mac-setup)
    - [Local Kubernetes](https://github.com/dotnet-architecture/eShopOnContainers/wiki/Deploy-to-Local-Kubernetes)

  - Advanced deployment, complex but more real-life:
    - [Deploy to AKS with a Service Mesh for resiliency](https://github.com/dotnet-architecture/eShopOnContainers/wiki/Deploy-to-Azure-Kubernetes-Service-(AKS))
      - Sidecar implementation with Envoy/Linkerd
      - Improved API Gateway and resilience
      - gRPC for microservice-to-microservice communications
      - Dev Spaces support (only for containers that don't use gRPC)

#### New folder structure

The repo also has a new, simpler, folder structure, as shown in the following image:

![](images/Release-Notes/new-folder-structure.png)

In the above image you can see that the first folder level contains, basically:

- **build**: Scripts for building Docker images.
- **deploy**: Scripts for deployment.
- **src**: All source projects, including tests.
  - **ApiGateways**: Envoy configuration and Aggregators source code.
  - **BuildBlocks**: Common components used by several projects.
  - **Mobile**: Mobile apps projects.
  - **Services**: Backend for all services. Including unit and functional tests for some projects.
    - Basket
    - Catalog
    - Identity
    - Location
    - Marketing
    - Ordering
    - Payment
    - Webhooks
  - **Tests**: General functional application tests.
  - **test-results**: Test results
  - **Web**: Web applications

#### Retired deployment scenarios

- Service Fabric & Service Fabric Mesh.
- Kubernetes using YAML (only Helm charts are supported)
- CLI scripts for build and push (docker-compose and docker multi-stage are used)
