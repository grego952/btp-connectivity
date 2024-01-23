<!-- loio6588a65269bd45a297ebcd6a3baef157 -->

# Managed Namespaces Mode

Manage namespaces for the transparent proxy for Kubernetes.

The transparent proxy can operate in all namespaces in the cluster, or only in namespaces labeled in the following way: *transparent-proxy.connectivity.api.sap/namespace:<namespace where Transparent Proxy is installed\>*.

For this feature, you can set the Helm property `config.managedNamespacesMode` to `all` or `labelSelector`.

The default value is `all`. This means that the proxy operates with destination custom resources across all namespaces in the cluster.

For more information, see [Configuration Guide](configuration-guide-2a22cd7.md).

