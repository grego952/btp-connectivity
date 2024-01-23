<!-- loio4fadac5e1b2e4316ba6f70327b1e034c -->

# Installing the Transparent Proxy as Subchart of the Connectivity Proxy

If you install the connectivity proxy with Helm, you can have the transparent proxy installed as a subchart. For more information about Helm subcharts, see the [Helm documentation](https://helm.sh/docs/chart_template_guide/subcharts_and_globals).

1.  The transparent proxy subchart is disabled by default. To enable it, set the `enabled` flag to `true` in the `transparent-proxy` section in the `values.yaml` file.

    > ### Sample Code:  
    > ```
    > transparent-proxy:
    >   enabled: true
    > ```

2.  You can modify the transparent proxy version from the `requirements.yaml` file in the connectivity proxy release.

**Related Information**  


[Transparent Proxy for Kubernetes](transparent-proxy-for-kubernetes-acc64ad.md "Use the transparent proxy for Kubernetes to connect workloads on a Kubernetes cluster to Internet and on-premise applications.")

[Configuration Guide](configuration-guide-eaa8204.md "Find an overview of configuration parameters for the connectivity proxy for Kubernetes.")

