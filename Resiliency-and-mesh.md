# Resiliency and Service Mesh

Previous versions of eShopOnContainers used the [Polly library](https://github.com/App-vNext/Polly) to provide resiliency scenarios. Polly is a fantastic open source library that provides advanced resiliency scenarios and patterns like retries (with exponential backoff) or circuit breakers.

This version of eShops drops the use of Polly in the following cases:

* Http REST calls between microservices
* gRPC calls between microservices

Polly is still used to guarantee resiliency in database connections and RabbitMQ/Azure Service Bus connections, but is no longer used for resiliency between synchronous microservice-to-microservice communication.

## Service Mesh

The reason to drop Polly for microservice-to-microservice communications is to show the use of a [Service Mesh](https://docs.microsoft.com/en-us/dotnet/architecture/cloud-native/service-mesh-communication-infrastructure). One of the reasons to use a Service Mesh is to delegate on it the communications resiliency and set policies of retries, circuit breakers and QoS.

To use service mesh, is needed to deploy eShopOnContainers on a Kubernetes cluster. Using eShopOnContainers from docker host (using compose) can't use Service Mesh and in this case no resiliency for the communications is built.

eShopOnContainers is ready to use [Linkerd](https://linkerd.io) as Service Mesh. There were several options to choose from, we choose Linkerd mainly for its easy installation and configuration, and because has minimal impact on the cluster where is installed.

## Enabling Mesh

To use eShopOnContainers under Linkerd, you need to install Linkerd first in your cluster. This is an administrative task performed only once. We don't provide scripts for Linkerd installation, but the process is very straightforward and is clearly described on its [installation page](https://linkerd.io/2/getting-started/). Just follow steps 0 through 3.

Once Linkerd is installed you can deploy eShopOnContainers. To enable the integration with Linkerd, pass the parameter `useMesh` to `$true` when running the `deploy-all.ps1` script. For the curious what this parameter does is pass the value `inf.mesh.enabled` to `true` to all helm charts. When this value is enabled the helm charts do:

1. Adds the `linkerd.io/inject: enabled` to all needed deployments.
2. Adds the annotations declared in file `ingress_values.yaml` to all ingress resources. Provided `ingress_values.yaml` is as follows:

```yaml
ingress:
  mesh:
    annotations:
      nginx.ingress.kubernetes.io/configuration-snippet: |
        proxy_set_header l5d-dst-override $service_name.$namespace.svc.cluster.local:$service_port;
        proxy_hide_header l5d-remote-ip;
        proxy_hide_header l5d-server-id;
``` 

This is the specific configuration needed to enable the integration between NGINX ingress (and/or Http Application Routing as is derived from NGINX) and Linkerd. If you use other ingress controller you will need to update this file accordingly, following the [Linkerd ingress integration](https://linkerd.io/2/tasks/using-ingress/) instructions.

## Service profiles

By default Linkerd only monitors the network status and gives you detailed results that you can view by using the `linkerd` CLI tool.

To enable retries and other network policies you must declare a _service profile_ for the specified service you want to be controlled. A very detailed explanation about service profiles is in the [Linkerd documentation](https://linkerd.io/2/tasks/setting-up-service-profiles/)

Just for reference we include service profiles for basket and catalog API. Feel free to update them, play with it and explore all Linkerd scenarios!

You can find the service profiles in folder `/k8s/linkerd`. Just use `kubectl apply` to apply them to the cluster. Once a service profile is applied, Linkerd is able to give you detailed statistics (by route) and apply retries and other policies.

**Note** Previous versions of eShopOnContainers had specific business scenarios to demo the [circuit breaker](https://en.wikipedia.org/wiki/Circuit_breaker_design_pattern) pattern. These secenarios have been removed as, when using Mesh, the circuit breakers are applied by the Mesh under-the-hoods, and the caller do not receive any specific information that a request has been aborted by the circuit breaker. Right now in Linkerd2 there is no specific option to set a circuit breaker policy. This could change in the future as the Mesh itself evolves.




