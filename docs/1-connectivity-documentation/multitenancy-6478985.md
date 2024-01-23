<!-- loio6478985d12a54d7ab8a4e5abce3972e0 -->

# Multitenancy

Use multitenancy for the transparent proxy for Kubernetes.

The transparent proxy works in two tenant modes: *dedicated* and *shared*. You can change the mode by modifying the Helm property `.config.tenantMode`.

For more information, see [Configuration Guide](configuration-guide-2a22cd7.md).

-   In the *dedicated* tenant mode, the transparent proxy can expose destinations only from the subaccount passed in the service key of the Destinations service. Requests to the transparent proxy remain unchanged.
-   In the *shared* tenant mode, the transparent proxy can expose destinations from any subscribed tenant to the subaccount passed in the service key of the Destinations service.



<a name="loio6478985d12a54d7ab8a4e5abce3972e0__section_f4t_vxx_yzb"/>

## HTTP

When requesting a destination through the transparent proxy in shared tenant mode, you must pass the `X-Tenant-Subdomain: <tenant-subdomain>` or `X-Tenant-Id: <tenant-id>` header.

A tenant is successfully onboarded when it is visible in the destination custom resource status. The onboarding of a tenant is dynamic and happens during the first request on behalf of that tenant.



<a name="loio6478985d12a54d7ab8a4e5abce3972e0__section_lk3_vxx_yzb"/>

## TCP

Tenants are configured in the destination custom resource \(CR\) as annotation with key "transparent-proxy.connectivity.api.sap/tenant-subdomains" and value <all tenant subdomains\> in form of a json array:

```
"transparent-proxy.connectivity.api.sap/tenant-subdomains": '["tenantSubdomain1", "tenantSubdomain2", ...]'
```

For each tenant, a new instance of TCP proxy is created which is assigned only to that specific tenant and destination. Also, a separate service is created with a prefix containing the tenant subdomain \(for example, if we have tenant subdomain "tenant1" and destination CR "dest", the service name will be "tenant1-dest".

Each tenant is successfully onboarded when it is visible in a Destination CR status.

