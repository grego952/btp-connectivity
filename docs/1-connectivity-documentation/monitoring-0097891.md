<!-- loio0097891bffc54edeabe0b0dc1df71e0a -->

# Monitoring

Check operability, scenarios and metrics of the connectivity proxy for Kubernetes.



<a name="loio0097891bffc54edeabe0b0dc1df71e0a__section_ovn_rmm_1qb"/>

## Basic Availability Monitoring

The basic availability check is the minimal verification you can do to make sure the connectivity proxy is alive. This check only shows if the process of the connectivity proxy is running and if it is able to handle requests. This check is also what is configured as the *liveness probe* for the Kubernetes deployment resource.

You can perform this check on-demand by invoking a simple HTTP GET request to the healthcheck endpoint of the connectivity proxy. If the response is ***200 OK***, the check was *successful*. Any other response means the check *failed*. There are two ways to perform this:

-   From **within the cluster**: Call `connectivity-proxy-tunnel:8042/healthcheck` and observe the result
-   From **outside the cluster**: Call `https://healthcheck.<ingress host of the connectivity proxy>/healthcheck` and observe the result. See [External Health Checking](external-health-checking-5c75674.md) for more details.



<a name="loio0097891bffc54edeabe0b0dc1df71e0a__section_az4_rmm_1qb"/>

## Scenario Monitoring

On top of the availability monitoring of the component itself, it is useful to also monitor entire scenarios. This, however, cannot be provided out of the box by the connectivity proxy as it is specific to the way you use the component. Some options you can explore for this are:

-   Monitor the failure rate of requests to the connectivity proxy.
-   Monitor the amount of error logs in the connectivity proxy.
-   Set up a scheduled execution of a full scenario that performs end-to-end verification, including the operations done via the connectivity proxy.



<a name="loio0097891bffc54edeabe0b0dc1df71e0a__section_f1p_rmm_1qb"/>

## Metrics

Currently, the connectivity proxy does not provide any dedicated support for metrics monitoring via [full metrics pipelines](https://kubernetes.io/docs/tasks/debug-application-cluster/resource-usage-monitoring/#full-metrics-pipeline).

However, you may want to use the [resource metrics pipeline](https://kubernetes.io/docs/tasks/debug-application-cluster/resource-usage-monitoring/#resource-metrics-pipeline) to collect basic metrics and observe them, or configure alerts based on those metrics.

