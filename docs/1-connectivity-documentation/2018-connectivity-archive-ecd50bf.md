<!-- loioecd50bf9f78046c99ea4dff7a34de068 -->

# 2018 Connectivity \(Archive\)





**2018**


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

Integration

</td>
<td valign="top">

Neo

</td>
<td valign="top">

Connectivity Service - Performance

</td>
<td valign="top">

A change in the SAP Cloud Platform Connectivity service improves performance of data upload \(on-premise to cloud\) and data download \(cloud to on-premise\) up to 4 times and 15-30 times respectively.

</td>
<td valign="top">

Changed

</td>
<td valign="top">

2018-12-20

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration

</td>
<td valign="top">

Neo

</td>
<td valign="top">

Connectivity Service - Resilience

</td>
<td valign="top">

The Connectivity service has a better protection against zombie connections, which improves resilience and overall availability for the cloud applications consuming it.

</td>
<td valign="top">

Changed

</td>
<td valign="top">

2018-12-20

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration

</td>
<td valign="top">

Neo

</td>
<td valign="top">

Password Storage Service

</td>
<td valign="top">

A Password Storage REST API is available in the SAP API Business Hub, see [Password Storage \(Neo Environment\)](https://api.sap.com/api/SCP_PasswordStorage/resource).

</td>
<td valign="top">

New

</td>
<td valign="top">

2018-12-06

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration

</td>
<td valign="top">

Neo

</td>
<td valign="top">

Destination Configuration Service

</td>
<td valign="top">

A [Destination Configuration service REST API](https://api.sap.com/package/scpconnectivity?section=Artifacts) is available in the SAP API Business Hub.

</td>
<td valign="top">

New

</td>
<td valign="top">

2018-12-06

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration

</td>
<td valign="top">

Cloud Foundry

</td>
<td valign="top">

Destination Service

</td>
<td valign="top">

A [Destination service REST API](https://api.sap.com/package/scpconnectivity?section=Artifacts) is available in the SAP API Business Hub.

</td>
<td valign="top">

New

</td>
<td valign="top">

2018-12-06

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration

</td>
<td valign="top">

Neo

</td>
<td valign="top">

JCo Runtime for SAP Cloud Platform - Fixes

</td>
<td valign="top">

-   When using `JCoRecord.fromJSON()` for a structure parameter, the data is now always sent to the backend system. Also, you do not need to append the number of provided rows for table parameters before parsing the JSON document any more.
-   Depending on the configuration of certain JCo properties, an internally managed connection pool could throw a `JCoException` \(error group `JCO_ERROR_RESOURCE)`. In a thread waiting for a free connection from this pool, an error message then erroneously reported that the pool was exhausted .

    This error situation could occur if the used destination was not configured with the property `jco.destination.max_get_client_time` set to 0 and the destination's `jco.destination.peak_limit` value was set higher than the `jco.destination.pool_capacity`.

    This issue has been fixed.




</td>
<td valign="top">

Changed

</td>
<td valign="top">

2018-12-06

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration

</td>
<td valign="top">

Neo

</td>
<td valign="top">

JCo Runtime for SAP Cloud Platform - Features

</td>
<td valign="top">

Support of the RFC fast serialization. Depending on the exchanged parameter and data types, the performance improvements for RFC communication can reach multiple factors.

See SAP note [2372888](https://me.sap.com/notes/2372888) \(prerequisites\) and [Parameters Influencing Communication Behavior](https://help.sap.com/viewer/b865ed651e414196b39f8922db2122c7/Cloud/en-US/9d768240af6446049cf90d47dc798b8d.html "JCo properties that allow you to control the connection to an ABAP system.") :arrow_upper_right: \(JCo configuration in SAP Cloud Platform\).

</td>
<td valign="top">

Changed

</td>
<td valign="top">

2018-12-06

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration

</td>
<td valign="top">

Neo

</td>
<td valign="top">

JCo Runtime for SAP Cloud Platform - Information

</td>
<td valign="top">

Local runtimes on Windows must install the VS 2013 redistributables for x64, instead of VS 2010.

</td>
<td valign="top">

Changed

</td>
<td valign="top">

2018-12-06

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration

</td>
<td valign="top">

-   Neo
-   Cloud Foundry



</td>
<td valign="top">

Cloud Connector Fixes

</td>
<td valign="top">

Release of Cloud Connector 2.11.3:

-   An issue in RFC communication could cause the trace entry *com.sap.scc.jni.CpicCommunicationException: no SAP ErrInfo available* when the network is slow. This issue has been fixed.
-   The Windows service no longer runs in *error 1067* when stopped by an administrator.
-   In previous releases, the connection between a shadow and a master instance occasionally failed at startup and produced an empty error message. This issue has been fixed.
-   The Cloud Connector does not cache Kerberos tokens in the protocol handler any more, as they are one-time tokens and cannot be reused.
-   For HTTP access control entries, you can configure resources containing a *\#* character.



</td>
<td valign="top">

Changed

</td>
<td valign="top">

2018-12-06

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration

</td>
<td valign="top">

-   Neo
-   Cloud Foundry



</td>
<td valign="top">

Cloud Connector Enhancements

</td>
<td valign="top">

Release of Cloud Connector 2.11.3:

-   If the user *sapadm* exists on a system, the installation on Linux assigns it to the *sccgroup*, which is a prerequisite for solution management integration to work properly, see [Configure Solution Management Integration](configure-solution-management-integration-3a058a2.md).
-   Restoring a backup has been improved.See [Configuration Backup](configuration-backup-abd1ba7.md).
-   The HTTP session store size has been reduced. You can handle higher loads with a given heap size.
-   Cipher suite configuration has been improved. Also, there is a new security status entry for cipher suites, see [Recommendations for Secure Setup](recommendations-for-secure-setup-e7ea82a.md).



</td>
<td valign="top">

Changed

</td>
<td valign="top">

2018-12-06

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration

</td>
<td valign="top">

Neo

</td>
<td valign="top">

HTTP Destinations

</td>
<td valign="top">

The *OAuth2 Client Credentials* grant type is supported by the *Destinations* editor in the SAP Cloud Platform cockpit as well as by the client Java APIs `ConnectivityConfiguration`, `AuthenticationHeaderProvider` and `HttpDestination`, available in SAP Cloud Platform Neo runtimes.

See [OAuth Client Credentials Authentication](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/7aefa21a65f94b25b7e639c3931b6f83.html).

</td>
<td valign="top">

Changed

</td>
<td valign="top">

2018-10-11

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration

</td>
<td valign="top">

Cloud Foundry

</td>
<td valign="top">

User Propagation

</td>
<td valign="top">

The connectivity service supports the SaaS application subscription flow and can be declared as a dependency in the get dependencies subscription callback, also via MTA \(multi-target\)-bundled applications.

See [Consuming the Connectivity Service \(Cloud Foundry Environment\)](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/313b215066a8400db461b311e01bd99b.html) and [Configure Principal Propagation via User Exchange Token \(Cloud Foundry Environment\)](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/39f538ad62e144c58c056ebc34bb6890.html).

</td>
<td valign="top">

Changed

</td>
<td valign="top">

2018-09-27

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration

</td>
<td valign="top">

-   Neo
-   Cloud Foundry



</td>
<td valign="top">

Cloud Connector

2.11.2

</td>
<td valign="top">

Release of Cloud Connector 2.11.2

-   SNC configuration now provides the value of the environment variable `SECUDIR`, which you need for the usage of the SAP Cryptographic Library \(SAPCRYPTOLIB\). See [Initial Configuration \(RFC\)](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/f09eefe71d1e4d4484e1dd4b121585fb.html).
-   On Linux, the RPM \(Red Hat Package Manager\) now ensures that the configuration of the interaction with the SAP Host Agent \(used for the Solution Manager integration\) is adjusted. See [Configure Solution Management Integration](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/3a058a25a0f0487eb5b8d2d0df8e9426.html).
-   The Cloud Connector shadow instance now provides a configuration option for the connection and request timeout that may occur during health check against the master instance. See [Master and Shadow Administration](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/7f57de170fbd4405ab485880772af1f1.html).



</td>
<td valign="top">

Changed

</td>
<td valign="top">

2018-08-16

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration

</td>
<td valign="top">

-   Neo
-   Cloud Foundry



</td>
<td valign="top">

Cloud Connector 2.11.2

</td>
<td valign="top">

Fixes of Cloud Connector 2.11.2

-   In a high availability setup, the switch from the master instance to the shadow instance occasionally caused communication errors towards on-premise systems. This issue has now been fixed.
-   You can now import multiple certificates with the same subject to the trust store. Details about expiration date and issuer are displayed in the tool tip. See [Set Up Trust](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/a4ee70f0274248f8bbc7594179ef948d.html#loioa4ee70f0274248f8bbc7594179ef948d__section_TrustStore), section *Trust Store*.
-   You can now configure also the MOC \(Multiple Origin Composition\) OData service paths as resources.
-   The `Location` header is now adjusted correctly according to your access control settings in case of a redirect.
-   Principal propagation now also works with SAML assertions that contain an empty attribute element.
-   SAP Cloud Platform applications occasionally got an HTTP 500 \(internal server error\) response when an HTTP connection was closed. The applications are now always informed properly.



</td>
<td valign="top">

Changed

</td>
<td valign="top">

2018-08-16

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Integration

</td>
<td valign="top">

Neo

</td>
<td valign="top">

HttpDestination Library

</td>
<td valign="top">

The SAP `HttpDestination` library \(available in the SDK and cloud runtime "Java EE 6 Web Profile"\) now creates Apache `HttpClient` instances which work with strict SNI \(Server Name Indication\) servers.

Use cases with strict SNI configuration on the server side will no longer get the error message *Failure reason: "peer not authenticated"*, that was raised either at runtime or while performing a connection test via the SAP Cloud Platform cockpit *Destinations* editor \(*Check Connection* function\).

</td>
<td valign="top">

Changed

</td>
<td valign="top">

2018-08-16

</td>
</tr>
</table>

