<!-- loiof6cb5bc1fac14a899b8457b4bf71bb56 -->

# Connectivity Proxy Integration

Integrate the transparent proxy with the connectivity proxy for Kubernetes.

The connectivity proxy is a Kubernetes component that connects workloads running on a Kubernetes cluster to on-premise systems exposed via the [Cloud Connector](cloud-connector-e6c7616.md). The transparent proxy itself doesn’t provide direct connections to on-premise systems, that is, the connectivity proxy integration is mandatory for the transparent proxy to route to on-premise destinations. To integrate the transparent proxy with the connectivity proxy, you must:

1.  Install a connectivity proxy instance or reuse an existing one. It must be installed in the same Kubernetes cluster where the transparent proxy is installed.

    For more information, see [Lifecycle Management](lifecycle-management-60c0a45.md).

2.  Follow the instructions under [Lifecycle Management](lifecycle-management-1c18e0c.md) and set up the `values.yaml` for integrating with the connectivity proxy, providing the `config.integration.connectivityProxy.*` parameters. For more information, see [Configuration Guide](configuration-guide-2a22cd7.md).

**Related Information**  


[Connectivity Proxy for Kubernetes](connectivity-proxy-for-kubernetes-e661713.md "Use the connectivity proxy for Kubernetes to connect workloads on a Kubernetes cluster to on-premise systems.")

