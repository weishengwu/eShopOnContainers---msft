## Related branch in GitHub
As of Feb. 2017, the related branch for working with VS 2015 and project.json projects is this:
**migration/net11**

It might be migrated/renamed to a branch called **vs2015**.

**IMPORTANT NOTE:** The branch supporting VS 2015 and project.json projects has been "deprecated" and even when it should work in VS 2015 and plain dotnet CLI and Docker CLI, this version will not get functional/features updates like the version for VS2017 and .CSPROJ projects that also works with the CLI.
Basically, the eShopOnhContainers with project.json projects **migration/net11** is the branch that is deprecated and not being evolving anymore.

## Development Environment Setup
### Requirements for January 2016 version of eShopOnContainers

WINDOWS DEV MACHINE
- Visual Studio 2015 with latest Update
- .NET Core 1.1 setup (Including ASP.NET Core and VS Tooling)
- Bower and Gulp as global installs (See steps below)
- <a href='https://docs.docker.com/docker-for-windows/'>Docker for Windows</a>

MAC DEV MACHINE
- Visual Studio Code
- .NET Core 1.1 for Mac - setup
- Bower and Gulp as global installs (See steps below)
- <a href='https://docs.docker.com/docker-for-mac/'>Docker for Mac</a>

### Installing and configuring Docker in your development machine

#### Set needed assigned Memory and CPU to Docker
In this application (January 2017 version) we run 1 instance of SQL Server running as a container with multiple databases (one DB per microservice), plus 6 ASP.NET Core apps/services and 1 Redis server, all of them running as Docker containers. So, especially because of SQL Server requirements on memory, it is important to set Docker up properly with enough memory RAM and CPU assigned to it or you will get difficult errors when starting the containers with "docker-compose up". 
Once Docker for Windows/Mac is installed in your machine, enter into its Settings and the Advanced menu option so you are able to adjust it to the minimum amount of memory and CPU (Memory: Around 4096MB and CPU:3) as shown in the image. Usually you might need a 16GB memory machine for this configuration if you also want to run the Android emulator for the Xamarin app at the same time. If you have a less powerful machine, you can try with a lower configuration and/or by not starting certain containers like the basket and Redis. But if you don't start all the containers, the application will not fully function properly, of course. 

<img src="img/docker_settings.png">

#### Share drives in Docker settings (In order to deploy and debug with Visual Studio 2017)
(Note, this is not required if running from Docker CLI with docker-compose up and using VS 2015 or any other IDE or Editor)<p>
In order to deploy/debug from Visual Studio 2017, you'll need to share the drives from Settings-> Shared Drives in the "Docker for Windows" configuration.
If you don't do this, you will get an error when trying to deploy/debug from VS 2017, like "Cannot create container for service yourApplication: C: drive is not shared". <p>


<img src="img/docker_settings_shared_drives.png">

#### Node, Bower and Gulp installation
(These steps about installing bower and gulp might not be needed anymore as these are being triggered from the project.json in the MVC project at the section 'prepublish":'). However, this will need to be migrated to .csproj when migrating to VS 2017. <p>
Before generating the Docker images, and specifically when generating the web apps binaries with "dotnet publish" from the custom scripts (like when running the build-images.ps1 script from PowerShell or the build-images.sh from bash in a Mac), it needs to have access to the paths where you have installed Bower and Gulp. For that, the recommendation is to install Bower and Gulp with a global installation by running the following commands from command-line or bash:
- Install Node if you don't have it installed, from here: https://nodejs.org/en/ 
 <img src="img/Node_setup_for_npm.png">
- After you install Node, you need to align that installed version with the version used by Visual Studio, so you need to make sure that VS2017 is using the same nodejs that you are using from command line.<br>
**Go to "Tools -> Options -> Project and Solutions -> Web Package Management -> External Web Tools"** and ensure that the nodejs you use from command line is listed before the entry "$(VSINSTALLDIR)\Web\External"
- Install Bower and Gulp with the following npm commands (npm is installed as part of Node)

    `npm install -g bower` 

    `npm install -g gulp`

Below you can see how those commands are run in Windows:
<img src="img/Bower_and_Gulp_setup.png">


## Build, Ship, Run 
In the global directory you will find the scripts needed to build, deploy and run the application into your local Docker development machine. The steps are the following: 

### Compile the .NET apps and Build the Docker images
- Open a PowerShell window in Windows, move to the root folder of your solution and run the <b>build-images.ps1</b> script file like in the following screenshot.

<b>IMPORTANT</b>: This script deletes all the Docker images registered in your local dev machine repository before creating the new images, so it is starting from a 100% clean state. If you don't want your local images in your PC to be deleted, edit and change the <b>build-images.ps1</b> script file before you run it.

- This Power-Shell script that you will find in the <u>root directory of the solution</u> is responsible for building the .NET applications, copy the binaries in a pub folder and use Docker CLI commands to build the custom Docker images needed to run the containers. You can see how to run that PowerShell script in the screenshot below:
<img src="img/Generating_Docker_Images.png">

- Once it finishes, you can check it out with Docker CLI if the images were generated correctly by typing in the PowerShell console the command: `docker images`
<img src="img/list-of-images.png">
Those Docker images are the ones you have available in your local image repository in your machine.
You might have additional images, but at least, you should see the following list of images which are 6 custom images starting with the prefix "eshop" which is the name of the image repo. The rest of the images that are not starting with "eshop" will probably be official base-images like the microsoft/aspnetcore or the SQL Server for Linux images.

### Deploy containers into your Docker host
You can deploy Docker containers to a regularDocker host either by using the `docker run` command which need to be executed once per microservice, or by using the CLI tool `docker-compose up` which is very convenient for multi-container applications as it can spin-up all the multiple containers in your application with a single command. These are the steps:
- <b>Run your containers in your local host</b>: Open your favorite command tool (PowerShell od CommandLine in Windows / Bash in Mac) <u> and move to the root directory of the solution</u> where the docker-compose.yml file is located and run the command `docker-compose up`. When running "docker-compose up" you should see something similar to the following screenshot in the PowerShell command window, although it will much longer than that, also showing many internal SQL commands from the services when populating the first time the sample data.
`docker-compose up`
<img src="img/docker-compose-up-1.png">

- Note that the first time you run any container (with docker run or docker-compose) it detects that it needs the base images we are using, like the SQL Server image and the Redis image, so it will pull or download those base images from the Internet, from the public repo at the Docker registry named DOCKER HUB, by pulling the "microsoft/mssql-server-linux" which is the base image for the SQL Server for Linux on containers, and the "library/redis" which is the base Redis image. Therefore, the first time you run docker-compose it might take a few minutes pulling those images before it spins up your custom containers.
The next time you run docker-compose up, since it'll have those base images already pulled/downloaded, it will just start the containers, like in the following screenshot:
<img src="img/docker-compose-up-2.png">

- <b>Check out the containers running in your Docker host</b>: Once docker-compose up finishes after a few minutes, you will have that PowerShell showing the execution's output in a "wait state", so in order to ask to Docker about "how it went" and see what containers are running, you need to open a second PowerShell window and type "docker ps" so you'll see all the running containers, as shown in the following screenshot.
<img src="img/docker-ps-with-all-microservices.png"> 
You can see the 6 custom containers running the microservices plus the 2 web applications. In adition you have the containers with the SQL databases and the Redis cache for the basket microservice data.


#### IMPORTANT: Open ports in Firewall so Authentication to the STS (Security Token Service container) can be done through the 10.0.75.1 IP which should be available and already setup by Docker
- You can manually create a rule in your local firewall in your development machine or you can also create that rule by just executing the <b>add-firewall-docker.ps1</b> script in the solution's root. 
- Basically, you need to open the ports 5100 to 5105 that are used by the solution by creating an IN-BOUND RULE in your firewall, as shown in the screenshot below (for Windows).
<img src="img/firewall-rule-for-eshop.png"> 


### Test the applications and microservices
Once the deploy process of docker-compose finishes you should be able to access the services in the following URLs or connection string, from your dev machine:

<a href="" target="top"></a>
- Web MVC: <a href="http://localhost:5100" target="top">http://localhost:5100</a>
- Web Spa: <a href="http://localhost:5104" target="top">http://localhost:5104</a> (Important, check how to set up the SPA app and requirements before building the Docker images. Instructions at  https://github.com/dotnet/eShopOnContainers/tree/master/src/Web/WebSPA/eShopOnContainers.WebSPA or the README.MD from eShopOnContainers/src/Web/WebSPA/eShopOnContainers.WebSPA)
- Catalog microservice: <a href="http://localhost:5101" target="top">http://localhost:5101</a> (Not secured)
- Ordering microservice: <a href="http://localhost:5102" target="top">http://localhost:5102</a> (Requires token for authorization)
- Basket microservice: <a href="http://localhost:5103" target="top">http://localhost:5103</a> (Requires token for authorization)
- Identity microservice: <a href="http://localhost:5105" target="top">http://localhost:5105</a>
- Orders database (SQL Server connection string): Server=tcp:localhost,5432;Database=Microsoft.eShopOnContainers.Services.OrderingDb;User Id=sa;Password=Pass@word;
- Catalog database (SQL Server connection string): Server=tcp:localhost,5434;Database=CatalogDB;User Id=sa;Password=Pass@word
- ASP.NET Identity database (SQL Server connection string): Server=localhost,5433;Database=aspnet-Microsoft.eShopOnContainers;User Id=sa;Password=Pass@word
- Basket data (Redis): listening at localhost:6379
 
#### Trying the Web MVC application with the DemoUser@microsoft.com user account
When you try the Web MVC application by using the url http://localhost:5100, you'll be able to test the home page which is also the catalog page. But when trying to add any article to the basket you will get redirected to the login page which is handled by the STS microservice (Security Token Service). At this point, you could register your own user/customer or you can also use a convenient default user/customer named DemoUser@microsoft.com so you don't need to register your own user and it'll be easier to test.
The credentials for this demo user are:
- User: demouser@microsoft.com
- Password: Pass@word1

Below you can see the login page when providing those credentials.
<img src="img/login-demo-user.png">

#### Trying the Xamarin.Forms mobile apps for Android, iOS and Windows
By default, this app shows fake data from mock-services. In order to really access the microservices/containers in Docker from the mobile app, you need to:
 - Disable mock-services in the Xamarin app by setting the <b>UseMockServices = false</b> in the App.xaml.cs and specify the host IP in  BaseEndpoint = "http://10.106.144.28" at the GlobalSettings.cs. Both files in the Xamarin.Forms project (PCL).
 - Another alternative is to change that IP through the app UI, by modifying the IP address in the Settings page of the App as shown in the screenshot below. 
- In addition, you need to make sure that the used TCP ports of the services are open in the local firewall. <img src="img/xamarin-settings.png">


### Deploying individiual services into Docker
Under each project root you will find a readme.md file which describes how to run and deploy the service individually into a docker host.

> ### Note on Windows Containers
> As mentioned, the development and testing of this project (January 2017 version) was done on Docker Linux containers running in development machines with "Docker for Windows" and the default Hyper-V Linux VM (MobiLinuxVM) installed by "Docker for Windows". 
In order to run the application on Windows Containers you'd need to change the base images used by each container:
> - Official .NET Core base-image for Windows Containers, at Docker Hub: https://hub.docker.com/r/microsoft/dotnet/ (Using the Windows Nanoserver tag)
> - Official base-image for SQL Server on Windows Containers, at Docker Hub: https://hub.docker.com/r/microsoft/mssql-server-windows


