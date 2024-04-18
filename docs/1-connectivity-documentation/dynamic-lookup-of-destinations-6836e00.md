<!-- loio6836e007ebb24954b727f1524837f741 -->

# Dynamic Lookup of Destinations

Create a single custom resource to look up one ore more destinations dynamically with the transparent proxy for Kubernetes.

The transparent proxy lets you perform a dynamic lookup of one or multiple destinations from a destination service instance and its tenants. To consume a destination in that way, you only have to create a single custom resource.

**Example: Destination Custom Resource**

```
apiVersion: destination.connectivity.api.sap/v1
kind: Destination
metadata:
  name: dynamic-destination
spec:
  destinationRef:
    name: "*"
  destinationServiceInstanceName: dest-service-instance //not mandatory
```

In the example above, a destination custom resource has `spec.destinationRef.name = "*"`, which indicates that this destination would accept dynamic lookup and only a single Kubernetes service will be created with name `dynamic-destination` which works as an entry point for all destinations from `destinationServiceInstanceName` with `name: dest-service-instance`.

The transparent proxy identifies the destination for which a request should be configured and dispatched by obtaining the destination name \(destination identifier\) from a custom header called `X-Destination-Name`.

> ### Note:  
> This header is specifically intended to identify a destination within a Destination service instance and its tenants.

The destination can also be combined by optionally providing a custom header called `X-Fragment-Name`.

**Example Destination:**

```
{
    "Name": "example-dest-client-cert",
    "Type": "HTTP",
    "ProxyType": "Internet",
    "URL": "https:/myapp.com",
    "Authentication": "ClientCertificateAuthentication",
    "KeyStorePassword": "Abcd1234",
    "KeyStoreLocation": "cert.jks"
}
```

**Example Fragment:**

```
{
    "FragmentName": "example-fragment",
    "URL": "https:/myotherapp.com"
}
```

If you want to call the `example-dest-client-cert` destination through the Kubernetes service named `dynamic-destination`, you can execute the command below:

```
curl dynamic-destination.<transparent-proxy-namespace> -H "X-Destination-Name: example-dest-client-cert"
```

If you want to call `example-dest-client-cert` destination, enriching it with the properties from fragment `example-fragment` through the Kubernetes service named `dynamic-destination`, you can execute the command below:

```
curl dynamic-destination.<transparent-proxy-namespace> -H "X-Destination-Name: example-dest-client-cert" -H "X-Fragment-Name: example-fragment"
```

