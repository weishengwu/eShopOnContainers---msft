The Web SPA application needs a few additional steps to make it work due to its JavaScript frameworks dependencies and JS code to be built before generating the Docker Images.

## Requirements and set up


### Install NPM
In order to be able to build the JavaScript dependencies from command line by using npm you need to install npm globally.

NPM is bundled with NODE.JS. Installing NPM and NODE is pretty straightforward by using the installer package available at https://nodejs.org/en/

<img src="img/spa/installing_npm_node.png">
You can install the version "Recommended For Most Users" of Node which at the moment of this writing was v6.9.3 LTS and comes with a newer version of NPM.
You can see the installed NPM version with the command <b>npm -v</b>, as shown below.
<p>
<img src="img/spa/npm-versions-powershell.png">

### Set NPM path into Visual Studio
NPM will be usually installed under this path:
<b>C:\Program Files (x86)\nodejs</b>.
You need to update that path in Visual Studio  under the "External Web Tools" location paths, as shown below:
<p>
<img src="img/spa/vs-tools-path-custom-node.png">
If you don't do this step you might have issues because of using different versions from VS or command line.
See:
http://www.hanselman.com/blog/VisualStudio2015FixingDependenciesNpmNotInstalledFromFseventsWithNodeOnWindows.aspx


### Build the SPA app with NPM
Now, you need to build the SPA app (TypeScript and Angular 2 based client app) with NPM.
* Open a command-prompt window and move to the root of the SPA application (src\Web\WebSPA\eShopOnContainers.WebSPA)
* Run the command <b>npm run build:prod</b> as shown below:
<p>
<img src="img/spa/npm-run-build.png">

If you get an error like <b>"Node Sass could not find a binding for your current environment: Windows 64-bit with Node.js 6.x"</b>, then run the command <b>npm rebuild node-sass</b> as in the following screenshot:
<img src="img/spa/npm-rebuild-node-sass.png">
Then, run again the <b>npm run build:prod</b> command that should finish with no errors.


### Build the Docker images and Deploy the containers
At this point you can choose between any of the two following options to build and deploy the Docker containers:
1. VS 2017 based: Build and deploy in a single step from Visual Studio 2017 as explained in this page: https://github.com/dotnet/eShopOnContainers/wiki/Setting-eShopOnContainer-solution-up-in-a-Visual-Studio-2017-environment 
2. CLI in Windows: Build the .NET bits with the dontnet CLI by using the Windows PowerShell script build-bits.ps1, then create the Docker images and deploy to the Docker host with "docker compose up/build", as explained in this page: https://github.com/dotnet/eShopOnContainers/wiki/Setting-the-eShopOnContainers-solution-up-in-a-Windows-CLI-environment-(dotnet-CLI,-Docker-CLI-and-VS-Code)
3. CLI in Mac: Build the .NET bits with the dontnet CLI by using the Mac Bash script 
build-bits.sh, then create the Docker images and deploy to the Docker host with "docker compose up/build", as explained in this page: https://github.com/dotnet/eShopOnContainers/wiki/Setting-eShopOnContainer-solution-up-in-a-Mac,-VS-Code-and-CLI-environment


