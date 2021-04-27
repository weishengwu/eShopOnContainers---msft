## eBook: Containerized Docker Application Lifecycle with Microsoft Platform and Tools

### Release 5.0.1 (2021-04-27)

*Reference commits :* [f03583f](https://github.com/dotnet/docs/pull/23895/commits/f03583f9ce85c4067c3946c7249192885d8612d6)

Includes GitHub related content in the following pages :

- `index.md`
- Under module `Microsoft-platform-tools-containerized-apps`
    - `index.md`
- Under module `docker-devops-workflow`
    - `index.md`
    - `docker-application-outer-loop-devops-workflow.md `

### Release 5.0 (2021-01-06)

*Reference commits :* [5ada0ba](https://github.com/dotnet/docs/pull/22242/commits/5ada0ba94f8e267993c6f2cba7db1237acfe8ce2), [c08d046](https://github.com/dotnet/docs/pull/22242/commits/c08d046f893d946a70163abc729aeeedcf88fdb3)

Updates `.NET 5` related content in the following pages :

- `Index`
- `Containerized Docker Application Lifecycle with Microsoft Platform and Tools`
- `Docker terminology`
- Under module `design-develop-containerized-apps`
	- `Development environment for Docker apps`
	- `Inner-loop development workflow for Docker apps`
	- `Use Docker Tools in Visual Studio on Windows`
	- `Visual Studio Tools for Docker on Windows`
	- `Monolithic applications`
	- `Build ASP.NET Core applications deployed as Linux containers into AKS/Kubernetes clusters`
- Under module `docker-devops-workflow`
	- `Docker application DevOps workflow with Microsoft tools`
	- `Steps in the outer-loop DevOps workflow for a Docker application`
	- `Creating CI/CD pipelines in Azure DevOps Services for a .NET application on Containers and deploying to a Kubernetes cluster`

### Release 3.1.1 (2020-11-10)

*Reference commits :* [b77b615](https://github.com/dotnet/docs/commit/153df0eaf4f6acd340e77818c6b617d9e554f004), [153df0e](https://github.com/dotnet/docs/commit/153df0eaf4f6acd340e77818c6b617d9e554f004), [b77b615](https://github.com/dotnet/docs/commit/b77b615d4b45334905c6e9dfa6b165abbcabc7d5), [fb43117](https://github.com/dotnet/docs/commit/fb431175564955b9beb6706de19a5ed9639995ee), [cc64143](https://github.com/dotnet/docs/commit/cc64143cb9e691d7668621429a96a167cf022214), [fcfbb09](https://github.com/dotnet/docs/commit/fcfbb094392830ef47d37a5c72fabef04bf34449), [a8bc0a6](https://github.com/dotnet/docs/commit/a8bc0a6478e569f2a8dca6a69bf5b2e4c2302d4e)

- Fixes the code block annotation in the following pages :
    - `Inner-loop development workflow for Docker apps`
    - `Using Windows PowerShell commands in a DockerFile to set up Windows Containers (Docker standard based)`
- Fixes broken link in the following pages :
    - `Visual Studio Tools for Docker on Windows`
- Removes orphaned images. 
- Changes docs prefix (https://docs.microsoft.com) in the following pages :
    - `Containerized Docker Application Lifecycle with Microsoft Platform and Tools`
    - `Manage production Docker environments`
    - `What is Docker?`    
- Updated ACR creation section in page `Build ASP.NET Core applications deployed as Linux containers into AKS/Kubernetes clusters`
- Updates docker file content in page ` Using Windows PowerShell commands in a DockerFile to set up Windows Containers (Docker standard based)`

*Contributions :* 

We’d like to acknowledge and thank the following community members for their valuable contributions !

[@nschonni](https://github.com/nschonni), [@DCtheGeek](https://github.com/DCtheGeek), [@stackoverjoe](https://github.com/stackoverjoe)


### Release 3.1 (2019-08-07)

Reference commit [b3d6542](https://github.com/dotnet/docs/pull/19798/commits/b3d6542eeeffa6819b51c80712f51026dea94714) ([PR #19798](https://github.com/dotnet/docs/pull/19798))

- Updated all the references to .NET Core 3.1.
- Updated cover page image.
- Updated Visual Studio 2019 related images.
- Updated Visual Studio Code(VS Code) related docker workflow
- Updated Azure CLI command parameters for AKS creation.
- Updated Azure CLI command parameters related to AKS deployment.
- Updated images related to AKS deployment. 
- Fixed the following issues :
    - Broken image links.
    - Incorrect image numbering in chapter - 4    
    - Broken Microsoft tools image.
    - Docker Desktop broken link.
    - Previous and Next Page broken link.


### Release 2.2 (2019-04-25)

Reference commit [6541f0d2](https://github.com/dotnet/docs/pull/12020/commits/6541f0d22e4248cb36a63d2c80d3fdf38aee1d74) ([PR #12020](https://github.com/dotnet/docs/pull/12020))

- Update to .NET Core 2.2 "wave" of technologies.
- Add a simple Docker analogy for newcomers.
- Update and extend the Docker terminology.
- Add the reference to related Microsoft guides/e-books.
- Add the section for challenges when using containers.
- Re-brand from Visual Studio Team Services to Azure DevOps Services.
- Re-brand Application Insights, Log Analytics and OMS to Azure Monitor.
- Focus orchestrator references mainly to Azure Kubernetes Services (AKS) and Azure Service Fabric.
- Update Docker container state manage references to current/recommended features.
- Add a section on getting started with Kubernetes.
- Introduce Azure Dev Spaces.
- Introduce Azure Service Fabric Mesh.
- Add section about deploying to AKS.
- Update references to new Docker Tools in Visual Studio.
- Add section on Visual Studio Code (VS Code) and Docker extension for VS Code.
- Update Docker image references to Microsoft Container Registry (MCR).
- Update samples to using Azure DevOps.
- Include section on creating Azure DevOps pipelines.
