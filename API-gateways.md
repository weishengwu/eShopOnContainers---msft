# API Gateways

eShopOnContainer use 4 API Gateways that implement the BFF pattern. Overall architecture is:

![Overall architecture of eShop](./images/Architecture/eshop-arq.png)

The image above is the architecture when running eShopOnContainers on Kubernetes with Service Mesh enabled. If Service Mesh is disabled all the "Linkerd" containers do not exist and if running outside Kubernetes the "Ingress controller" do not exists and you access directly to API Gateways.

In this architecture the 4 blue boxes in the column labelled as "eShop Ingress" are the four BFFs.

Currently they are implemented using [Envoy](https://www.envoyproxy.io/). Each BFF provides a unique entrypoint for its clients and then forwards the call to the specific microservice or the custom aggregator.

The communication between BFF and the microservices is always using HTTP/REST. This could change in the future by using gRPC from the BFF to the microservices, while mantaining a HTTP/REST façade from the BFFs to the clients.

**Note**: The communication between the aggregators and the microservices is using gRPC, but between the BFFs and the aggregators is still HTTP/REST.