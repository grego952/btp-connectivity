<!-- loioc5257cf110bf4b7b9054eab74ededff4 -->

# Using the Transparent Proxy

Use the transparent proxy for Kubernetes in different SAP BTP communication scenarios.

The transparent proxy lightens the way your Kubernetes workloads use SAP BTP destinations of type *Internet* and *on-premise*. It provides authentication, principal propagation, SOCKS5 handshake, and easy access to the destination target systems by exposing them as [Kubernetes services](https://kubernetes.io/docs/concepts/services-networking/service/).

To target a given destination for handling by the transparent proxy, you should create a custom Kubernetes resource of type `destinations.destination.connectivity.api.sap` that references the given destination. If you do not create a custom Kubernetes resource of type `destinations.destination.connectivity.api.sap` for a given destination, the destination will not be handled by the transparent proxy.

> ### Note:  
> There should be no Kubernetes service in the namespace where the transparent proxy is installed with a `name` equal to the `name` of the destination custom resource of type `destination.connectivity.api.sap`, because the transparent proxy handles the creation of Kubernetes services based on the information stored in these custom resources.

**Related Information**  


[Internet Connectivity](internet-connectivity-d5ba479.md "Use the transparent proxy for Kubernetes to set up connections of type Internet.")

[On-Premise Connectivity](on-premise-connectivity-41cd3b9.md "Use the transparent proxy for Kubernetes to set up connections of type on-premise.")

[HTTP Authentication](http-authentication-5883721.md "HTTP authentication for the transparent proxy for Kubernetes.")

[Managed Namespaces Mode](managed-namespaces-mode-6588a65.md "Manage namespaces for the transparent proxy for Kubernetes.")

[Communication between Internal Components](communication-between-internal-components-80455ca.md "Configure secure internal communication between transparent proxy components.")

