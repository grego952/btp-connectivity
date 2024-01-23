<!-- loioa5c54eff16364afd85c1391d7a3a359b -->

# Frequently Asked Questions

Answers to the most common questions about the connectivity proxy for Kubernetes.





### **When using one of the two untrusted operational modes, what is the purpose of the `allowedClientId` property? What token should I provide in the `Proxy-Authorization` header?**

The `Proxy-Authorization` header serves as a way for workloads calling the proxy to authenticate against it. To do this, they need to provide this header with a JSON Web token \(JWT\) as value.

To accept the JWT, it must be issued by the OAuth client, specified via the `allowedClientId`. By configuring the `allowedClientId`, you determine which OAuth client protects the proxy endpoints.

The OAuth client must be XSUAA-based.



### **How is the `Proxy-Authorization` header verified?**

There are several aspects that are being verified:

-   The signature is being verified by calling XSUAA to get the public keys for the tenant, on behalf of which the JWT is issued, and using those keys to check if it is valid.
-   The token validity is also verified and expired tokens are rejected.
-   Also, we allow only tokens issued by a specified client ID \(via the `allowedClientId` configuration\).



### **Why do I need the `connectivity:connectivity_proxy` service key?**

The connectivity proxy is a distributed software component that needs to connect to an instance of the central Connectivity service to function.

This pairing is achieved via a `connectivity:connectivity_proxy service` key, which contains both routing information and credentials for this pairing.



### **Why do I need a public endpoint for the connectivity proxy?**

To preserve the integrity of an on-premise landscape and not expose anything from there to the Internet, the flow for establishing the connection between connectivity proxy and Cloud Connector is initiated by the Cloud Connector.

The public endpoint is used by the Cloud Connector to call the connectivity proxy and enable the data exchange.



### **What is the relation of the connectivity proxy to the Connectivity service in SAP BTP?**

The connectivity proxy is a distributed component that must be paired to an instance of the Connectivity service in SAP BTP in order to function.

Cloud Connectors would still connect to the Connectivity service on SAP BTP and the connectivity proxy will make use of those Cloud Connectors via the established pairing.



### **What is the relation of the connectivity proxy to the Destination service in SAP BTP?**

There is no dependency or tight integration.

You can use the Destination service to store and retrieve on-premise destination configurations which can then be used to construct a request to on-premise systems through the connectivity proxy.



### **Are there any client libraries that I can use with the connectivity proxy?**

Please check [Using the Connectivity Proxy](using-the-connectivity-proxy-f3c1ef4.md).



### **When do I need a subscription to the `connectivity:connectivity_proxy` instance?**

Please check [Connectivity Service](connectivity-service-0edfc0b.md).



### **Can I port a cloud SDK application from the Cloud Foundry environment to Kubernetes and use the connectivity proxy?**

It is a bit clunky, but yes.

If you set up the connectivity proxy in an untrusted operational mode, the way the SDK works is well suited for it.

However, since the SDK is created with the Cloud Foundry environment in mind, you would need to simulate the `VCAP_SERVICES` environment to get it working.



### **Is there an equivalent to the lite plan from the Cloud Foundry environment? Is the lite plan relevant for the connectivity proxy?**

The lite plan is only relevant for the Cloud Foundry environment.

There is no lite plan for the connectivity proxy. Instead, you use an XSUAA-based OAuth client of your choice to protect the connectivity proxy, and use it to issue tokens.

