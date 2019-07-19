## Next major release

Features that will be included in next major release.

- Migrate solution from ASP.NET Core 2.2 to 3.0 and update all projects to use the latest .NET Core 3.0 templates.

- Implement the new .NET Core 3.0 WorkerService in Ordering.API and other background processes.

- Improve Ordering.API
  - Group order items
  - apply discounts from Marketing.API

- Handle two deployment scenarios
  - Basic deployment, better for learning:
    - Docker compose
    - Local Kubernetes
    - Visual Studio F5 experience

  - Advanced deployment, complex but more real-life:
    - Sidecar implementation with Envoy/Istio
    - Improved API Gateway and resilience
    - gRPC for inter-service communications
    - Azure Dev Spaces

## Feature candidates

Check the [backlog](Backlog) for candidate features.
