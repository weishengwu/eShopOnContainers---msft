# gRPC

One of the big news on netcore 3.0 is the native support for gRPC. eShopOnContainers makes use of gRPC for internal microservice-to-microservice synchronous communication. Note that, in eShop most of the communication between microservices is decoupled and asynchronous using an Event Bus (we support RabbitMQ or Azure Service Bus).

In current implementation use of gRPC is limited to the communication between aggregators and micro services. We have following synchronous communications between services in eShop:

1. External clients (i. e. Xamarin App or Browser) to Api Gateways (BFFs): Use HTTP/REST
2. From BFFs to Aggregators: Use HTTP/REST
    * This is basically a request forward. Based on route request is forwarded from the BFF to the aggregator. This is performed for "logically complex" requests, when a single client call involves various microservices that are coordinated from the aggregator.
3. From BFFs to microservices: Use HTTP/REST
    * This is basically a request forward. Based on route request is forwarded from the BFF to the internal microservice. This is performed for simple CRUD requests.
4. From Aggregators to microservices: Use gRPC

Currently we are not transcoding from gRPC to HTTP/REST. This would allow use gRPC from the BFFs to both aggregators and microservices while keeping a HTTP/REST interfaceto the clients. This gRPC<->HTTP/REST translation could be done at BFF level.

Following microservices expose gRPC endpoints:

* Ordering API
* Catalog API
* Basket API

And following BFFs are gRPC clients:

* Mobile Shopping
* Web Shopping