
> **CONTENT**
- [Causes](#causes)
  - [Details](#details)
- [Solutions](#solutions)

## Causes

This error occurs because the connecting app isn't registered in the IdentityServer database as an authorized client.

The authorized client registration occurs when the Identity DB is seeded, and in eShopOnContainers this happens when the DB is first created. So this only happens when first installed or when restarting the Identity service if the DB has been deleted.

When registering the clients, eShopOnContainers reads the values from the following configuration variables, from either the `appsettings.json` file, the `docker-compose.override.yml` file or the equivalent environment variables:

```yaml
- SpaClient
- MvcClient
- LocationApiClient
- MarketingApiClient
- BasketApiClient
- OrderingApiClient
- MobileShoppingAggClient
- WebShoppingAggClient
- WebhooksApiClient
- WebhooksWebClient
```

### Details

IdentityServer uses the `RedirectUri` to decide if the connecting client is authorized

When a user that's not been authorized tries to use the [client] app, they are  redirected to the IdentityServer's `/connect/authorize` endpoint, and the request includes a redirection uri that's used to complete the login process, as shown in the following image:

![](images/unauthorized_client-error-on-Login/identity-server-authorize-request.png)

The authorized clients are registered in the `Clients` table and the related redirect URIs in the `ClientRedirectUris` table as shown in the following image:

![](images/unauthorized_client-error-on-Login/ClientRedirectUris-table.png)

It's important to keep in mind that if the application is registered as `http://host.docker.internal:5004` but started as `http://localhost:5104` it's considered to be a different one, so it'll get the `unauthorized_client` message.

## Solutions

So the possible solution are:

1. Make sure you are starting the app from the correct address.

2. Update the `ClientRedirectUris` table to the correct values.

3. Drop the `IdentityDb` database and restart the `Identity` service, after updating the `docker-compose.override.yml` file, or the `configmap.yaml` in Kubernetes, so that all the clients are registered correctly.
