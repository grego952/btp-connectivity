<!-- loio783d44d73212468fbe414495dc32a721 -->

# Destination Fragments

Extend your destination with a destination fragment.

You can use the “Find Destination” API to extend your destination with a destination fragment.

For more information, see [Extending Destinations with Fragments](extending-destinations-with-fragments-f56600a.md).

> ### Sample Code:  
> ```
> {
>     "FragmentName": "example-fragment",
>     "URL": "https:/myotherapp.com"
> }
> ```

You can reference a fragment as follows.

-   Directly in the destination custom resource:

    > ### Sample Code:  
    > ```
    > apiVersion: destination.connectivity.api.sap/v1
    > kind: Destination 
    > metadata: 
    >   name: example-dest 
    > spec:   
    >   destinationRef:
    >     name: "example-dest-client-cert"
    >   destinationServiceInstanceName: dest-service-instance-example // can be ommited if config.destinationService.defaultInstanceName is provided
    >   fragmentRef:
    >     name: "example-fragment"
    > ```

    > ### Note:  
    > Static reference of a fragment is only applicable for a destination custom resource that references a particular destination. The [Dynamic Lookup of Destinations](dynamic-lookup-of-destinations-6836e00.md) feature is not compatible with this approach.

-   Dynamically passing a fragment as an HTTP header is only compatible with the [Dynamic Lookup of Destinations](dynamic-lookup-of-destinations-6836e00.md) approach. You can check the examples given there.

