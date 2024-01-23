<!-- loio2f8b0329c4984514950dd559e42aa496 -->

# 2021 Connectivity \(Archive\)





**2021**


<table>
<tr>
<th valign="top">

Technical Component

</th>
<th valign="top">

Capability

</th>
<th valign="top">

Environment

</th>
<th valign="top">

Title

</th>
<th valign="top">

Description

</th>
<th valign="top">

Action

</th>
<th valign="top">

Type

</th>
<th valign="top">

Available as of

</th>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

Connectivity Service - Cloud Connector - SAP Cloud PKI

</td>
<td valign="top">

SAP Cloud PKI \(public key infrastructure\) is enabled for technical communication between Cloud Connector and Connectivity service.

-   The change is transparent for the Cloud Connector - as soon as you renew your subaccount certificate in the Cloud Connector, the newly issued X.509 client certificate will be part of SAP Cloud PKI.
-   If you are using Connectivity proxy software components as part of your solution, make sure you use version 2.4.1 or higher. For scenarios with termination in the ingress, version 2.3.1 of the Connectivity proxy is sufficient.



</td>
<td valign="top">

Info only

</td>
<td valign="top">

New

</td>
<td valign="top">

2021-12-02

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Cloud Foundry

-   Neo



</td>
<td valign="top">

Destination Service - Mail Destinations

</td>
<td valign="top">

You can now configure destinations of type MAIL with any OAuth-based authentication type as available for HTTP destinations, including the option for mTLS via X.509 client certificate.

> ### Restriction:  
> The Mail Java API \(Neo environment\) does not provide the `javax.mail.Session` object out of the box. It must be configured manually.



</td>
<td valign="top">

Info only

</td>
<td valign="top">

New

</td>
<td valign="top">

2021-12-02

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Cloud Foundry

-   Neo



</td>
<td valign="top">

Cloud Connector 2.14.0.1 - Enhancements

</td>
<td valign="top">

Release of Cloud Connector version 2.14.0.1 introduces the following enhancements:

-   Cloud Connector can now use SAPMachine 11 as Java runtime.

    For more information, see [Prerequisites](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/e23f776e4d594fdbaeeb1196d47bbcc0.html#loioe23f776e4d594fdbaeeb1196d47bbcc0__jdk).

-   Cloud Connector supports Windows Server 2022 as additional OS version.

    For more information, see [Prerequisites](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/e23f776e4d594fdbaeeb1196d47bbcc0.html#loioe23f776e4d594fdbaeeb1196d47bbcc0__matrix).

-   Monitoring was extended to show usage information for service channels \(on-premise to cloud scenarios\).

    For more information, see [Monitoring](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/6d9c937dd35344bca3eb61ebf34a5c1d.html).

-   An administrator can now configure more connectivity-related parameters on the *Configuration* \> *Advanced* screen instead of modifying the configuration files on OS level.

    For more information, see [Configure Tunnel Connections](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/3975253c1a884638bf6f408f55ea349e.html).

-   You can define a different location for audit log and trace files.

    For more information, see [Manage Audit Logs](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/2264c7002f844fe4833186a1d168de66.html) and [Troubleshooting](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/e7df7f15bb571014ae24bca245319880.html)

-   Additional configuration REST APIs let you configure the Cloud Connector remotely.

    For more information, see [Configuration REST APIs](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/cfb9d579f50b4711a514dc8f08d22f73.html).

-   The additional role *Subaccount Administrator* lets you define authorizations limited to subaccount-related tasks. Cross-subaccount configuration can only be viewed by users having this role.

    For more information, see [Use LDAP for Authentication](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/120ceecfd84145a181ac160d588a7a3d.html).

-   Access control usage monitor data is now persisted and will survive a restart.
-   The connection check for HTTPS access control entries now reveals information about the causes for a failing check and potential configuration issues if principal propagation with x.509 certificates is used.

Action: We recommend that you always use the latest Cloud Connector version.

For more information, see [Upgrade](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/7a7cc373019b4b6eaab39b5ab7082b09.html).

</td>
<td valign="top">

Recommended

</td>
<td valign="top">

New

</td>
<td valign="top">

2021-12-02

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Cloud Foundry

-   Neo



</td>
<td valign="top">

Cloud Connector 2.14.0.1 - Fixes

</td>
<td valign="top">

Release of Cloud Connector version 2.14.0.1 provides the following bug fixes:

-   Audit log selection was not working correctly if the end of the time interval was before noon.

    This issue has been fixed.

-   If an RFC connection is broken while waiting for data from the ABAP system, the processing engine could get into an inconsistent state, causing wrong processing for succeeding requests sent from the cloud application, which eventually could make the cloud application hang.

    This issue has been fixed.

-   Fixed a race condition that could occur if many requests were sent from the cloud application over the same RFC connection, and if the network from the cloud application to the Cloud Connector was very fast.

    In such a situation, two threads were processing this single RFC connection, causing an inconsistency that could lead to a `NullPointerException` in `RfcBlock.populateRequestStatistics` when trying to access the field *<performanceStatistics\>*.

-   When configuring an RFC SNC acccess control entry, but overall SNC configuration is incomplete, Cloud Connector now reports the configuration error at runtime instead of falling back to plain RFC, if offered by the backend.




</td>
<td valign="top">

Info only

</td>
<td valign="top">

Changed

</td>
<td valign="top">

2021-12-02

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

Destination Service - Features

</td>
<td valign="top">

-   The *Destinations* UI in the cockpit lets you configure an X.509 client certificate for automatic token retrieval when using the relevant OAuth-based authentication types. The `AuthenticationHeaderProvider` Java client library, part of SAP Java Buildpack, was adapted as well. The REST API already supports it.

-   The `ProxyType` attribute now offers the new option `PrivateLink`, allowing you to configure a destination with URL, and optionally a token service URL, pointing to services consumed via the SAP Private Link service \(beta\).

    For more information, see also [What Is SAP Private Link Service \(Beta\)?](https://help.sap.com/viewer/42acd88cb4134ba2a7d3e0e62c9fe6cf/CLOUD/en-US/3eb3bc7aa5db4b5da9dcdbf8ee478e52.html).

    > ### Note:  
    > The `CheckConnection` functionality as well as automatic token retrieval are not yet supported.




</td>
<td valign="top">

Info only

</td>
<td valign="top">

New

</td>
<td valign="top">

2021-11-18

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Neo



</td>
<td valign="top">

Destination Service - Features

</td>
<td valign="top">

The *Destinations* UI in the cockpit lets you configure an X.509 client certificate for automatic token retrieval when using the relevant OAuth-based authentication types. The `AuthenticationHeaderProvider` Java client library, part of the Neo runtimes, was adapted as well.

</td>
<td valign="top">

Info only

</td>
<td valign="top">

New

</td>
<td valign="top">

2021-11-18

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

Destination Service - Bug Fix

</td>
<td valign="top">

-   A change has been applied that improves the stability and availability of the service during startup, for example, in case of a rolling update.

-   A request processing change has been applied, improving asyncronous handling of the processing load, ultimately improving overall service stability and availability.



</td>
<td valign="top">

Info only

</td>
<td valign="top">

Changed

</td>
<td valign="top">

2021-11-18

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

Destination Service - OAuth

</td>
<td valign="top">

-   Destinations with `ProxyType` set to `OnPremise` can now be configured with OAuth-based authentication types, both via the BTP cockpit UI and the Destination service REST API.

-   Automated token retrieval from OAuth servers residing on premise, exposed via Connectivity service and Cloud Connector, is now supported.



</td>
<td valign="top">

Info only

</td>
<td valign="top">

New

</td>
<td valign="top">

2021-11-04

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

Connectivity Proxy Version 2.4.1

</td>
<td valign="top">

Connectivity proxy version 2.4.1 is now available.

-   Connectivity CA is now automatically downloaded during help deployment.
-   Applies critical preparation for adoption of SAP Cloud PKI.
-   Improved server certificate validation towards remote targets.
-   Multiple open source software components reported as vulnerable have been replaced.



</td>
<td valign="top">

Info only

</td>
<td valign="top">

Announcement

</td>
<td valign="top">

2021-10-21

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

Connectivity Service - Bug Fix

</td>
<td valign="top">

An internal service exception could result in a *502 Bad Gateway* error on the client side, which was visible in the Cloud Connector logs during automatic reconnect.

This issue has been fixed.

</td>
<td valign="top">



</td>
<td valign="top">

Changed

</td>
<td valign="top">

2021-10-07

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

Destination Service - Bug Fixes

</td>
<td valign="top">

-   In some cases, a Destination service instance could not be deleted. The operation now works as expected.

-   A performance optimisation reduces the overall amount of remote calls to XSUAA when the Destination service is called with a user token.

    As a result, less load is put on XSUAA, and the Destination service responds faster. This fix contributes to improving overall stability.




</td>
<td valign="top">



</td>
<td valign="top">

Changed

</td>
<td valign="top">

2021-10-07

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

SAP Java Buildpack

</td>
<td valign="top">

SAP Java Buildpack has been updated from version 1.38.0 to 1.39.0.

-   The `com.sap.cloud.security.xsuaa` API has been updated to version 2.10.5.
-   The Connectivity API extension has been updated to version 3.12.0.



</td>
<td valign="top">



</td>
<td valign="top">

New

</td>
<td valign="top">

2021-09-13

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

Destination Service - Authentication Types

</td>
<td valign="top">

When using authentication type `OAuth2ClientCredentials`, you can choose a tenant to perform automated token retrieval that is different from the tenant used to look up the destination configuration.

This feature is especially useful for automated service scenarios, like running offline jobs, and so on.

> ### Note:  
> You cannot use this feature in combination with a passed user context. In this case, the tenant used to perform automated token retrieval is exclusively determined by the user context.

For more information, see [OAuth Client Credentials Authentication](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/4e1d742a3d45472d83b411e141729795.html).

</td>
<td valign="top">



</td>
<td valign="top">

New

</td>
<td valign="top">

2021-08-26

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Neo



</td>
<td valign="top">

Destinations - Timeout Properties

</td>
<td valign="top">

You can configure timeout properties in the destination configuration, following a documented naming convention.

This feature lets you manage timeouts externally, regardless of the cloud application's lifecycle.

Using [HttpDestination](https://help.sap.com/viewer/b865ed651e414196b39f8922db2122c7/Cloud/en-US/c2a0d33bbc464b8fae30fed707ae9034.html) library version [2.15](https://search.maven.org/artifact/com.sap.cloud.connectivity/sap-cloud-connectivity-httpdestination/2.15.0/jar), timeout properties are processed at runtime when pre-configuring the HTTP client instance for the cloud application.

For more information, see [HTTP Destinations](https://help.sap.com/viewer/b865ed651e414196b39f8922db2122c7/Cloud/en-US/b068356dd7c34cf7ad6b6023deeb317d.html).

</td>
<td valign="top">



</td>
<td valign="top">

New

</td>
<td valign="top">

2021-08-26

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Cloud Foundry

-   Neo



</td>
<td valign="top">

Cloud Connector - Security Fixes

</td>
<td valign="top">

Multiple vulnerabilities in the Cloud Connector have been fixed.

For more information, see SAP security note [3058553](https://me.sap.com/notes/3058553).

</td>
<td valign="top">



</td>
<td valign="top">

Changed

</td>
<td valign="top">

2021-08-12

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

Destination Service - Client Certificates

</td>
<td valign="top">

When generating an X.509 client certificate \(as announced on July 1\), you can set a password to protect the private key. If you choose a PKCS12 file format, also the keystore is protected by the same password.

</td>
<td valign="top">



</td>
<td valign="top">

New

</td>
<td valign="top">

2021-08-12

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Neo



</td>
<td valign="top">

Destination Service - HTTP Headers

</td>
<td valign="top">

As of [HttpDestination version 2.14.0](https://search.maven.org/artifact/com.sap.cloud.connectivity/sap-cloud-connectivity-httpdestination/2.14.0/jar), any defined HTTP header in the destination configuration \(see [HTTP Destinations](https://help.sap.com/viewer/b865ed651e414196b39f8922db2122c7/Cloud/en-US/b068356dd7c34cf7ad6b6023deeb317d.html)\) is processed at runtime, that is, it is added to the request that is sent to the target server.

</td>
<td valign="top">



</td>
<td valign="top">

New

</td>
<td valign="top">

2021-08-12

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Neo



</td>
<td valign="top">

Connectivity Service - Bug Fix

</td>
<td valign="top">

A few stabilisation fixes have been applied in the Connectivity service to handle rare cases in which an abnormal amount of metering data was received by the Cloud Connector. This could cause a partial blockage of the service.

</td>
<td valign="top">



</td>
<td valign="top">

Changed

</td>
<td valign="top">

2021-08-12

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

Destination Service - Bug Fix

</td>
<td valign="top">

A few stabilisation fixes have been applied on the REST server-side logic, allowing more efficient parallel request handling under load.

</td>
<td valign="top">



</td>
<td valign="top">

Changed

</td>
<td valign="top">

2021-08-12

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Cloud Foundry

-   Neo



</td>
<td valign="top">

Cloud Connector 2.13.2 - Enhancements

</td>
<td valign="top">

Release of Cloud Connector version 2.13.2 introduces the following improvement:

-   The HTML validation of login information has been improved.



</td>
<td valign="top">



</td>
<td valign="top">

New

</td>
<td valign="top">

2021-07-15

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Cloud Foundry

-   Neo



</td>
<td valign="top">

Cloud Connector 2.13.2 - Fixes

</td>
<td valign="top">

Release of Cloud Connector version 2.13.2 provides the following bug fixes:

-   A regression prevented that links provided in the login info widget \(login screen\) could be clicked.

    This issue has been fixed.

-   When rewriting a location header for redirect responses \(status codes 30x\), the lookup to determine the virtual host that replaces the internal one is now case insensitive.

-   When using custom attributes in JWTs \(JSON web tokens\) for principal propagation, the value can now be extracted even if represented as single element array.

-   A slow network could prevent a successful initial push, caused by an unintended timeout. As a consequence, the configuration on the shadow instance could be incomplete, even though the shadow showed a successful connection.

    This issue has been fixed.

-   CPIC traces can now be turned on and off multiple times without the need to restart.

-   Issues with restoring a 2.13.x backup into a fresh installation on Linux have been fixed.




</td>
<td valign="top">



</td>
<td valign="top">

Changed

</td>
<td valign="top">

2021-07-15

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

Destination Service

</td>
<td valign="top">

-   Using the [Destination service REST API](https://api.sap.com/api/SAP_CP_CF_Connectivity_Destination/resource), you can configure a service-side issued X.509 client certificate as part of the [SAP Cloud PKI](http://cps.pki.co.sap.com/cps/SAP-Cloud-PKI_CP_v1.0.pdf) \(public key infrastructure\) and formally choose *automatic renewal* of the certificate.
-   The same feature is available in the *Destinations* editor of the cloud cockpit \(*Connectivity* \> *Destinations*\).
-   The *SAP Java Buildpack* now includes Java APIs as part of a client library for the Destination service. You can use the `ConnectivityConfiguration` Java API to retrieve destination and certificate configurations, and `AuthenticationHeaderProvider` Java API to provide prepared HTTP headers holding authentication tokens for various scenarios.

    For more information, see [Destination Java APIs](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/60f00ec5724e4875b51a2cadfb2364b2.html).




</td>
<td valign="top">



</td>
<td valign="top">

New

</td>
<td valign="top">

2021-07-01

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

Destination Service - Destinations Editor

</td>
<td valign="top">

The *Destinations* UI \(editor\) in the cockpit lets you create a certificate configuration entry containing an X.509 client certificate part of SAP Cloud PKI \(public key infrastructure\).

Optionally, you can specify values for the certificate common name \(CN\) as well as for the validity period \(minimum value: one day, maximum value: one year\). This feature has already been available via the Destination service REST API.

</td>
<td valign="top">



</td>
<td valign="top">

New

</td>
<td valign="top">

2021-06-17

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Cloud Foundry

-   Neo



</td>
<td valign="top">

Destination Service - Destinations Editor

</td>
<td valign="top">

The *Destinations* UI \(editor\) in the cockpit has introduced a warning message as a reminder that the user's personal password should not be used when configuring the authentication type of a destination, for example, `BasicAuthentication` or `OAuth2Password`.

The reason behind is that by design, destination configurations are meant to be used by one or more cloud applications which tipically are used by more than one person.

</td>
<td valign="top">



</td>
<td valign="top">

New

</td>
<td valign="top">

2021-06-17

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Cloud Foundry

-   Neo



</td>
<td valign="top">

Connectivity Service - Bug Fix

</td>
<td valign="top">

In rare cases, the Cloud Connector version shown in the cockpit \(*Connectivity* → *Cloud Connectors*\) got lost.

This issue has been fixed.

</td>
<td valign="top">



</td>
<td valign="top">

Changed

</td>
<td valign="top">

2021-06-17

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

Destination Service - Bug Fix

</td>
<td valign="top">

An issue has been resolved which prevented updating a service instance \(previously created in the cockpit\) via the Cloud Foundry CLI.

</td>
<td valign="top">



</td>
<td valign="top">

Changed

</td>
<td valign="top">

2021-06-17

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

Connectivity Service - Principal Propagation

</td>
<td valign="top">

You can configure a principal propagation scenario using a user access token issued by the Identity Authentication service \(IAS\), in addition to the scenarios based on XSUAA.

For more information, see [Principal Propagation via IAS Token](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/47a3cff4f33a4a0f9af1b0d6677a9e6e.html).

</td>
<td valign="top">



</td>
<td valign="top">

New

</td>
<td valign="top">

2021-06-03

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

Destination Service - HTTP Destinations

</td>
<td valign="top">

A naming convention has been introduced, specifying how to properly configure HTTP headers and queries in a destination configuration.

For more information, see [HTTP Destinations](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/42a0e6b966924f2e902090bdf435e1b2.html).

</td>
<td valign="top">



</td>
<td valign="top">

New

</td>
<td valign="top">

2021-06-03

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Cloud Foundry

-   Neo



</td>
<td valign="top">

Connectivity Service - Tunnel Connections

</td>
<td valign="top">

On the cloud side, the tunnel connection idle threshold has been increased to better match both older \(yet supported\) and latest Cloud Connector versions \(versions lower or equal to 2.13\). This ensures the internal heartbeat mechanism would work properly even in some special cases in which short interruptions have been observed.

</td>
<td valign="top">



</td>
<td valign="top">

Changed

</td>
<td valign="top">

2021-06-03

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

Destination Service - Bugfix

</td>
<td valign="top">

The service could have experienced delays in case of parallel load which caused requests to be executed unexpectedly slower on random basis. This issue has been fixed.

</td>
<td valign="top">



</td>
<td valign="top">

Changed

</td>
<td valign="top">

2021-06-03

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Cloud Foundry

-   Neo



</td>
<td valign="top">

Java Connector 3.1.4.0 - Enhancements

</td>
<td valign="top">

Release of Java Connector \(JCo\) version 3.1.4.0 introduces the following features and improvements:

-   JCo now offers the ABAP server processing time for JCo client scenarios via method `JCoThrougput.getServerTime()`.
-   `JCoRepository` methods were enhanced to ignore trailing blanks in passed structure, table, and function module names which are supposed to be looked up.
-   Performance was improved for setting `DATE` and `TIME` datatype fields when using *strings* as input values.



</td>
<td valign="top">



</td>
<td valign="top">

New

</td>
<td valign="top">

2021-05-20

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Cloud Foundry

-   Neo



</td>
<td valign="top">

Java Connector 3.1.4.0 - Bug Fixes

</td>
<td valign="top">

Release of Java Connector \(JCo\) version 3.1.4.0 provides the following bug fixes:

-   When invoking remote function modules \(RFMs\) via the t/q/bgRFC protocol to the same `JCoDestination` in multiple threads simultaneously, used TIDs, queue names and unit IDs could have been overwritten and used in the wrong thread context, which might have led to data loss in the target system.

    For example, IDocs that seemed to have been transferred correctly without an error, were not stored in the target system, because the TID contract was broken and several IDocs were erroneously sent at the same time with the same TID although different ones had been specified.

    This issue has been fixed.

    > ### Note:  
    > This regression bug was introduced with JCo 3.1.3.

-   When the new reentrance ticket technology, introduced as of S/4HANA 1909, was used to log on to the communication partner system, and `JCoCustomRepository` was configured to use query mode `DISABLE_REPOSITORY_POOL`, querying RFC metadata resulted in a logon failure \(*invalid logon ticket*\).

    This issue has been fixed.

-   If a JSON document contained numeric fields with negative values, for example, for a field of type `BCD` or `INT`, the JSON parser did not accept the sign character when analyzing the value for the given field. In this case, J`CoRecord.fromJSON()` threw an exception similar to *JCoSerializationException: \(191\) JCO\_ERROR\_SERIALIZATION: Digit\(s\) expected near position <\#\#\#\>*.

    This issue has been fixed.




</td>
<td valign="top">



</td>
<td valign="top">

Changed

</td>
<td valign="top">

2021-05-20

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

Cloud Foundry

</td>
<td valign="top">

Cockpit: Cloud Connectors View

</td>
<td valign="top">

The *Cloud Connectors* view in the SAP BTP cockpit is now also available if your account is running on cloud management tools feature set B. For more information, see [Monitoring](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/6d9c937dd35344bca3eb61ebf34a5c1d.html) \(section *Monitoring from the Cockpit*\).

</td>
<td valign="top">



</td>
<td valign="top">

New

</td>
<td valign="top">

2021-04-22

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Neo
-   Cloud Foundry



</td>
<td valign="top">

Cloud Connector 2.13.1 - Enhancements

</td>
<td valign="top">

Release of Cloud Connector version 2.13.1 introduces the following features and improvements:

-   Additional audit log entries for changing the trace level are available.
-   You can open the support log assistant directly from the *Log And Trace Files* screen.

    For more information, see [Troubleshooting](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/e7df7f15bb571014ae24bca245319880.html), section *Log And Trace Files*.

-   The dependency on ping checks for connections to the LDAP system, which is used for UI authentication, has been minimized to avoid unnecessary role switches in high availability mode.



</td>
<td valign="top">



</td>
<td valign="top">

New

</td>
<td valign="top">

2021-03-25

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Neo
-   Cloud Foundry



</td>
<td valign="top">

Cloud Connector 2.13.1 - Fixes

</td>
<td valign="top">

Release of Cloud Connector version 2.13.1 provides the following bug fixes:

-   Connecting a subaccount with several hundred access control entries is working again.
-   With release 2.13.1, restoring a backup created in version 2.13.0 works properly again for a Cloud Connector running on Linux.
-   Backups created in version 2.12.5 and older can be restored properly. Failures on restore led to a non-usable Cloud Connector setup.
-   The following high availability issues have been fixed:
    -   Improved implementation ensures that a high availability setup does not end up in a shadow/shadow situation. This issue could occur under rare circumstances.
    -   Errors could occur if subaccounts have a larger number of access control entries.
    -   Network issues could prevent the individual replication of configuration changes.
    -   After switching roles, connections can now always be reestablished correctly.

-   The connection test for LDAPS access control entries now works correctly.
-   A memory leak in the comprised netty library has been fixed by upgrading to a newer version.
-   A subaccount display issue has been fixed: In version 2.13.0, subaccounts on *eu2.hana.ondemand.com* were displayed as belonging to region Europe \(Rot\) instead of Europe \(Frankfurt\).



</td>
<td valign="top">



</td>
<td valign="top">

Changed

</td>
<td valign="top">

2021-03-25

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

Cloud Foundry

</td>
<td valign="top">

Destination Service - Mobile Service Instances

</td>
<td valign="top">

You can create a destination configuration pointing to a mobile service instance, resulting in a fully functional destination configuration, including automatic token retrieval for the respective OAuth flows supported by the mobile service.

</td>
<td valign="top">



</td>
<td valign="top">

New

</td>
<td valign="top">

2021-02-25

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Kyma
-   Other



</td>
<td valign="top">

Destination Service - Consumption from Kyma or Kubernetes Environments

</td>
<td valign="top">

Consumption of the Destination service from the Kyma or Kubernetes environments has been officially documented.

For more information, see [Create and Bind a Destination Service Instance](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/9fdad3cad92e4b63b73d5772014b380e.html).

</td>
<td valign="top">



</td>
<td valign="top">

New

</td>
<td valign="top">

2021-02-25

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

Cloud Foundry

</td>
<td valign="top">

Principal Propagation Authentication - OpenID Connect

</td>
<td valign="top">

When sending a user principal via the HTTP header `X-user-token`, you can use any *OpenID Connect*-compliant OAuth server and a related OpenID access token for passing the user identity.

To enable this feature, you must specify either `x_user_token.jwks_uri` `x_user_token.jwks` as additional attribute, as described in the respective authentication type. or

For more information, see [HTTP Destinations](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/42a0e6b966924f2e902090bdf435e1b2.html).

</td>
<td valign="top">



</td>
<td valign="top">

New

</td>
<td valign="top">

2021-02-11

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

Cloud Foundry

</td>
<td valign="top">

OAuth - X.509 Client Certificates

</td>
<td valign="top">

You can use X.509 client certificates for OAuth flows supported by the respective authentication types, see [OAuth with X.509 Client Certificates](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/2c162aaa9e464480b2307879d1b865f5.html).

</td>
<td valign="top">



</td>
<td valign="top">

New

</td>
<td valign="top">

2021-02-11

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

Cloud Foundry

</td>
<td valign="top">

"Find Destination" REST API - Skip Credentials

</td>
<td valign="top">

The "Find Destination" REST API endpoint has been enhanced with a new feature enabling the client application to initiate a skip of credentials in the returned response.

This parameter is useful especially for OAuth destinations \(such as *OAuth2 User Token Exchange*, *OAuth2 JWT Bearer*, *OAuth2 SAML Bearer Assertion*\).

The client application may actually need only the auto-retrieved token by the service, which makes the credentials optional for the application, and in certain cases they are preferred not to be returned in the response.

For more information, see [SAP API Business Hub](https://api.sap.com/api/SAP_CP_CF_Connectivity_Destination/resource).

</td>
<td valign="top">



</td>
<td valign="top">

New

</td>
<td valign="top">

2021-02-11

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

Cloud Foundry

</td>
<td valign="top">

Destinations - Authentication Types

</td>
<td valign="top">

-   The property `SystemUser` is deprecated. The cockpit now shows an alert if this feature is still in use, suggesting what to do instead. Alternatives for technical user authentication are *Basic Authentication*, *OAuth2 Client Credentials*, or *Client Certificate Authentication*.

    See also [OAuth SAML Bearer Assertion Authentication](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/c69ea6aacd714ad2ae8ceb5fc3ceea56.html).

    > ### Note:  
    > In general, we recommend that you work on behalf of specific \(named\) users rather than working with a technical user. To extend an OAuth access token's validity, consider using an OAuth refresh token.

-   Authentication type *SAP Assertion SSO* is deprecated. The cockpit now shows an alert if this feature is still in use, suggesting what to do instead.

    Authentication types *Principal Propagation* \(for on-premise connections\), *OAuth2 SAML Bearer Assertion* \(Internet connections\) or *SAML Assertion* \(Internet connections\) are the recommended mechanisms for establishing single sign-on \(SSO\).

    See [SAP Assertion SSO Authentication](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/ceb8c4fa61e6443190185696c6d0342d.html).




</td>
<td valign="top">



</td>
<td valign="top">

Changed

</td>
<td valign="top">

2021-02-11

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

Neo

</td>
<td valign="top">

Password Storage API

</td>
<td valign="top">

The Password Storage API documentation on SAP API Business Hub has been moved from the deprecated API package ** to [SAP Cloud Platform Credential Store](https://api.sap.com/package/CredentialStore?section=Artifacts).

</td>
<td valign="top">



</td>
<td valign="top">

Changed

</td>
<td valign="top">

2021-01-28

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Neo
-   Cloud Foundry



</td>
<td valign="top">

Cloud Connector 2.13.0 - Enhancements

</td>
<td valign="top">

Release of Cloud Connector version 2.13.0 introduces the following features and improvements:

-   Cloud Connector 2.13 is based on a different runtime container.

    Up to version 2.12.x, the JavaWeb 1.x runtime based on Tomcat 7 was used. It now switches to JavaWeb 3.x based on Tomcat 8.5.

    As a consequence, the internal structure has changed and works differently. The upgrade will adjust these changes as much as possible for versions 2.9 and higher.

-   Linux on *ppc64 little endian* \(ppc64le\) is added as a supported platform for the Cloud Connector.

    For more information, see [Prerequisites](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/e23f776e4d594fdbaeeb1196d47bbcc0.html#loioe23f776e4d594fdbaeeb1196d47bbcc0__matrix).

-   A set of new configuration REST APIs has been added.

    For more information, see [Configuration REST APIs](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/cfb9d579f50b4711a514dc8f08d22f73.html).

-   An additional screen in the subaccount-specific monitoring provides usage statistics of the various access control entries.

    Alternatively, you can access the same data using a new monitoring REST API.

    For more information, see [Monitoring](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/6d9c937dd35344bca3eb61ebf34a5c1d.html).

-   For access control entries of type TCP, you can configure a port range instead of a single port.

    For more information, see [Configure Access Control \(TCP\)](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/befd4374d33a4833be117d7149b6a103.html).

-   You can configure a widget that shows information about the Cloud Connector on the login screen.

    For more information, see [Configure Login Screen Information](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/916df5b825494bc087a5a619e741eeef.html).

-   Improved high availability communication supersedes applying SAP note [2915578](https://launchpad.support.sap.com/#/notes/2915578/E).
-   For new Cloud Connector versions, a notification and alert is shown to help you schedule the update.
-   The Cloud Connector supports JSON Web tokens \(JWTs\) based on OpenID-Connect \(OIDC\) for principal propgation authentication \(Cloud Foundry environment\).

    For more information, see [Configure Principal Propagation via OIDC Token](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/000232bddce348ecb068fcbf9d13717d.html).

-   Client-side load balancing based on round-robin was introduced for Cloud Connector connections to SAP Cloud Platform to address its endpoints which are exposed on multiple IP addresses for high availability.

-   Scenarios based on the HTTP header *Expect: 100-continue* and response code *HTTP 100* are now supported.




</td>
<td valign="top">



</td>
<td valign="top">

New

</td>
<td valign="top">

2021-01-14

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

-   Neo
-   Cloud Foundry



</td>
<td valign="top">

Cloud Connector 2.13.0 - Fixes

</td>
<td valign="top">

Release of Cloud Connector version 2.13.0 provides the following bug fixes:

-   When doing a rollover at midnight, the initial audit log entry for a new file was not created correctly and the audit log checker wrongly assessed such files as corrupted.

    This issue has been fixed.

-   Incorrect host information could be used in audit logs related to access control audit entries.

    This issue has been fixed.




</td>
<td valign="top">



</td>
<td valign="top">

Changed

</td>
<td valign="top">

2021-01-14

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration Suite

</td>
<td valign="top">

Cloud Foundry

</td>
<td valign="top">

Cloud Connector - Subaccount Configuration

</td>
<td valign="top">

For a subaccount that uses a custom identity provider \(IDP\), you can choose this IDP for authentication instead of the \(default\) SAP ID service when configuring the subaccount in the Cloud Connector.

For more information, see [Use a Custom IDP for Subaccount Configuration](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/202261235a204db5ba0b35bbaa6d40ff.html).

</td>
<td valign="top">



</td>
<td valign="top">

New

</td>
<td valign="top">

2021-01-14

</td>
</tr>
</table>

