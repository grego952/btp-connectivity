<!-- loio0edfc0b92547427f8d63ed93bfa5c550 -->

# Connectivity Service

Use the connectivity proxy for Kubernetes with the Connectivity service to connect to on-premise systems.

On-premise systems are exposed via the Cloud Connector. The Cloud Connector is connected to \(registered in\) the SAP Connectivity service and ready to serve. The connectivity proxy is the software component to which, at runtime, the Cloud Connector connects and establishes the business data tunnel.

To use the connectivity proxy, it must be paired with the SAP Connectivity service, that is, configured to connect to the central service to which initially theCloud Connector was connected. This enables the connectivity proxy to dynamically \(on-demand\) serve its purpose, that is, to securely establish business data tunnel connections to the Cloud Connector, hosted in an on-premise network next to the backend systems.



## Prerequisites

You have an account on SAP BTP, Cloud Foundry environment, and your SAP BTP account user has the authorization to create service instances.



<a name="loio0edfc0b92547427f8d63ed93bfa5c550__section_mhb_2r2_1qb"/>

## Procedure

1.  Create a Connectivity service instance with service plan `connectivity_proxy`.
2.  Create a service key of the created service instance.

    > ### Tip:  
    > You can create the service key with x.509 credentials instead of a client secret, but only in the SAP-managed certificate case. If you do so, you must take care to rotate the key before the certificate expires.

3.  Follow the instructions under [Lifecycle Management](lifecycle-management-60c0a45.md) and set up the Kubernetes secret for pairing with the central SAP Connectivity service, providing the content of the created service key.
4.  Check the [Configuration Guide](configuration-guide-eaa8204.md) for `config.integration.connectivityService`\* parameters.

