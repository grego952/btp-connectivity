<!-- loiofce292aeb9e24b7abd47c0b38f6fe8a9 -->

# Troubleshooting

Find troubleshooting information for the transparent proxy for Kubernetes.



<a name="loiofce292aeb9e24b7abd47c0b38f6fe8a9__section_ydc_nfn_t5b"/>

## Get Logs of the Transparent Proxy Components

The transparent proxy consists of a transparent proxy manager, transparent HTTP proxy, and multiple transparent TCP proxy instances.

1.  To get the logs of the transparent proxy manager, execute:

    ```
    kubectl logs -l transparent-proxy.connectivity.api.sap/component=manager --tail=-1 -n <installation-namespace> > transparent-proxy-manager.log
    ```

2.  To get the logs of the transparent HTTP proxy, execute:

    ```
    kubectl logs -l transparent-proxy.connectivity.api.sap/component=http --all-containers --tail=-1 -n <installation-namespace> > transparent-http-proxy.log
    ```

3.  To get the logs of the transparent TCP proxy instances, execute:

    ```
    kubectl logs -l transparent-proxy.connectivity.api.sap/component=tcp --tail=-1 -n <installation-namespace> > transparent-tcp-proxy.log
    ```

4.  To get the logs of the transparent proxy health check, execute:

    ```
    kubectl logs -l transparent-proxy.connectivity.api.sap/component=healthcheck --tail=-1 -n <installation-namespace> > transparent-proxy-health-check.log
    ```


Files created by the above commands:

-   `transparent-proxy-manager.log`
-   `transparent-http-proxy.log`
-   `transparent-tcp-proxy.log`
-   `transparent-proxy-health-check.log`

can be used for investigation purposes. For more information, see [Recommended Actions](recommended-actions-20b1a62.md).



<a name="loiofce292aeb9e24b7abd47c0b38f6fe8a9__section_ng1_4fn_t5b"/>

## Get Status of *destinations.destination.connectivity.api.sap* Custom Resources

```
kubectl describe destinations -n <installation-namespace>
```



<a name="loiofce292aeb9e24b7abd47c0b38f6fe8a9__section_rjt_4sf_vwb"/>

## Change Log Levels of the Transparent Proxy Components

When the default logging level is not sufficient for debugging the issue you are facing, you can change the log level to get more insight about the problem.

Changing a log level is done without any downtime and requires no restarts. All you need to do is invoke a simple command on the pod of a transparent proxy component where you need to gain more insight. Here are some examples:

1.  To change the log level of the transparent proxy manager, execute:

    ```
    kubectl exec <transparent proxy manager pod> -n <installation-namespace> -it -- /etc/logging/change-log-level DEBUG
    ```

2.  To change the log level of the transparent HTTP proxy, execute:

    ```
    kubectl exec <transparent http proxy pod> -n <installation-namespace> -it -- /etc/logging/change-log-level DEBUG
    ```

3.  To change the log level of a transparent TCP proxy instance, execute:

    ```
    kubectl exec <transparent tcp proxy instance pod> -n <installation-namespace> -it -- /etc/logging/change-log-level DEBUG
    ```

4.  To change the log level of the transparent proxy health check, execute:

    ```
    kubectl exec <transparent proxy health check pod> -n <installation-namespace> -it -- /etc/logging/change-log-level DEBUG
    ```


Accepted log levels are: `trace`, `debug`, `info`, `warn`, `error`, `fatal`. The default log level across all transparent proxy components is info.



<a name="loiofce292aeb9e24b7abd47c0b38f6fe8a9__section_fnw_4bt_v5b"/>

## Basic CPU and Memory Monitoring

When using `kubectl`, you can monitor CPU and memory of the transparent proxy's pods out of the box:

```
kubectl top pods -n <installation-namespace> -l 'transparent-proxy.connectivity.api.sap/component in (http,manager,tcp)'
```

For more information on using `kubectl`, see [Interacting with running Pods](https://kubernetes.io/docs/reference/kubectl/cheatsheet/#interacting-with-running-pods).



<a name="loiofce292aeb9e24b7abd47c0b38f6fe8a9__section_j2x_qfn_t5b"/>

## Common Issues and Solutions


<table>
<tr>
<th valign="top">

Issue

</th>
<th valign="top">

Solution

</th>
</tr>
<tr>
<td valign="top">

The call to the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) referencing your destination returns 404.

</td>
<td valign="top">

Make sure the URL configured in the destination is valid. Wait for the next transparent proxy manager completion.

</td>
</tr>
<tr>
<td valign="top">

The call to the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) referencing your destination returns 400.

Check also 'x-error-message', 'x-error-origin' and *'x-internal-error-code'* response headers for more concrete information.

</td>
<td valign="top">

Check your request headers or OAuth configuration fields in the referenced destination. Example for Authorization header of scheme *"Authorization: Bearer <base64-encoded-token\>"*.

</td>
</tr>
<tr>
<td valign="top">

The call to the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) referencing your destination returns response with status code 400 and has response header 'x-error-message' with value ''x-token-service-tenant‘ request header is missing. It is required when 'tokenServiceURLType' property in the destination is of type Common.'.

</td>
<td valign="top">

Make sure you add a valid 'x-token-service-tenant' request header to each destination that has 'tokenServiceURLType' property of type Common.

</td>
</tr>
<tr>
<td valign="top">

The call to the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) referencing your destination returns response with status code 400 and has response header 'x-error-message' with value 'Cannot mix header ‘x-client-assertion-destination-name‘ with headers ‘x-client-assertion‘ and ‘x-client-assertion-type‘.'.

</td>
<td valign="top">

Make sure you pass either ‘x-client-assertion-destination-name‘ or ‘x-client-assertion‘ and ‘x-client-assertion-type‘ request headers and not the combination of all of them.

</td>
</tr>
<tr>
<td valign="top">

The call to the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) referencing your destination returns response with status code 400 and has response header 'x-error-message' with value 'Destination service returned unsuccessful status code. Check your related request headers.' and 'Destination service' value in the 'x-error-origin' header.

</td>
<td valign="top">

Make sure you pass a valid 'authorization' header value that is appropriate for the referenced destination authentication type.

</td>
</tr>
<tr>
<td valign="top">

The call to the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) referencing your destination returns the error code 400 with message "In multi-tenant operational mode, either X-Tenant-Id or X-Tenant-Subdomain header is mandatory to be provided.".

</td>
<td valign="top">

Make sure you pass either the `X-Tenant-Id` or the `X-Tenant-Subdomain` header in shared mode.

</td>
</tr>
<tr>
<td valign="top">

The call to the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) referencing your destination returns the error code 400 with message "Both X-Tenant-Id and X-Tenant-Subdomain headers are passed. Either X-Tenant-Id or X-Tenant-Subdomain is accepted at a time.".

</td>
<td valign="top">

Make sure you pass either the `X-Tenant-Id` or the `X-Tenant-Subdomain` header but not both at the same time in shared mode.

</td>
</tr>
<tr>
<td valign="top">

The call to the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) referencing your destination returns response with status code 400 and has response header 'x-error-message' with value ''x-destination-name' header is missing but required for an endpoint exposing multiple destinations via the same Destination CR.'.

</td>
<td valign="top">

In case the spec.destinationRef.name property is "\*" the 'x-destination-name' header is mandatory provide reference to a valid destination.

</td>
</tr>
<tr>
<td valign="top">

The call to the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) referencing your destination returns response with status code 400 and has response header 'x-error-message' with value 'The value of the header 'x-destination-name' exceeds the maximum allowed length of 200'.

</td>
<td valign="top">

The provided header value is wrong since the Destination service allows a maximum length for a destination name of 200 symbols.

</td>
</tr>
<tr>
<td valign="top">

The call to the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) referencing your destination returns response with status code 400 and has response header 'x-error-message' with value 'The value of the header 'x-destination-name' contains characters that are not allowed. Check the destination name restrictions in the Destination service documentation.'.

</td>
<td valign="top">

The provided header value for 'x-destination-name' has invalid characters.

</td>
</tr>
<tr>
<td valign="top">

The call to the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) referencing your destination returns response with status code 400 and has response header 'x-error-message' with value 'The requested endpoint is bound to a concrete destination via the respective Destination CR. 'x-destination-name' header is not supported for this endpoint. Contact the Transparent Proxy Administrator.'.

</td>
<td valign="top">

The Destination Custom Resource is bound to a specific destination via spec.destinationRef.name property. Either change the spec.destinationRef.name property in the CR to "\*" or do not pass the 'x-destination-name' header.

</td>
</tr>
<tr>
<td valign="top">

The call to the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) referencing your destination returns 500 and *Transparent proxy internal error. Contact the transparent proxy administrator.*.

</td>
<td valign="top">

See [Recommended Actions](recommended-actions-20b1a62.md).

</td>
</tr>
<tr>
<td valign="top">

The call to the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) referencing your destination returns 500 and *Invalid destination configuration. Contact the destination administrator.*

</td>
<td valign="top">

There could be an issue with the fields in

```
config.integration.destinationService.serviceCredentials.secretData
```

or with the configuration fields of the destination. Contact the destination administrator.

</td>
</tr>
<tr>
<td valign="top">

The call to the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) referencing your destination returns response with status code 502 and has response header 'x-error-message' with value 'Destination '<name\>' referred in Destination CR '<name\>' is not found in tenant '<tenant-subdomain\>'. Inspect the Destination CR or contact the Destination Administrator.' and 'Destination service' value in the 'x-error-origin' header.

</td>
<td valign="top">

Check if your referenced destination exists in the specified Destination service instance or contact the destination administrator.

</td>
</tr>
<tr>
<td valign="top">

The call to the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) referencing your destination returns response with status code 502 and has response header 'x-error-message' with value 'Invalid destination configuration. Contact the destination administrator.' and 'Destination service' value in the 'x-error-origin' header.

</td>
<td valign="top">

There could be an issue with the configuration fields of the Destination. Contact the destination Administrator.

</td>
</tr>
<tr>
<td valign="top">

The call to the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) referencing your destination returns response with status code 502 and has response header 'x-error-message' with value 'Invalid OAuth configuration in destination '<name\>' referred in Destination CR '<name\>'. Contact the Destination Administrator.' and 'Destination service' value in the 'x-error-origin' header.

</td>
<td valign="top">

Check Auth Configuration fields or your request headers in the referenced Destination.

</td>
</tr>
<tr>
<td valign="top">

The call to the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) referencing your destination returns response with status code 502 and has response header 'x-error-message' with value 'On-Premise technical connectivity is not configured. There is no value provided for connectivity proxy service name.' and 'Transparent Proxy' value in the 'x-error-origin' header.

</td>
<td valign="top">

Make sure you provide correct Connectivity proxy serviceName in Helm Configurations.

</td>
</tr>
<tr>
<td valign="top">

The call to the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) referencing your destination returns response with status code 502, and has response header 'x-error-message' with value 'The Destination service instance name in the Destination CR '%s' is not configured as expected.' and 'Transparent Proxy' value in the 'x-error-origin' header.

</td>
<td valign="top">

Check if you pass a valid Destination service instance in Destination CR or contact the Kubernetes cluster administrator to check the Helm configuration.

</td>
</tr>
<tr>
<td valign="top">

The call to the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) referencing your destination returns response with status code 500, response header 'x-error-message' with value "Tenant subdomain '<tenantSubdomain\>' could not be determined as valid tenant for Destination service instance with name '<destinationServiceInstanceName\>' as provided in the Transparent Proxy deployment configuration. Contact the Tenant administrator." response header '*x-error-origin*' with value "XSUAA", response header *'x-internal-error-code' with value "404".*

</td>
<td valign="top">

The passed tenant in x-tenant-subdomain is not found. Make sure you pass existing tenant in x-tenant-subdomain.

</td>
</tr>
<tr>
<td valign="top">

The call to the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) referencing your destination returns response with status code 500, response header 'x-error-message' with value "Tenant id '<tenantSubdomain\>' could not be determined as valid tenant for Destination service instance with name '<destinationServiceInstanceName\>' as provided in the Transparent Proxy deployment configuration. Contact the Tenant administrator." response header '*x-error-origin*' with value "XSUAA", response header *'x-internal-error-code' with value "404".*

</td>
<td valign="top">

The passed tenant in x-tenant-id is not found. Make sure you pass existing tenant in x-tenant-id.

</td>
</tr>
<tr>
<td valign="top">

The call to the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) referencing your destination returns response with status code 500, response header 'x-error-message' with value "Tenant subdomain '<tenantSubdomain\>' is not subscribed to respective provider application using Destination service instance with name '<destinationServiceInstanceName\>', as provided in the Transparent Proxy deployment configuration, under provider tenant subdomain '<providerTenantSubdomain\>'. Contact the Destination Administrator." response header '*x-error-origin*' with value "XSUAA", response header *'x-internal-error-code' with value "401".*

</td>
<td valign="top">

The passed tenant in x-tenant-subdomain is not subscribed to the provider. Make sure you pass subscribed to the provider tenant in x-tenant-subdomain.

</td>
</tr>
<tr>
<td valign="top">

The call to the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) referencing your destination returns response with status code 500, response header 'x-error-message' with value "Tenant id '<tenantId\>' is not subscribed to respective provider application using Destination service instance with name '<destinationServiceInstanceName\>', as provided in the Transparent Proxy deployment configuration, under provider tenant subdomain '<providerTenantSubdomain\>'. Contact the Destination Administrator." response header '*x-error-origin*' with value "XSUAA", response header *'x-internal-error-code' with value "401".*

</td>
<td valign="top">

The passed tenant in x-tenant-id is not subscribed to the provider. Make sure you pass subscribed to the provider tenant in x-tenant-id.

</td>
</tr>
<tr>
<td valign="top">

The call to the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) referencing your destination returns response with status code 502, response header 'x-error-message' with value "Destination '<destinationName\>' referred in Destination CR '<crName'\> is not found in tenant '<tenantName\>'. Inspect the Destination CR or contact the Destination Administrator." response header '*x-error-origin*' with value "Destination Service", response header *'x-internal-error-code' with value "404".*

</td>
<td valign="top">

The referenced destination is not found in the Destination service for the given tenant.

</td>
</tr>
<tr>
<td valign="top">

The call to the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) referencing your destination returns response with status code 502, response header 'x-error-message' with value "Destination '%s' not found in tenant '%s'. Contact the Destination Administrator." response header '*x-error-origin*' with value "Destination Service", response header *'x-internal-error-code' with value "404".*

</td>
<td valign="top">

The referenced destination is not found in the Destination service for the given tenant.

</td>
</tr>
<tr>
<td valign="top">

The `destinations.destination.connectivity.api.sap` custom resource referencing your destination with name "testdest" has the name "testservice". The call to the "testservice" [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) returns an unsuccessful status code or the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) does not exist. The last condition of type `Available` of the `destinations.destination.connectivity.api.sap` custom resource has status `False` with the reason *ConfigurationError-ReferencedDestination-NotFound*.

</td>
<td valign="top">

Create a destination with name "testdest". Wait for the next transparent proxy manager completion.



</td>
</tr>
<tr>
<td valign="top">

The `destinations.destination.connectivity.api.sap` custom resource referencing your destination with name "testdest" has the name "testservice". The call to the "testservice" [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) returns an unsuccessful status code or the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) does not exist. The last condition of type `Available` of the `destinations.destination.connectivity.api.sap` custom resource has status `False` with the reason *ConfigurationError-ReferencedDestination-TypeNotSupported*.

</td>
<td valign="top">

For the destination with name "testdest", update the *Type* field with supported values: `HTTP` or `TCP`. Wait for the next transparent proxy manager completion.

</td>
</tr>
<tr>
<td valign="top">

The `destinations.destination.connectivity.api.sap` custom resource referencing your destination with name "testdest" has the name "testservice". The call to the "testservice" [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) returns an unsuccessful status code or the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) does not exist. The last condition of type `Available` of the `destinations.destination.connectivity.api.sap` custom resource has status `False` with the reason *ConfigurationError-ReferencedDestination-ProxyTypeNotSupported*.

</td>
<td valign="top">

For the destination with name "testdest", update the *ProxyType* field with supported values: `OnPremise` or `Internet`. Wait for the next transparent proxy manager completion.

</td>
</tr>
<tr>
<td valign="top">

The `destinations.destination.connectivity.api.sap` custom resource referencing your destination with name "testdest" has the name "testservice". The call to the "testservice" [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) returns an unsuccessful status code or the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) does not exist. The last condition of type `Available` of the `destinations.destination.connectivity.api.sap` custom resource has status `False` with the reason *ConfigurationError-ReferencedDestination-UrlNotSupported*.

</td>
<td valign="top">

For the destination with name "testdest", update the *URL* field with supported values:

-   The field must not be empty.
-   If `Type` is `TCP` and `ProxyType` is `OnPremise`, the URL must start with `tcp://`.
-   If `Type` is `HTTP`, the URL must start with `http://` or `https://`.

Wait for the next transparent proxy manager completion.

</td>
</tr>
<tr>
<td valign="top">

The `destinations.destination.connectivity.api.sap` custom resource referencing your destination with the name "testdest" has the name "testservice". The call to the "testservice" [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) returns an unsuccessful status code or the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) does not exist. The last condition of type "Available" of the `destinations.destination.connectivity.api.sap` custom resource has the status "False" with the reason *ConfigurationError-ReferencedDestination-LoopbackUrlNotSupported*.

</td>
<td valign="top">

For the destination with the name "testdest", update the *URL* field with supported values:

Should not be empty, and should not be a loopback URL \(loopback URLs are those, which contain exactly one of the following hosts: "localhost", "127.0.0.1", "::1", "0:0:0:0:0:0:0:1"\).

Wait for the next transparent proxy manager completion.

</td>
</tr>
<tr>
<td valign="top">

The `destinations.destination.connectivity.api.sap` custom resource referencing your destination with the name "testdest" has the name "testservice". The call to the "testservice" [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) returns an unsuccessful status code or the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) does not exist. The last condition of type "Available" of the `destinations.destination.connectivity.api.sap` custom resource has the status "False" with the reason *ConfigurationError-ReferencedDestination-KeyStoreInvalid*.

</td>
<td valign="top">

For the destination with the name "testdest", update the *KeyStoreLocation* field with supported values. Supported cert store types are `p12`, `pfx`, `pem`, `der`, `cer`, `crt`.

</td>
</tr>
<tr>
<td valign="top">

The `destinations.destination.connectivity.api.sap` custom resource referencing your destination with the name "testdest" has the name "testservice". The call to the "testservice" [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) returns an unsuccessful status code or the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) does not exist. The last condition of type "Available" of the `destinations.destination.connectivity.api.sap` custom resource has the status "False" with the reason *ConfigurationError-ReferencedDestination-TrustStoreInvalid*.

</td>
<td valign="top">

For the destination with the name "testdest", update the *TrustStoreLocation* field with supported values. Supported cert store types are `p12`, `pfx`, `pem`, `der`, `cer`, `crt`.

</td>
</tr>
<tr>
<td valign="top">

The `destinations.destination.connectivity.api.sap` custom resource referencing your destination with the name "testdest" has the name "testservice". The call to the "testservice" [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) returns an unsuccessful status code or the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) does not exist. The last condition of type "Available" of the `destinations.destination.connectivity.api.sap` custom resource has the status "False" with the reason *ConfigurationError-ReferencedDestination-HttpUrlWithTrustStoreOrKeyStoreNotSupported*.

</td>
<td valign="top">

Update the destination with the name "testdest" so that it does not have a URL that starts with "http://" and has `TrustStoreLocation` or `KeyStoreLocation` in the same time.

</td>
</tr>
<tr>
<td valign="top">

The `destinations.destination.connectivity.api.sap` custom resource referencing your destination with name "testdest" has the name "testservice". The call to the "testservice" [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) returns an unsuccessful status code or the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) does not exist. The last condition of type `Available` of the `destinations.destination.connectivity.api.sap` custom resource has status `False` with the reason *ConfigurationFailed*.

</td>
<td valign="top">

Wait for the next transparent proxy manager completion. If the issue remains, see [Recommended Actions](recommended-actions-20b1a62.md).

</td>
</tr>
<tr>
<td valign="top">

The `destinations.destination.connectivity.api.sap` custom resource referencing your destination with name "testdest" has the name "testservice". The call to the "testservice" [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) returns an unsuccessful status code or the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) does not exist. The last condition of type `Available` of the `destinations.destination.connectivity.api.sap` custom resource has status `False` with the reason *ServiceCreationFailed*.

</td>
<td valign="top">

Wait for the next transparent proxy manager completion. If the issue remains, see [Recommended Actions](recommended-actions-20b1a62.md).

</td>
</tr>
<tr>
<td valign="top">

The call to the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) referencing your destination returns an unsuccessful status code or the [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) does not exist.

</td>
<td valign="top">

Wait for the next transparent proxy manager completion. If the issue remains, see [Recommended Actions](recommended-actions-20b1a62.md).

</td>
</tr>
<tr>
<td valign="top">

The last condition of type "Available" of the `destinations.destination.connectivity.api.sap` custom resource has the status "False" with the reason *ConfigurationError-DuplicateDestinationCustomResource*. There is a `destinations.destination.connectivity.api.sap` custom resource with the same name in another namespace.

</td>
<td valign="top">

Change the name of your `destinations.destination.connectivity.api.sap` custom resource or remove the other one if you have control of it.

</td>
</tr>
<tr>
<td valign="top">

The last condition of type "Available" of the *destinations.destination.connectivity.api.sap* custom resource has the status "False" with the reason "ConfigurationError-ProxyTenantModeMismatch" and message "Technical connectivity is not configured. Connectivity Proxy tenant mode \\"dedicated\\" is not compatible with Transparent Proxy tenant mode \\"shared\\"".

</td>
<td valign="top">

The Connectivity proxy should be configured with the same tenant mode as the Transparent proxy.

</td>
</tr>
<tr>
<td valign="top">

The last condition of type "Available" of the *destinations.destination.connectivity.api.sap* custom resource has the status "False" with the reason "ConfigurationError-ProxyTenantModeMismatch" and message "Technical connectivity is not configured. Connectivity Proxy tenant mode \\"shared\\" is not compatible with Transparent Proxy tenant mode \\"dedicated\\"".

</td>
<td valign="top">

The Connectivity proxy should be configured with the same tenant mode as the Transparent proxy.

</td>
</tr>
<tr>
<td valign="top">

The last condition of type "Available" of the *destinations.destination.connectivity.api.sap* custom resource has the status "False" with the reason "ConfigurationError-MultitenancyAnnotation-Invalid" and message "Technical connectivity is not configured. \\"transparent-proxy.connectivity.api.sap/tenant-subdomains\\" annotation is invalid".

</td>
<td valign="top">

Use a proper json array formatting when specifying the TCP tenants in your "transparent-proxy.connectivity.api.sap/tenant-subdomains" annotation.

</td>
</tr>
<tr>
<td valign="top">

The last condition of type "Available" of the *destinations.destination.connectivity.api.sap* custom resource has the status "False" with the reason "FailedToApplyConfiguration" and message "Configuration failed for tenants: \[\\"Tenant1\\", \\"Tenant2\\"...\]" where Tenant1, Tenant2, etc. are tenant subdomains specified in the "transparent-proxy.connectivity.api.sap/tenant-subdomains" annotation.

</td>
<td valign="top">

Check the transparent proxy manager for error logs. The tenants Tenant1, Tenant2 could not be onboarded because either the specified destination is not found in the destination service for the given tenants, is not valid in the destinations service or creating k8s components for the given destination/tenant failed.

</td>
</tr>
<tr>
<td valign="top">

Applying helm configuration fails with "When .Values.config.security.communication.internal.encryptionEnabled is true, .Values.config.security.communication.internal.certManager.issuerRef.name cannot be empty".

</td>
<td valign="top">

Set value to `.Values.config.security.communication.internal.certManager.issuerRef.name` when `.Values.config.security.communication.internal.encryptionEnabled` is true.

</td>
</tr>
<tr>
<td valign="top">

Applying helm configuration fails with ".Values.config.security.communication.internal.certManager.issuerRef.namespace and .Values.config.security.communication.internal.certManager.issuerRef.kind are both passed. Use .Values.config.security.communication.internal.certManager.issuerRef.kind when your issuer is of type cert-manager.io and .Values.config.security.communication.internal.certManager.issuerRef.namespace when your issuer is of type cert.gardener.cloud".

</td>
<td valign="top">

Pass either `.Values.config.security.communication.internal.certManager.issuerRef.kind` or `.Values.config.security.communication.internal.certManager.issuerRef.namespace`, not both, when `.Values.config.security.communication.internal.encryptionEnabled is true`.

</td>
</tr>
<tr>
<td valign="top">

Applying helm configuration fails with "Neither .Values.config.security.communication.internal.certManager.issuerRef.namespace or .Values.config.security.communication.internal.certManager.issuerRef.kind is passed. Use .Values.config.security.communication.internal.certManager.issuerRef.kind when your issuer is of type cert-manager.io and .Values.config.security.communication.internal.certManager.issuerRef.namespace when your issuer is of type cert.gardener.cloud".

</td>
<td valign="top">

One of `.Values.config.security.communication.internal.certManager.issuerRef.kind` and `.Values.config.security.communication.internal.certManager.issuerRef.namespace` is required when `.Values.config.security.communication.internal.encryptionEnabled` is true.

</td>
</tr>
<tr>
<td valign="top">

Applying helm configuration fails with "Issuer of version cert.gardener.cloud/v1alpha1 with name 'test' in namespace 'test' not found".

</td>
<td valign="top">

Make sure that *Issuer* of version *cert.gardener.cloud/v1alpha1* with name 'test' in namespace 'test' exists.

</td>
</tr>
<tr>
<td valign="top">

Applying helm configuration fails with "Issuer of version cert-manager.io/v1 with name 'test' in namespace 'test' not found".

</td>
<td valign="top">

Make sure that *Issuer* of version *cert-manager.io/v1* with name 'test' in namespace 'test' exists.

</td>
</tr>
<tr>
<td valign="top">

Applying helm configuration fails with "ClusterIssuer of version cert-manager.io/v1 with name 'test' not found".

</td>
<td valign="top">

Make sure that *ClusterIssuer* of version *cert-manager.io/v1* with name 'test' exists.

</td>
</tr>
<tr>
<td valign="top">

Applying helm configration fails with "Istio not installed on the cluster. Revise your Istio integration configuration."

</td>
<td valign="top">

The configuration for integration in Istio service mesh is provided, but Istio is not installed on the cluster. Either install Istio on the cluster or remove the configuration for integration in Istio service mesh.

</td>
</tr>
<tr>
<td valign="top">

Applying helm configuration fails with "An error occurred because certain necessary configuration settings are missing. Ensure that either 'config.security.communication.internal.encryptionEnabled' or 'config.integration.serviceMesh.istio.istio-integration' is provided.".

</td>
<td valign="top">

Integration either with *Istio* or *cert-manager* is mandatory.

This is done by configuring at least one of the two properties: `config.integration.serviceMesh.istio.istio-integration` or `config.security.communication.internal.encryptionEnabled`.

-   `config.integration.serviceMesh.istio.istio-integration` makes `config.security.communication.internal.encryptionEnabled` optional.
-   If "encryptionEnabled" is set to true and `config.integration.serviceMesh.istio.istio-integration` is missing , you must provide `config.security.communication.internalCommunication.certManager.issuerRef.name` and `config.security.communication.internalCommunication.certManager.issuerRef.kind`.



</td>
</tr>
<tr>
<td valign="top">

The *destinations.destination.connectivity.api.sap* custom resource referencing your destination with the name "testdest" has the name "testservice". The last condition of type "Available" of the *destinations.destination.connectivity.api.sap* custom resource has the status "False" with the reason "ConfigurationError-K8sResourceWithNameAlreadyPresent".

</td>
<td valign="top">

There is a Kubernetes resource with the name of the Destination custom resource present in the same namespace. Rename one of the resources to remove the collision.

</td>
</tr>
</table>

