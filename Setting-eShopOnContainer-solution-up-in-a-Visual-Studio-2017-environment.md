## Setting eShopOnContainers up in a Visual Studio 2017 development machine

Windows dev machine with Visual Studio 2017 and Docker for Windows installetion requirements:
- <a href='https://docs.docker.com/docker-for-windows/install/'>Docker for Windows</a> installed
- <a href='https://www.visualstudio.com/vs/'>Visual Studio 2017 installed </a> (Latest version)
- Bower and Gulp as global installs (See steps below)

### Installing and configuring Docker in your development machine

#### Install Docker for Windows
Install Docker for Windows (The Stable channel should suffice) from this page: https://docs.docker.com/docker-for-windows/install/
About further info on Docker for windows, check this additional page
https://docs.docker.com/docker-for-windows/ 

Docker for Windows uses Hyper-V to run a Linux VM which is the by default Docker host. If you don't have Hyper-V installed/enabled, it'll be installed and you will probably need to reboot your machine.

**IMPORTANT**: Check that you don't have any other hypervisor installed that might be not compatible with Hyper-V. For instance, Intel HAXM can be installed by VS 2017 if you chose to install Google's Android emulator which works on top of Intel HAXM. In that case, you'd need to uninstall Google's Android emulator and Intel HAXM.
VS 2017 recommends to install the Google Android emulator because it is the only Android emulator with support for Google Play Store, Google Maps, etc. However, take into account that it currently is not compatible with Hyper-V, so you might have incompatibilities with this scenario.

#### Set needed assigned Memory and CPU to Docker
For the development environment of eShopOnContainers, by default, it runs 1 instance of SQL Server running as a container with multiple databases (one DB per microservice), other 6 additional ASP.NET Core apps/services each one running as a container, plus 1 Redis server running as a container. Therefore, especially because of the SQL Server requirements on memory, it is important to set Docker up properly with enough memory RAM and CPU assigned to it or you will get errors when starting the containers with VS 2017 or "docker-compose up".

Once Docker for Windows is installed in your machine, enter into its Settings and the Advanced menu option so you are able to adjust it to the minimum amount of memory and CPU (Memory: Around 4096MB and CPU:3) as shown in the image. Usually you might need a 16GB memory machine for this configuration if you also want to run the Android emulator for the Xamarin app or multiple instances of applications demanding significant memory at the same time. If you have a less powerful machine, you can try with a lower configuration and/or by not starting certain containers like the basket and Redis. But if you don't start all the containers, the application will not fully function properly, of course. 

<img src="img/docker_settings.png">

#### Share drives in Docker settings (In order to deploy and debug with Visual Studio 2017)
(Note, this is not required if running from Docker CLI with docker-compose up and using VS 2015 or any other IDE or Editor)<p>
In order to deploy/debug from Visual Studio 2017, you'll need to share the drives from Settings-> Shared Drives in the "Docker for Windows" configuration.
If you don't do this, you will get an error when trying to deploy/debug from VS 2017, like "Cannot create container for service yourApplication: C: drive is not shared". <p>
The drive you'll need to share depends on where you place your source code.


<img src="img/docker_settings_shared_drives.png">


### Installing and configuring Visual Studio 2017 in your development machine

#### Install Visual Studio 2017
Once you have the bits downloaded locally, run the VS 2017 setup file and select the following workloads depending on the apps you intend to test or work with:

##### Working only with the server side (Microservices and web applications) - Workloads

- ASP.NET and web development
- .NET Core cross-platofrm development
- Azure development (Optional) - It is optional but recommended in case you want to deploy to Docker hosts in Azure or use any other infrastructure in Azure.
<img src="img/vs2017/vs2017_server_workload.png">

##### Working with the mobile app (Xamarin Mobile apps for iOS, Android and Windows UWP) - Workloads
If you also want to test/work with the eShopOnContainer model app based on Xamarin, you need to install the following additional workloads:
- Mobile development with .NET (Xamarin)
- Universal Windows Platform development
- .NET desktop development (Optional) - This is not required, but just in case you also want to make tests consuming the microservices from WPF or WinForms desktop apps

<img src="img/vs2017/vs2017_additional_mobile_workloads.png">

IMPORTANT: As mentioned above, make sure you are NOT installing Google's Android emlulator with Intel HAXM hypervisor or you will run on an incompatibility and Hyper-V won't work in your machine, therefore, Docker for Windows wont work when trying to run the Linux host or any host witih Hyper-V. 

Make sur eyou are NOT selecting
the highlighted options below with a red arrows:

<img src="img/vs2017/xamarin-workload-options.png">

### Clone the eShopOnContainers code from GitHub
**As of February 2017**, the branch to clone/download from GitHub compatible with Visual Studio 2017 is the branch named **vs2017**:

<img src="img/vs2017/github-clone-branch.png">

So make sure you switch to that branch in VS 2017 after cloning or clone that beanch with a Git command, from command prompt or PowerShell, similar to:

    git clone -b vs2017 https://github.com/dotnet/eShopOnContainers.git


### Open eShopOnContainers solution, Build, Run

#### Open eShopOnContainers solution in Visual Studio 2017

- If testing/working only with the server-side applications and services, open the solution: **eShopOnContainers-ServicesAndWebApps.sln**

- If testing/working either with the servier-side applications and services plus the Xamarin mobile apps, open the solution: **eShopOnContainers.sln**

Below you can see the full **eShopOnContainers-ServicesAndWebApps.sln** solution (server side) opened in Visual Studio 2017:

<img src="img/vs2017/vs-2017-eshoponcontainers-servicesandwebapps-solution.png">

Note how VS 2017 loads the docker-compose.yml files in a special node-tree so it uses that configuration to deploy/debug all the containers configured, at the same time into your Docker host.

#### Build and run eShopOnContainers from Visual Studio 2017

##### Set docker-compose as the default StartUp project
In case it is not your "by default project", right click on the "docker-compose" node and select the "Set as Startup Project" menu option, as shwon below:
<img src="img/vs2017/set-docker-node-as-default.png">

At this point, after waiting sometime for the Nuget packages to be properly restored, you should be able to build the whole solution or even directly deploy/debug it into Docker by simple hitting F5 or pressing the debug "Play" button that now should be labeled as "Docker": 

<img src="img/vs2017/debug-F5-button.png">

VS 2017 should compile the .NET projects, then create the Docker images and finally deploy the containers in the Docker host (your by default Linux VM in Docker for Windows). Finally, because the docker-compose configuration project is configured to open the MVC application, it should open your by default browser and show the MVC application with data coming from the microservices/containers:
<img src="img/vs2017/vs2017-f5-with-eshoponcontainers-web-mvc-in-browser.png">

Here's how the docker-compose configuration project is configured to open the MVC application:

<img src="img/vs2017/docker-compose-properties.png">

Finally, you can check out how the multiple containers are runnin in your Docker host by running the command **"docker ps"** like below:

<img src="img/vs2017/docker-ps.png">

You can see the 8 containers are running and what ports are being exposed, etc.

### Debug with several breakpoints across the multiple containers/projects

Something very compelling and productive in VS 2017 is the capability to debug several breakpoints across the multiple containers/projects.
For instance, you could set a breakpoint in a controller within the MVC web app plus a second breakpoint in a second controller within the Catalog Web API microservice, then refresh the browser if you were still running the app or F5 again, and VS will be stopping within your microservices running in Docker as shown below! :)

Breakpoint at the MVC app running as Docker container in the Docker host:
<img src="img/vs2017/debugging-mvc-app.png">

Press F5 again...

Breakpoint at the Catalog microservice running as Docker container in the Docker host:
<img src="img/vs2017/debugging-webapi-microservice.png">

And that's it! Super simple! Visual Studio is handling all the complexities under the covers and you can directly do F5 and debug a multi-container application! 





