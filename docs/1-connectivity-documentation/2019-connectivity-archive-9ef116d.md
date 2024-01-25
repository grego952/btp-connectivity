<!-- loio9ef116dfb6dd46c0ad3a865e9e91976e -->

# 2019 Connectivity \(Archive\)


 


**2019**


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

Cloud Connector 2.12.2 - Features

</td>
<td valign="top">

Release of Cloud Connector version 2.12.2 introduces the following features and enhancements:

-   You can turn on the TLS trace from the Cloud Connector administration UI instead of modifying the `props.ini` file on OS level. See [Troubleshooting](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/e7df7f15bb571014ae24bca245319880.html).

-   The status of the used subaccount certificate is shown on the *Subaccount* overview page of the Cloud Connector administration UI, in addition to expiring certificates shown in the *Alerting* view. See [Establish Connections to SAP Cloud Platform](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/db9170a7d97610148537d5a84bf79ba2.html#loiodb9170a7d97610148537d5a84bf79ba2__establish_cloud_conection).




</td>
<td valign="top">

New

</td>
<td valign="top">

2019-12-05

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

Cloud Connector 2.12.2 - Fixes

</td>
<td valign="top">

Release of Cloud Connector version 2.12.2 provides the following bug fixes:

-   Subject values for certificates requiring escaping are treated correctly.

-   Establishing a connection to the master is now possible when being logged on to the shadow with a user that has a space in its name.

-   Performance statistics could show too long total execution times. This issue has been fixed.

-   IP address changes for the connectivity service hosts are recognized properly.

-   The Cloud Connector could crash on Windows, when trying to enable the payload trace with 4-eyes-principle without the required user permissions. This issue has been fixed.




</td>
<td valign="top">

Changed

</td>
<td valign="top">

2019-12-05

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

Applications sending a significant amount of data payload during OAuth authorization processing could cause an out-of-memory error on the Connectivity service side. This issue has been fixed.

</td>
<td valign="top">

Changed

</td>
<td valign="top">

2019-11-21

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

Region Europe \(Frankfurt\) - Change of Connectivity Service Hosts

</td>
<td valign="top">

The following IP addresses of the Connectivity service hosts for region Europe/Frankfurt \(`eu2.hana.ondemand.com`\) will change on **26 October 2019**:

-   `connectivitynotification.eu2.hana.ondemand.com`: from 157.133.70.140 \(current\) to 157.133.206.143 \(new\)
-   `connectivitycertsigning.eu2.hana.ondemand.com`: from 157.133.70.132 \(current\) to 157.133.205.174 \(new\)
-   `connectivitytunnel.eu2.hana.ondemand.com`: from 157.133.70.141 \(current\) to 157.133.205.233 \(new\)

If you have allowed the current addresses or IP ranges in your firewall rules, make sure you also include the new values **before 26 October 2019**.

See also: [Prerequisites: Network](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/e23f776e4d594fdbaeeb1196d47bbcc0.html#loioe23f776e4d594fdbaeeb1196d47bbcc0__network).

</td>
<td valign="top">

Announcement

</td>
<td valign="top">

2019-10-03

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

Destination Service - Connection Check

</td>
<td valign="top">

Using the *Destinations* editor in the cockpit, you can check connections also for on-premise destinations.

See [Check the Availability of a Destination](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/71ea3ccf4ebc4c63a3989c0b318e3e9b.html).

</td>
<td valign="top">

Changed

</td>
<td valign="top">

2019-09-26

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

Cloud Connector - Java Runtime

</td>
<td valign="top">

The support for using Cloud Connector with Java runtime version 7 will end on December 31, 2019. Any Cloud Connector version released after that date may contain Java byte code requiring at least a JVM 8.

We therefore strongly recommend that you perform **fresh** installations only with **Java 8**, and **update** existing installations running with Java 7, to Java 8 as of now.

See [SAP Cloud Connector – Java 7 support will phase out](https://blogs.sap.com/2019/09/12/sap-cloud-connector-java-7-support-will-phase-out/) and [Update the Java VM](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/0eb9851c41914d379feb138bf808a18f.html).

</td>
<td valign="top">

Announcement

</td>
<td valign="top">

2019-09-13

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

Cloud Connector 2.12.1 - Features

</td>
<td valign="top">

Release of Cloud Connector version 2.12.1 introduces the following features and enhancements:

-   Subject Alternative Names are separated from the subject definition and provide enhanced configuration options. You can configure complex values easily when creating a certificate signing request.

    See [Exchange UI Certificates in the Administration UI](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/b70bf164a6e6498b8bf1f459554609f5.html).

-   In a high availability setup, the master instance detection no longer switches automatically if the configuration between the two instances is inconsistent.
-   Disaster recovery switch back to main subaccount is periodically checked \(if not successful\) every 6 hours.
-   Communication to on-premise systems supports SNI \(Server Name Indication\).



</td>
<td valign="top">

New

</td>
<td valign="top">

2019-08-15

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

Cloud Connector 2.12.1 - Fixes

</td>
<td valign="top">

Release of Cloud Connector version 2.12.1 provides the following bug fixes:

-   The communication between master and shadow instance no longer ends up in unusable clients that show 403 results due to CSRF \(Cross-Site Request Forgery\) failures, which could cause undesired role switches.
-   When restoring a backup, the administrator password check works with all LDAP servers.
-   The LDAP configuration test utility properly supports secure communication.
-   The Refresh Subaccount Certificate dialog is no longer hanging when the refresh action fails due to some authentication or authorization issue.



</td>
<td valign="top">

Changed

</td>
<td valign="top">

2019-08-15

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

Destination Service - Scope Attribute for OAuth-based Authentication Types

</td>
<td valign="top">

You can use the `scope` destination attribute for the OAuth-based authentication types `OAuth2ClientCredentials`, `OAuth2UserTokenExchange` and `OAuth2SAMLBearerAssertion`. This additional attribute provides flexibility on destination configuration level, letting you specify what scopes are selected when the OAuth access token is automatically retrieved by the service.

See [HTTP Destinations](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/42a0e6b966924f2e902090bdf435e1b2.html).

</td>
<td valign="top">

New

</td>
<td valign="top">

2019-08-15

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

JCo Runtime for SAP Cloud Platform - Features

</td>
<td valign="top">

-   Additional APIs have been added to `JCoBackgroundUnitAttributes`. See API documentation for details.
-   If a structure or table contains only char-like fields, new APIs let you read or modify all of them at once for the structure or the current table row.

    See API documentation of `JCoTable` and `JCoStructure`.




</td>
<td valign="top">

New

</td>
<td valign="top">

2019-07-18

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

JCo Runtime for SAP Cloud Platform - Fixes

</td>
<td valign="top">

-   qRFC and tRFC requests sent to an ABAP system by JCo can be monitored again by AIF.
-   Structure fields of type STRING are no longer truncated if there is a white space at the end of the field.



</td>
<td valign="top">

Changed

</td>
<td valign="top">

2019-07-18

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

Connectivity Service - JCo Multitenancy

</td>
<td valign="top">

The Connectivity service supports multitenancy for JCo applications.

This feature requires a runtime environment with SAP Java Buildpack version 1.9.0 or higher.

See [Scenario: Multitenancy for JCo Applications \(Advanced\)](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/93c1e031e2434fc09a13bbd8ea87d1db.html).

</td>
<td valign="top">

New

</td>
<td valign="top">

2019-06-20

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

Cloud Cockpit - Cloud Connector View

</td>
<td valign="top">

The Cloud Connector view is available also for Cloud Foundry regions. It lets you see which Cloud Connectors are connected to a subaccount.

</td>
<td valign="top">

New

</td>
<td valign="top">

2019-04-25

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

Cloud Connector 2.12 - Features

</td>
<td valign="top">

Release of Cloud Connector version 2.12 introduces the following features and enhancements:

-   The administration UI is now accessible not only with an administrator role, but also with a display and a support role. See [Configure Named Cloud Connector Users](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/3859e50f652e4a4b9c66a6a572ced7a4.html) and [Use LDAP for Authentication](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/120ceecfd84145a181ac160d588a7a3d.html).
-   For HTTP access control entries, you can
    -   allow a protocol upgrade, e.g. to WebSockets, for exposed resources. See [Limit the Accessible Services for HTTP\(S\)](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/e7d4927dbb571014af7ef6ebd6cc3511.html#loioe7d4927dbb571014af7ef6ebd6cc3511__limit).
    -   define which host \(virtual or internal\) is sent in the host header.See [Expose Intranet Systems](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/e7d4927dbb571014af7ef6ebd6cc3511.html#loioe7d4927dbb571014af7ef6ebd6cc3511__expose), Step 8.

-   A disaster recovery subaccount in disaster recovery mode can be converted into a standard subaccount, if a disaster recovery region replaces the original region permanently.See [Convert a Disaster Recovery Subaccount into a Standard Subaccount](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/35736580b814412788e0b5b3915cbdc3.html).
-   A service channel overview lets you check at a glance, which server ports are used by a Cloud Connector installation. See [Service Channels: Port Overview](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/449dbf5fd2294f93aafb996a231b3155.html).
-   Important subaccount configuration can be exported, and imported into another subaccount. See [Copy a Subaccount Configuration](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/513d1296750548d9b8c1741cc8954a1d.html).
-   An LDAP authentication configuration check lets you analyze and fix configuration issues before activating the LDAP authentication.See [Use LDAP for Authentication](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/120ceecfd84145a181ac160d588a7a3d.html).
-   You can use different user roles to access the Cloud Connector configuration REST APIs. See [Configuration REST APIs](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/cfb9d579f50b4711a514dc8f08d22f73.html).
-   REST APIs for shadow instance configuration have been added. See [Shadow Instance Configuration](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/2f6f67716d6944919fcdc43c92ceefb8.html).
-   You can define scenarios for resources. Such a scenario can be exported, and imported into other hosts. See [Configure Accessible Resources](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/3b12086100b344d39a2ff0c9410e66c6.html).



</td>
<td valign="top">

New

</td>
<td valign="top">

2019-04-25

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

Cloud Connector 2.12 - Fixes

</td>
<td valign="top">

Release of Cloud Connector version 2.12 provides the following bug fixes:

-   The SAN \(subjectAlternativeName\) usage in certificates can be defined in a better way and is stored correctly in the certificate. See [Exchange UI Certificates in the Administration UI](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/b70bf164a6e6498b8bf1f459554609f5.html).
-   `IllegalArgumentException` does not occur any more in HTTP processing, if the backend closes a connection and data are streamed.
-   DNS caching is now recognized in reconnect situations if the IP of a DNS entry has changed.
-   SNC with load balancing now works correctly for RFC SNC-based access control entries.
-   A master-master situation is also recognized if, at startup of the former master instance, the new master \(the former shadow instance\) is not reachable.
-   Solution management model generation works correctly for a shadow instance.
-   The daemon is started properly on SLES 12 standard installations at system startup.



</td>
<td valign="top">

Changed

</td>
<td valign="top">

2019-04-25

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

Destination Service - Authentication Types

</td>
<td valign="top">

Authentication type `OAuth2SAMLBearerAssertion` provides two different types of `Token Service URL`:

-   `Dedicated`: used in the context of a single tenant, or
-   `Common`: used in the context of multiple tenants.

For type `Common`, the tenant subdomain is automatically set to the target `Token Service URL`.

In addition, cloud applications can use the `x-user-token` HTTP header to propagate the user access token to the external target service at runtime. By default, the user principal is processed via the authorization HTTP header.

See [SAML Bearer Assertion Authentication](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/c69ea6aacd714ad2ae8ceb5fc3ceea56.html).

</td>
<td valign="top">

New

</td>
<td valign="top">

2019-04-11

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

Connectivity Service - Fix

</td>
<td valign="top">

When an on-premise system closed a connection that uses an RFC or SOCKS5 proxy, the Connectivity service kept the connection to the cloud application alive.

This issue has been fixed. The connection is now always closed right after sending the response.

</td>
<td valign="top">

Changed

</td>
<td valign="top">

2019-04-11

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

Connectivity Service - Protocols

</td>
<td valign="top">

The Connectivity service supports TCP connections to on-premise systems, exposing a SOCKS5 proxy to cloud applications. This feature follows the concept of binding the credentials of a Connectivity service instance.

See [Using the TCP Protocol for Cloud Applications](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/cd1583775afa43f0bb9ec69d9dbcc880.html).

</td>
<td valign="top">

New

</td>
<td valign="top">

2019-03-14

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

Connectivity Service - Fix

</td>
<td valign="top">

After receiving an on-premise system response with HTTP header *Connection: close*, the Connectivity service kept the HTTP connection to the cloud application alive.

This issue has been fixed. The connection is now always closed right after sending the response.

</td>
<td valign="top">

Changed

</td>
<td valign="top">

2019-03-14

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

Cloud Connector - Certificate Update

</td>
<td valign="top">

For the Connectivity service \(Neo environment\), **a new, region-specific certificate authority** \(X.509 certificate\) is being introduced.

If you use the Cloud Connector for on-premise connections to the Neo environment, you must import the new certificate authority into your trust configuration.

-   After the **next month** \(concrete notification will be rolled out\), the current certificate authority will no longer be used to issue client certificates for Cloud Connector deployments, and only the new one will be used.

    The Connectivity service will still trust client certificates of Cloud Connector deployments that were already issued.


-   After a **three-month period** \(concrete notification will be rolled out\), that trust will be removed and your Cloud Connector deployment must be configured to use the new client certificates.

See [Update the Certificate for a Subaccount](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/071708a655de4486b498cf5b16fb8ea8.html).

</td>
<td valign="top">

Announcement

</td>
<td valign="top">

2019-02-28

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

Destination Service - Authentication Types

</td>
<td valign="top">

The new authentication type `OAuth2UserTokenExchange` lets your applications use an automated exchange of user access tokens when accessing other applications or services. The feature supports single-tenant and multi-tenant scenarios. See [OAuth User Token Exchange Authentication](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/e3c333f9de6245fca326993f2397c13a.html). 

</td>
<td valign="top">

New

</td>
<td valign="top">

2019-02-14

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

RFC - Stateful Sequences

</td>
<td valign="top">

You can make a stateful sequence of function module invocations work across several request/response cycles. See [Invoking ABAP Function Modules via RFC](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/628bae0298e6451b998127830975a7f3.html#loio628bae0298e6451b998127830975a7f3__restrict). 

</td>
<td valign="top">

Changed

</td>
<td valign="top">

2019-01-31

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

Cloud Connector 2.11.3

</td>
<td valign="top">

A security note for Cloud Connector version 2.11.3 has been issued. See SAP note [2696233](https://me.sap.com/notes/2696233).

</td>
<td valign="top">

Changed

</td>
<td valign="top">

2019-01-15

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

Protocols - RFC Communication

</td>
<td valign="top">

You can use the RFC protocol to set up communication with on-premise ABAP systems for applications in the Cloud Foundry environment.

This feature requires a runtime environment with SAP Java Buildpack version 1.8.0 or higher. See [Invoking ABAP Function Modules via RFC](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/fa4adc9bd40e45dbac573fd616695446.html).

</td>
<td valign="top">

New

</td>
<td valign="top">

2019-01-17

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

Destinations - Renew Certificates

</td>
<td valign="top">

A button in the *Destinations* editor lets you update the validity period of an X.509 certificate. See [Set up Trust Between Systems](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/82dbecae3454493782d16a79e30f1a6d.html). 

</td>
<td valign="top">

New

</td>
<td valign="top">

2019-01-17

</td>
</tr>
</table>

