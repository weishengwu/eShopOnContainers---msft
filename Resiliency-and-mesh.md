# Resiliency and Service Mesh

Previous versions of eShopOnContainers used the [Polly library](https://github.com/App-vNext/Polly) to provide resiliency scenarios. Polly is a fantastic open source library that provides advanced resiliency scenarios and patterns like retries (with exponential backoff) or circuit breakers.

This version of eShops drops the use of Polly in the following cases:

* Http REST calls between microservices
* gRPC calls between microservices

Polly is still used to guarantee resiliency in database connections and RabbitMQ/Azure Service Bus connections, but is no longer used for resiliency between synchronous microservice-to-microservice communication.

## Service Mesh

In a production scenarios based on Kubernetes using a [Service Mesh](https://docs.microsoft.com/en-us/azure/aks/servicemesh-about) is a good option to provide resilienciy between your services.

A Service Mesh is a product that offers resiliency, observability and others features to your workloads running on the cluster. There are various meshes you can use and each one have its own characteristics, so you should evaluate carefully which one suits better your needs. Once installed the mesh will monitor all the traffic between your services and apply the needed policies. Those policies could be for resiliency (like using retries and/or circuit breakers) or for other tasks (like encrypt all traffic inside the cluster).

When you use a Mesh for resiliency, nothing special is needed **in your code**. The Mesh is a pure infrastructure concept, so your Kubernetes files will be affected, but your code won't. If the Mesh is controlling the network and applying a specific policy for making retries, these retries will be made automatically (at the Mesh level) whithout your code having any notice. From your code perspective, you have done a single call, that can either succeed of fail after some retries. If the mesh is applying an open circuit-breaker, your code won't know that: simply all your network calls will fail (until the circuit is closed again).

This simplifies your code, as allows you to focus on the business requeriments, and let the mesh apply the needed policies.

## Service Mesh and eShopOnContainers

The reason to drop Polly for microservice-to-microservice communications is to show the use of a [Service Mesh](https://docs.microsoft.com/en-us/dotnet/architecture/cloud-native/service-mesh-communication-infrastructure). One of the reasons to use a Service Mesh is to delegate on it the communications resiliency and set policies of retries, circuit breakers and QoS.

To use service mesh, is needed to deploy eShopOnContainers on a Kubernetes cluster. Using eShopOnContainers from docker host (using compose) can't use Service Mesh and in this case no resiliency for the communications is built.

eShopOnContainers is ready to use [Linkerd](https://linkerd.io) as Service Mesh. There were several options to choose from, we choose Linkerd mainly for its easy installation and configuration, and because has minimal impact on the cluster where is installed.

### Why Linkerd?

There are a various meshes out here, and selecting the right service mesh for your project can be a hard choice. Every mesh offers a set of features and follow distinct approaches to solve the same set of problems. Based on your experience, deployment operations, code management and requirements one mesh can fit better than other. 

So, **before choosing a specific service mesh, evaluate various options, play with some of them, and take a decision based on your experience and needs**. For eShopOnContainers we choose Linkerd as our current Mesh but this don't mean that Linkerd should be your mesh for your projects. In the future we don't discard to integrate eShop with other meshes as well.

Before selecting a Mesh, you should ask yourself some questions:

* Do you _really_ need the Mesh? A Mesh is a non-trivial piece of infrastructure that impacts your solution. Don't add complexity if it is not needed. Some of the problems that a Mesh solves can be solved using other ways (i. e. resiliency can be solved by Polly, A/B testing can be solved using different services and with standard ingress controller).

* Can your infrastructure support the Mesh? The mesh is not free. Usually every Mesh came with a set of containers run as a side-car containers for all your workload, plus additional containers running as a control plane. Those containers require CPU and memory to run.

If you evaluate those questions and come up with the answer that you want to use a Mesh, then you need to choose the right one for you. There are various options out here:

* [Istio](https://istio.io/): Istio is a full featured and highly customizable Mesh. It offers a lot of powerful features, but comes with a high learning curve and complex deployment (i. e. 80+ CRDs are added to your cluster). Although a basic installation of istio is not complex, get the real value of it requires significant ammount of work. Istio integrates a lot of different products (Envoy, Grafana, Prometheus, Jaeger, Kali) playing everyone a specific role inside the mesh.

* [Consul](https://www.consul.io/mesh.html): Consul from Hashicorp is another option for a service Mesh. Like istio it is based using Envoy a sidecars and offers a wide set of advanced capabilities.

* [Linkerd](https://linkerd.io/2/overview/): Linkerd (please note that we are always referring to Linkerd 2 when using the word "Linkerd"), is a lightweight and easy-to-install service Mesh. Do not offer the same broad range of capabilities that Istio or Consul, but is easier to install and start with.

**In eShopOnContainers we choose Linkerd, for its easy installation and setup**. Other meshes offers a broad range of services, but most of them go beyond the scope of a project like eShopOnContainers. However remind: evaluate the options, your needs before choosing your mesh (if any).

## Installing the Mesh

To use eShopOnContainers under Linkerd, you need to install Linkerd first in your cluster. This is an administrative task performed only once. We don't provide scripts for Linkerd installation, but the process is very straightforward and is clearly described on its [installation page](https://linkerd.io/2/getting-started/). Just follow steps 0 through 3.

## Enabling Mesh

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




