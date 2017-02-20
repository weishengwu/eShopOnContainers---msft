This environment is a mix between the VS 2017 environment and a Windows CLI environment. Therefore, in this case sometimes you might want to build/run/debug the solution through VS 2017 and other times you might want to build/run by using the CLI (Command line interface plus PowerShell scripts and "docker-compose up/build" CLI).

In regards the required SDK installation for using the CLI, you need first to follow the same steps than the ones specified in the CLI setup, here:  

https://github.com/dotnet/eShopOnContainers/wiki/Setting-the-eShopOnContainers-solution-up-in-a-Windows-CLI-environment-(dotnet-CLI,-Docker-CLI-and-VS-Code)

However, there are few additional steps to be performed so the VS 2017 configuration matches the CLI configuration and you don't have conflicts.

VS config about external NODE/NPM path, etc....
