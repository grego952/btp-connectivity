<!-- loiocd02e5cca9f641e1854107641b41886a -->

# Destination Service Integration

Integrate the transparent proxy for Kubernetes with the SAP BTP Destination service.

The Destination service lets you declaratively model a technical connection as a destination configuration, and via its REST APIs find the destination configuration that is required to access a remote service or system from your Kubernetes workload. To integrate the transparent proxy with the Destination service, you must:

1.  Create a Destination service instance or reuse an existing one.
2.  Create a service key of the service instance.
3.  Follow the instructions under [Lifecycle Management](lifecycle-management-1c18e0c.md) and set up the `values.yaml` for pairing with the Destination service, providing a base64-encoded service key for the Destination service.
4.  Check the [Configuration Guide](configuration-guide-2a22cd7.md) for the `config.integration.destinationService.instances` property.

