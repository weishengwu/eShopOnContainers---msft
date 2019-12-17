The initial Docker for Desktop configuration is not suitable to run eShopOnContainers because it runs a total of 25 Linux containers.

Even though the microservices are rather light, the application also runs SQL Server, Redis, MongoDb, RabbitMQ and Seq as separate containers. The SQL Server container has four databases (for different microservices) and takes an important amount of memory.

 So it's important to configure enough memory RAM and CPU to Docker.

## Memory and CPU

Once Docker for Windows is installed, go to the Settings > Advanced option to configure the minimum amount of memory and CPU:

- Memory: 4096 MB
- CPU: 2

This amount of memory is the absolute minimum to have the app running, and that's why you'll a 16GB RAM machine for optimal configuration.

![](images/Docker-configuration/eshoponcontainers-docker-configuration-memory-cpu.png)

[What can I do if my computer only has 8 GB RAM?](#low-memory-configuration)

## Shared drives

This step is optional but recommended, as Docker sometimes needs to access the shared drives when building, depending on the build actions.

This is not really necessary when building from the CLI, but it's mandatory when building from Visual Studio to access the code to build.

The drive you'll need to share depends on where you place your source code.

![](images/Docker-configuration/eshoponcontainers-docker-configuration-shared-drives.png)

## Networking

IMPORTANT: Ports 5100 to 5105 must be open in the local Firewall, so authentication to the STS (Security Token Service container, based on IdentityServer) can be done through the 10.0.75.1 IP, which should be available and already setup by Docker. These ports are also needed for client remote apps like Xamarin app or SPA app in a remote browser.

You can manually create a rule in your local firewall in your development machine or you can just run the **`add-firewall-rules-for-sts-auth-thru-docker.ps1`** script available in the solution's **`deploy\windows\`** folder.

![](images/Docker-configuration/firewall-rule-for-eshop.png)

**NOTE:** If you get the error **Unable to obtain configuration from: `http://10.0.75.1:5105/.well-known/openid-configuration`** you might need to allow the program `vpnkit` for connections to and from any computer through all ports.

If you are working within a corporate VPN you might need to run this power shell command every time you power up your machine, to allow access from `DockerNAT` network:

```
Get-NetConnectionProfile | Where-Object { $_.InterfaceAlias -match "(DockerNAT)" } | ForEach-Object { Set-NetConnectionProfile -InterfaceIndex $_.InterfaceIndex -NetworkCategory Private }
```

## Low memory configuration

If your computer only has 8 GB RAM, you **might** still get eShopOnContainers up and running, but it's not sure and you will not be able to run Visual Studio. You might be able to run VS Code and you'll be limited to the CLI. You might even need to run Chromium or any other bare browser, Chrome will most probably not do. You'll also need to close any other program running in your machine.

The easiest way to get Chromium binaries directly from Google is to install the [node-chromium package](https://www.npmjs.com/package/chromium) in a folder and then look for the `chrome.exe` program, as follows:

1. Install node.

2. Create a folder wherever best suits you.

3. Run `npm install --save chromium`

4. After installation finishes go to folder `node_modules\chromium\lib\chromium\chrome-win` (in Windows) to find `chrome.exe`

The installation process should look something like this:

![](images/Docker-configuration/install-chromium-browser.png)

## Additional resources

- **[eShopOnContainers issue] Can't display login page on MVC app** \
  <https://github.com/dotnet-architecture/eShopOnContainers/issues/295#issuecomment-327973650>

- **[docs.microsoft.com issue] Configuring Windows vEthernet Adapter Networks to Properly Support Docker Container Volumes** \
  <https://github.com/dotnet/docs/issues/11528#issuecomment-486662817>

- **[eShopOnContainers PR] Add Power Shell script to set network category to private for DockerNAT** \
  <https://github.com/dotnet-architecture/eShopOnContainers/pull/1019>

- **Troubleshoot Visual Studio development with Docker (Networking)** \
  <https://docs.microsoft.com/en-us/visualstudio/containers/troubleshooting-docker-errors?view=vs-2019#errors-specific-to-networking-when-debugging-your-application>
