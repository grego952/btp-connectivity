<!-- loioaebcc82c94ac4325af52a5d6994fe5b5 -->

# Troubleshooting in Kyma

Find solutions for issues with the transparent proxy in Kyma.



<a name="loioaebcc82c94ac4325af52a5d6994fe5b5__section_cg4_fyc_zxb"/>

## Common Issues and Solutions

For custom resources having a *Warning* state, refer to this table to find a solution for specific issues.

Check the [Configuration Guide](configuration-guide-2a22cd7.md) after identifying your misconfiguration in the transparent proxy custom resource conditions.


<table>
<tr>
<th valign="top">

Custom Resource Condition Message

</th>
<th valign="top">

Solution

</th>
</tr>
<tr>
<td valign="top">

An error occurred because certain necessary configuration settings are missing. Make sure either `config.security.communication.internal.encryptionEnabled` or `config.integration.serviceMesh.istio.istio-integration` is provided.

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

Custom resource with name "<name\>" already exists in this namespace.

</td>
<td valign="top">

There could be only 1 transparent proxy custom resource in a single namespace. Delete the unnecessary custom resource or move it to another namespace.

</td>
</tr>
<tr>
<td valign="top">

When `config.security.communication.internal.encryptionEnabled` is true, `config.security.communication.internal.certManager.issuerRef.name` cannot be empty.

</td>
<td valign="top">

If `config.security.communication.internalCommunication.encryptionEnabled` is set to true, then `config.security.communication.internal.certManager.issuerRef.name` cannot be empty.

</td>
</tr>
<tr>
<td valign="top">

`config.security.communication.internal.certManager.issuerRef.namespace` and `config.security.communication.internal.certManager.issuerRef.kind` are both passed.

Use `config.security.communication.internal.certManager.issuerRef.kind` when your issuer is of type `cert-manager.io` and `config.security.communication.internal.certManager.issuerRef.namespace` when your issuer is of type `cert.gardener.cloud`.

</td>
<td valign="top">

If `config.security.communication.internalCommunication.encryptionEnabled` is set to true, you must pass either `config.security.communication.internal.certManager.issuerRef.kind` or `config.security.communication.internal.certManager.issuerRef.namespace`, not both.

</td>
</tr>
<tr>
<td valign="top">

Neither `config.security.communication.internal.certManager.issuerRef.namespace` nor `config.security.communication.internal.certManager.issuerRef.kind` is passed.

Use `config.security.communication.internal.certManager.issuerRef.kind` when your issuer is of type [cert-manager.io](http://cert-manager.io/) and `config.security.communication.internal.certManager.issuerRef.namespace` when your issuer is of type `cert.gardener.cloud`.

</td>
<td valign="top">

If `config.security.communication.internalCommunication.encryptionEnabled` is set to true, you must pass either `config.security.communication.internal.certManager.issuerRef.kind` or `config.security.communication.internal.certManager.issuerRef.namespace`, both cannot be empty.

</td>
</tr>
<tr>
<td valign="top">

"certificates.cert-manager.io" custom resource definition not found.

</td>
<td valign="top">

If `config.security.communication.internalCommunication.encryptionEnabled` is set to true, [cert-manager](https://cert-manager.io/docs/) must be installed in the cluster.

</td>
</tr>
<tr>
<td valign="top">

"certificates.cert.gardener.cloud" custom resource definition not found,

</td>
<td valign="top">

If `config.security.communication.internalCommunication.encryptionEnabled` is set to true and `config.security.communication.internalCommunication.certManager.issuerRef.namespace` is not empty, then [cert-manager-gardener](https://github.com/gardener/cert-management) must be installed in the cluster.

</td>
</tr>
<tr>
<td valign="top">

`config.security.communication.internalCommunication.certManager.issuerRef` properties: \[kind and name\] should be provided.

</td>
<td valign="top">

If `config.security.communication.internalCommunication.encryptionEnabled` is set to true, a valid reference to an existing `Issuer` or `ClusterIssuer` must be provided to secure the internal transparent proxy communication by mTLS.

</td>
</tr>
<tr>
<td valign="top">

Resource with api version *cert-manager.io/v1* and kind "<Issuer|ClusterIssuer\>" with name "<name\>" not found.

</td>
<td valign="top">

The referenced `Issuer` or `ClusterIssuer` is not found in the cluster. If it is of type `Issuer`, check the namespace and name. For `ClusterIssuer`, check the name.

</td>
</tr>
<tr>
<td valign="top">

Resource with api version *cert.gardener.cloud/v1alpha1* and kind "Issuer" in namespace "<namespace\>" with name "<name\>" not found.

</td>
<td valign="top">

The referenced *Issuer* with api version *cert.gardener.cloud/v1alpha1* is not found. Check the specified namespace to see if the resource exists.

</td>
</tr>
<tr>
<td valign="top">

Provide at least one Destination service instance in `config.integration.destinationServiceIntegration.instances`, or create and bind an instance in the `sap-transp-proxy-system` namespace using the *SAP BTP Service Operator*.

</td>
<td valign="top">

The transparent proxy should have at least one Destination service instance configured in `config.integration.destinationServiceIntegration.instances`, or resources of api version "services.cloud.sap.com/v1" and kind "ServiceInstance" should exist in the "sap-transp-proxy-system" namespace.

</td>
</tr>
<tr>
<td valign="top">

Destination service instance name should be provided.

</td>
<td valign="top">

Some of the entries in `config.integration.destinationService.instances` does not have `name` specified.

</td>
</tr>
<tr>
<td valign="top">

`secretName` should be provided for Destination service instance: "<name\>".

</td>
<td valign="top">

The given destination service instance should have valid reference to a secret holding the service credentials for consuming the Destination service.

</td>
</tr>
<tr>
<td valign="top">

`secret` with name "<name\>" not found in namespace: "<namespace\>".

</td>
<td valign="top">

The provided secret cannot be found in the referenced `namespace.Examples`:

-   The referenced secret holding the service credentials for the Destination service is not found for the referenced destination service instance. Check the `secretName` and `secretNamespace` properties provided in the `serviceCredentials` section for the given instance in `config.integration.destinationService.instances`.
-   The referenced secret holding the service credentials for the connectivity proxy is not found. Check the *secretName* and `secretNamespace` properties provided in the `serviceCredentials` section for the given instance in `config.integration.connectivityProxy.serviceCredentials`.



</td>
</tr>
<tr>
<td valign="top">

`secretName` should be provided for connectivity proxy service instance in shared mode.

</td>
<td valign="top">

`config.integration.connectivityProxy.serviceCredentials.secretName` should be provided when `config.integration.connectivityProxy.serviceName` is not blank, and the connectivity proxy referenced by `config.integration.connectivityProxy.serviceName` is in shared mode.

</td>
</tr>
<tr>
<td valign="top">

`configMap` "connectivity-proxy" not found in namespace "<namespace\>".

</td>
<td valign="top">

The given config map is not present in the same namespace as the service defined in `config.integration.connectivityProxy.serviceName`.

If the service name contains a namespace, the config map should be in that namespace otherwise it should be in the same namespace as the transparent proxy custom resource.

</td>
</tr>
<tr>
<td valign="top">

Key "connectivity-proxy-config.yml" not found in `configMap`\`s Data from `configMap`: "connectivity-proxy" in namespace "<namespace\>".

</td>
<td valign="top">

The referenced config map does not contain the expected "connectivity-proxy-config.yml" `Data` key.

</td>
</tr>
<tr>
<td valign="top">

Connectivity proxy tenant mode "<tenant\_mode\>" is not compatible with transparent proxy tenant mode "<tenant\_mode\>".

</td>
<td valign="top">

The tenant mode defined in the connectivity proxy\`s `configmap` is different from the one defined in `config.tenantMode` of the transparent proxy custom resource. The tenant modes of the connectivity proxy and transparent proxy must be **equal** \(shared & shared or dedicated & dedicated\).

</td>
</tr>
<tr>
<td valign="top">

Istio not installed on the cluster. Revise your Istio integration configuration.

</td>
<td valign="top">

The configuration for integration in Istio service mesh is provided, but Istio is not installed on the cluster. Either install Istio on the cluster or remove the configuration for integration in Istio service mesh.

</td>
</tr>
</table>

