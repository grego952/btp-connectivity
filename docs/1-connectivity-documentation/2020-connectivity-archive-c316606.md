<!-- loioc316606caef14baf81fbf4c74dfb8303 -->

# 2020 Connectivity \(Archive\)





**2020**


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

-   Neo
-   Cloud Foundry



</td>
<td valign="top">

Java Connector \(JCo\) - Client Certificates

</td>
<td valign="top">

JCo provides the new property `jco.client.tls_client_certificate_logon` to support the usage of a TLS client certificate for logging on to an ABAP system via WebSocket RFC.

For more information, see:

[User Logon Properties](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/8b1e1c3b3e284d61bc167e84d4c9d7a1.html) \(Cloud Foundry environment\)

[User Logon Properties](https://help.sap.com/viewer/b865ed651e414196b39f8922db2122c7/Cloud/en-US/629f957a973b49fda84f67338ab39371.html) \(Neo environment\)

For more information on WebSocket RFC, see also:

[WebSocket RFC](https://help.sap.com/viewer/753088fc00704d0a80e7fbd6803c8adb/202009.001/en-US/51f1edadb2754e539f6e6335dd1eb4cc.html)

</td>
<td valign="top">

New

</td>
<td valign="top">

2020-12-17

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

HTTP Destinations - Authentication Types

</td>
<td valign="top">

Authentication type *SAP Assertion SSO* is deprecated. It will soon be removed as a feature from the Destination service.

Use [Principal Propagation SSO Authentication](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/73194cc419894433994c5f0444b4c6a1.html) instead, which is the recommended mechanism for establishing single sign-on \(SSO\).

</td>
<td valign="top">

Deprecated

</td>
<td valign="top">

2020-12-17

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

HTTP Destinations - Authentication Types

</td>
<td valign="top">

Authentication type *SAP Assertion SSO* is deprecated.

Use [Principal Propagation SSO Authentication](https://help.sap.com/viewer/b865ed651e414196b39f8922db2122c7/Cloud/en-US/56dd01441ef443c488406940ce09da8b.html) instead, which is the recommended mechanism for establishing single sign-on \(SSO\).

</td>
<td valign="top">

Deprecated

</td>
<td valign="top">

2020-12-17

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

HTTP Destinations - Destination Properties

</td>
<td valign="top">

The destination property `SystemUser` for the authentication types:

-   OAuth SAML Bearer Assertion Authentication
-   SAP Assertion SSO Authentication

will be removed soon. More information on timelines and required actions will be published in the release notes at a later stage.

See also:

[OAuth SAML Bearer Assertion Authentication](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/c69ea6aacd714ad2ae8ceb5fc3ceea56.html)

[SAP Assertion SSO Authentication](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/ceb8c4fa61e6443190185696c6d0342d.html)

</td>
<td valign="top">

Announcement

</td>
<td valign="top">

2020-12-03

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

JCo Runtime - Enhancement

</td>
<td valign="top">

JCo Runtime 3.1.3.0 introduces the following enhancement:

If the backend is known to be new enough, JCo does not check for the existence of RFC\_METADATA\_GET, thus avoiding the need to provide additional authorizations for the repository user.

</td>
<td valign="top">

New

</td>
<td valign="top">

2020-11-05

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

JCo Runtime - Bug Fix

</td>
<td valign="top">

JCo Runtime 3.1.3.0 provides the following bug fix:

Up to JCo 3.1.2, the initial value for fields of type STRING and XSTRING was *null*. Since the initial value check in ABAP is different, JCo now behaves the same way and uses an emtpy string and an empty byte array, respectively.

</td>
<td valign="top">

Changed

</td>
<td valign="top">

2020-11-05

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

Destination Service - Automatic Token Retrieval

</td>
<td valign="top">

The Destination service offers a new feature related to the automatic token retrieval functionality, which lets the destination administrator define HTTP headers and query parameters as additional configuration properties, used at runtime when requesting the token service to obtain an access token.

See [HTTP Destinations](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/42a0e6b966924f2e902090bdf435e1b2.html).

</td>
<td valign="top">

New

</td>
<td valign="top">

2020-11-05

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

Documentation - Principal Propagation Scenarios

</td>
<td valign="top">

The documentation of principal propagation \(user propagation\) scenarios provides improved information on the basic concept and guidance on how to set up different scenarios.

See [Principal Propagation](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/e2cbb48def4342048362039cc157b12e.html).

</td>
<td valign="top">

Changed

</td>
<td valign="top">

2020-10-22

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

Cloud Connector 2.12.5 - Enhancements

</td>
<td valign="top">

Release of Cloud Connector version 2.12.5 introduces the following improvements:

-   For principal propagation scenarios, custom attributes stored in `xs.user.attributes` of the JWT \(JSON Web token\) are now accessible for the subject pattern. See [Configure a Subject Pattern for Principal Propagation](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/58803a25e5894d759e0df1c5513b41ed.html).
-   Improved resolving for DNS names with multiple IP addresses by adding randomness to the choice of the IP to use. This is relevant for many connectivity endpoints in SAP Cloud Platform, Cloud Foundry environment.



</td>
<td valign="top">

New

</td>
<td valign="top">

2020-10-22

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

Cloud Connector 2.12.5 - Fixes

</td>
<td valign="top">

Release of Cloud Connector version 2.12.5 provides the following bug fixes:

-   After actively performing a master-shadow switch for a disaster recovery subaccount, a zombie connection could cause a timeout of all application requests to on-premise systems. This issue has been fixed.
-   When refreshing the subaccount certificate in an high availability setup, transferring the changed certificate to the shadow was not immediately triggered, and the updated certificate could get lost. This issue has been fixed.
-   If many RFC connections were canceled at the same time, the Cloud Connector could crash in the native layer, causing the process to die. This issue has been fixed.
-   The LDAP configuration test now supports all possible configuration parameters.



</td>
<td valign="top">

Changed

</td>
<td valign="top">

2020-10-22

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

Connectivity Service - Service Instances - Quota Management

</td>
<td valign="top">

When using service plan “lite”, quota management is no longer required for this service. From any subaccount you can consume the service using service instances without restrictions on the instance count.

Previously, access to service plan “lite” has been granted via entitlement and quota management of the application runtime. It has now become an integral service offering of SAP Cloud Platform to simplify its usage.

See also [Create and Bind a Connectivity Service Instance](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/a2b88cf9d41e4061bfb06a23d9ba1c43.html).

</td>
<td valign="top">

Changed

</td>
<td valign="top">

2020-10-08

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

Destination Service - Service Instances - Quota Management

</td>
<td valign="top">

When using service plan “lite”, quota management is no longer required for this service. From any subaccount you can consume the service using service instances without restrictions on the instance count.

Previously, access to service plan “lite” has been granted via entitlement and quota management of the application runtime. It has now become an integral service offering of SAP Cloud Platform to simplify its usage.

See also [Create and Bind a Destination Service Instance](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/9fdad3cad92e4b63b73d5772014b380e.html).

</td>
<td valign="top">

Changed

</td>
<td valign="top">

2020-10-08

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

SAP Java Buildpack - Java Connector \(JCo\)

</td>
<td valign="top">

The SAP Java Buildpack has been updated from 1.27.3. to 1.28.0.

-   TomEE Tomcat has been updated from 7.0.104 to 7.0.105.
-   SAPJVM has been updated to 81.65.65.
-   The *com.sap.cloud.security.xsuaa* API has been updated from 2.7.5 to 2.7.6.
-   The SAP HANA driver has been updated from 2.5.49 to 2.5.52.
-   **JCo-corresponding libraries** have been updated: *connectivity* to 3.3.3, *connectivity apiext* to 0.1.37.
-   The **activation process for the JCo component** in the SAP Java Buildpack has been changed. Starting with this release, it is activated by setting the following environment variable: ***<USE\_JCO=true\>***.

    > ### Note:  
    > The **previous activation process** for the JCo component is deprecated and **will expire after a transition period**.




</td>
<td valign="top">

Changed

</td>
<td valign="top">

2020-09-24

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

Destination Service - Error Handling

</td>
<td valign="top">

Error handling has been improved for updating service instances via the Cloud Foundry CLI and the cloud cockpit when providing the configuration JSON data.

</td>
<td valign="top">

Changed

</td>
<td valign="top">

2020-09-10

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

Connectivity Service - Bug Fix

</td>
<td valign="top">

A synchronization issue has been fixed on cloud side that in very rare cases could lead to a *zombie* tunnel from the Cloud Connector to SAP Cloud Platform, which required to reconnect the Cloud Connector.

</td>
<td valign="top">

Changed

</td>
<td valign="top">

2020-09-10

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

Destination Service - Bug Fix

</td>
<td valign="top">

During *Check Connection* processing of a destination with basic authentication, the Destination service now uses the user credentials for both the HTTP HEAD and HTTP GET requests to verify the connection on HTTP level.

</td>
<td valign="top">

Changed

</td>
<td valign="top">

2020-09-10

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

Destination Service - Bug Fix

</td>
<td valign="top">

Using authentication type `OAuth2SAMLBearerAssertion`, an issue could occur when adding the user's SAML group attributes into the resulting SAML assertion that is sent to the target token service. This issue has been fixed.

</td>
<td valign="top">

Changed

</td>
<td valign="top">

2020-08-13

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

Destination Service REST API - Pagination Feature

</td>
<td valign="top">

The REST API pagination feature provides improved error handling in case of issues with the pagination, for example, if an invalid page number is provided.

</td>
<td valign="top">

Changed

</td>
<td valign="top">

2020-08-13

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

HttpDestination Library - New Version

</td>
<td valign="top">

The `HttpDestination` v2 library has been officially released in the [Maven Central Repository](https://search.maven.org/search?q=a:sap-cloud-connectivity-httpdestination). It enables the usage in Tomcat and TomEE-based runtimes the same way as in the deprecated *JavaWeb* and *Java EE 6 Web Profile* runtimes. See also [HttpDestination Library](https://help.sap.com/viewer/b865ed651e414196b39f8922db2122c7/Cloud/en-US/c9bb25f2c35e4fddb8c86382cb87ce7a.html).

</td>
<td valign="top">

New

</td>
<td valign="top">

2020-07-30

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

Destination Service - Bug Fix

</td>
<td valign="top">

An error handling issue has been fixed in the Destination service, which is related to the recently introduced *SAP Assertion SSO authentication* type. If a wrong input was provided, you can now see the error properly, and recover it.

</td>
<td valign="top">

Changed

</td>
<td valign="top">

2020-07-30

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

You can use authentication type `OAuth2JWTBearer` when configuring a Destination. It is a simplified version of the authentication type `OAuth2UserTokenExchange` and represents the official OAuth grant type for exchanging OAuth tokens. See [HTTP Destinations](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/42a0e6b966924f2e902090bdf435e1b2.html).

</td>
<td valign="top">

New

</td>
<td valign="top">

2020-07-02

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

Destination Service - HTTP Header

</td>
<td valign="top">

The Destination service provides a prepared HTTP header that simplifies application and service development. See [HTTP Destinations](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/42a0e6b966924f2e902090bdf435e1b2.html) \(code samples\).

</td>
<td valign="top">

New

</td>
<td valign="top">

2020-07-02

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

Destination Service - Bug Fix

</td>
<td valign="top">

A concurrency issue in the Destination service, related to parallel auth token retrieval in the token cache functionality, could result in partial request failures. This issue has been fixed.

</td>
<td valign="top">

Changed

</td>
<td valign="top">

2020-07-02

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

HTTP Destinations - Authentication Types

</td>
<td valign="top">

The Cloud Foundry environment supports `SAP Assertion SSO` as authentication type for configuring destinations in the Destination service. See [HTTP Destinations](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/42a0e6b966924f2e902090bdf435e1b2.html).

</td>
<td valign="top">

New

</td>
<td valign="top">

2020-06-18

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

Destination Service REST API

</td>
<td valign="top">

The "Find Destination" REST API now includes the scopes of the automatically retrieved access token in the response that is returned to the caller. See ["Find Destination" Response Structure](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/83a3f3b9cd314618aba651044ed5b9df.html#loio83a3f3b9cd314618aba651044ed5b9df__tokens).

</td>
<td valign="top">

New

</td>
<td valign="top">

2020-06-04

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

Destinations for Service Instances

</td>
<td valign="top">

For subscription-based scenarios, you can use an automated procedure to create a destination that points to your service instance. See [Managing Destinations](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/84e45e071c7646c88027fffc6a7bb787.html).

</td>
<td valign="top">

New

</td>
<td valign="top">

2020-06-04

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

Connectivity Service - Bug Fix

</td>
<td valign="top">

In rare cases, establishing a secure tunnel between Cloud Connector \(version 2.12.3 or older\) and the Connectivity service could cause an issue that requires to manually disconnect and connect the Cloud Connector.

This issue has been fixed. The fix requires Cloud Connector version 2.12.4 or higher.

</td>
<td valign="top">

Changed

</td>
<td valign="top">

2020-05-21

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

Cloud Connector 2.12.4 - Features

</td>
<td valign="top">

Release of Cloud Connector version 2.12.4 introduces the following features and enhancements:

-   You can activate the SSL trace in the Cloud Connector administration UI also for the shadow instance.



</td>
<td valign="top">

New

</td>
<td valign="top">

2020-05-07

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

Cloud Connector 2.12.4 - Fixes

</td>
<td valign="top">

Release of Cloud Connector version 2.12.4 provides the following bug fixes:

-   You can edit and delete domain mappings in the Cloud Connector administration UI correctly.
-   The REST API does no longer return an empty configuration.
-   REST API DELETE operations do not require setting a content-type application/json to function properly.
-   If more than 2000 audit log entries match a selection, redefining the search and getting a shorter list now works as expected.
-   A potential leak of HTTP backend connections has been closed.



</td>
<td valign="top">

Changed

</td>
<td valign="top">

2020-05-07

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

Connectivity Service - Bug Fix

</td>
<td valign="top">

A fix has been applied in the Connectivity service internal load balancers, enabling the sending of TCP keep-alive packets on client and server side. This change mainly affects SOCKS5-based communication scenarios.

</td>
<td valign="top">

Changed

</td>
<td valign="top">

2020-03-26

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

Destination Service - Service Instances

</td>
<td valign="top">

You can create a service instance specifying an update policy. This allows you to avoid name conflicts with existing destinations. See [Create and Bind a Destination Service Instance](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/9fdad3cad92e4b63b73d5772014b380e.html).

</td>
<td valign="top">

New

</td>
<td valign="top">

2020-03-26

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

Cockpit - Destination Management

</td>
<td valign="top">

The *Destinations* editor in the cockpit is available for accounts running on the cloud management tools feature set B. See [Managing Destinations](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/84e45e071c7646c88027fffc6a7bb787.html).

</td>
<td valign="top">

New

</td>
<td valign="top">

2020-03-12

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

Connectivity Service - Bug Fix

</td>
<td valign="top">

When creating or editing a destination with authentication type `OAuth2ClientCredentials` in the cockpit, the parameter `Audience` could not be added as additional property. This issue has been fixed.

</td>
<td valign="top">

Changed

</td>
<td valign="top">

2020-03-12

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

Cloud Connector 2.12.3 - Features

</td>
<td valign="top">

Release of Cloud Connector version 2.12.3 introduces the following features and enhancements:

-   When using the SAP JVM as runtime, the thread dump includes additional information about currently executed RFC function modules.
-   The hardware monitor includes a Java Heap history, showing the usage in the last 24 hours.
-   If you are using the file `scc_daemon_extension.sh` to extend the daemon in a Linux installation, the content is included in the initialization section of the daemon. This lets you make custom extensions to the daemon that survive an upgrade. See [Installation on Linux OS](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/f069840fa34c4196a5858be33a2734ea.html), section *Installer Scenario*.



</td>
<td valign="top">

New

</td>
<td valign="top">

2020-02-27

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

Cloud Connector 2.12.3 - Fixes

</td>
<td valign="top">

Release of Cloud Connector version 2.12.3 provides the following bug fixes:

-   When switching roles between master and shadow instance in a high availability setup, the switch is no longer blocked by active RFC function module invocations.
-   A fix in the backend HTTP connection handling prevents issues when the backend tries to send the HTTP response before completely reading the HTTP request.
-   When sending large amounts of data to an on-premise system, and using RFC with a network that provides large bandwidth, the Cloud Connector could fail with the error message *Received invalid block with negative size*. This issue has been fixed.
-   The Cloud Connector admin UI now shows the correct user information for installed Cloud Connector instances in the *About* window.
-   Fixes in the context of disaster recovery:
    -   The location ID is now handled properly when setting it *after* adding the recovery subaccount.
    -   Application trust settings and application-specific connections are applied in the disaster case.
    -   Principal propagation settings are applied in the disaster case




</td>
<td valign="top">

Changed

</td>
<td valign="top">

2020-02-27

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

JCo Runtime - WebSocket RFC

</td>
<td valign="top">

The JCo runtime in SAP Cloud Platform lets you use WebSocket RFC \(RFC over Internet\) with ABAP servers as of S/4HANA \(on-premise\) version 1909. In the RFC destination configuration, this is reflected by new configuration properties and by the option to choose between different proxy types.

See [Target System Configuration](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/ab6eac92978f469e9eabe3d477ca2411.html) \(Cloud Foundry environment\), or [Target System Configuration](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/f8fac995b0144a0b8ec0801b8f7bab3e.html) \(Neo environment\).

</td>
<td valign="top">

New

</td>
<td valign="top">

2020-02-13

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

Connectivity Service for Trial Accounts - Bug Fix

</td>
<td valign="top">

The Connectivity service is operational again for trial accounts. A change in the Cloud Foundry Core component caused the service not be accessible by applications hosted in DiegoCell that are dedicated for trial usage in a separate VPC \(virtual private cloud\) account. This issue has been fixed.

</td>
<td valign="top">

Changed

</td>
<td valign="top">

2020-01-30

</td>
</tr>
</table>

