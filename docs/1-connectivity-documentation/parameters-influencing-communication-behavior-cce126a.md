<!-- loiocce126a22e7b462fac6d4de58551e238 -->

# Parameters Influencing Communication Behavior

JCo properties that allow you to control the connection to an ABAP system.

All properties are optional.


<table>
<tr>
<th valign="top">

Property

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

`jco.client.trace`

</td>
<td valign="top">

Defines whether protocol traces are created. Valid values are `1` \(trace is on\) and `0` \(trace is off\). The default value is `0`.

</td>
</tr>
<tr>
<td valign="top">

`jco.client.codepage`

</td>
<td valign="top">

Declares the 4-digit SAP codepage that is used when initiating the connection to the backend. The default value is `1100` \(comparable to iso-8859-1\). It is important to provide this property if the password that is used contains characters that cannot be represented in `1100`.

</td>
</tr>
<tr>
<td valign="top">

`jco.client.delta`

</td>
<td valign="top">

Enables or disables table parameter delta management. It is enabled if set to `1`, and respectively disabled if set to `0`. The default value is `1`.

</td>
</tr>
<tr>
<td valign="top">

`jco.client.cloud_connector_version`

</td>
<td valign="top">

Defines the Cloud Connector version used for establishing a connection to the on-premise system. The default value is `2`. Currently, no other values are supported.

</td>
</tr>
<tr>
<td valign="top">

`jco.client.cloud_connector_location_id`

</td>
<td valign="top">

You can connect multiple Cloud Connectors to a subaccount as long as their location ID is different. The location ID specifies the Cloud Connector over which the connection is opened. The default value is an empty string identifying the Cloud Connector that is connected without any location ID.

> ### Note:  
> When working with the *Destinations* editor in the cockpit, enter the Cloud Connector location ID in the *<Location ID\>* field. Do not enter it as additional property.



</td>
</tr>
<tr>
<td valign="top">

`jco.client.serialization_format`

</td>
<td valign="top">

Defines the serialization format that is used when transferring function module data to the partner system. The property impacts the serialization behavior of function module data. Valid values are `columnBased` and `rowBased`. If you choose `columnBased`, the *fast RFC serialization* is used, as long as the partner system supports it, see SAP Note [2372888](https://me.sap.com/notes/2372888). When choosing the `rowBased` option, *classic* or *basXML* serialization are used. The default value is `rowBased`.

</td>
</tr>
<tr>
<td valign="top">

`jco.client.network`

</td>
<td valign="top">

Defines which network type is expected to be used for the destination.The property impacts the serialization behavior of function module data, see SAP Note [2372888](https://me.sap.com/notes/2372888). Valid values are `WAN` and `LAN`. The default value is `LAN`.

</td>
</tr>
</table>

