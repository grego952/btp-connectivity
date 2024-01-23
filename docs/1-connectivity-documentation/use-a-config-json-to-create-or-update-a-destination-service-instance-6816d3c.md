<!-- loio6816d3caeb464f8d8b0d1b5ad0da5869 -->

# Use a Config.JSON to Create or Update a Destination Service Instance

Configure specific parameters in a `config.json` file to create or update a Destination service instance.

When creating or updating a Destination service instance, you can configure the following settings, which are part of the `config.json` input file \(see [Open Service Broker API](https://www.openservicebrokerapi.org/)\), both via SAP BTP cockpit or Cloud Foundry command line interface \(CLI\):


<table>
<tr>
<th valign="top">

Parameter

</th>
<th valign="top">

Value

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

`init_data`

</td>
<td valign="top">

JSON

</td>
<td valign="top">

The data \(destinations, certificates\) to initialise or update the service instance with. The data can be stored on both *service instance* data and *subaccount* data.

</td>
</tr>
<tr>
<td valign="top">

`HTML5Runtime_enabled`

</td>
<td valign="top">

Boolean

</td>
<td valign="top">

Indicates whether the SAP BTP HTML5 runtime should be enabled to work with the service instance on behalf of the HTML5 applications associated with it during deployment.

</td>
</tr>
</table>

Find the `config.json` structure below:

> ### Sample Code:  
> ```
> {
>     "HTML5Runtime_enabled" : "true",
>     "init_data" : {
>         "subaccount" : {
>             "existing_destinations_policy": "update|fail|ignore",
>             "existing_certificates_policy": "update|fail|ignore",
>             "destinations" : [
>                 {
>                     ...
>                 }
>             ],
>             "certificates" : [
>                 {
>                     ...
>                 }
>             ]
>         },
>         "instance" : {
>             "existing_destinations_policy": "update|fail|ignore",
>             "existing_certificates_policy": "update|fail|ignore",
>             "destinations" : [
>                 {
>                     ...
>                 }
>             ],
>             "certificates" : [
>                 {
>                     ...
>                 } 
>             ]
>         }
>     }
> }
> ```

**Related Information**  


[HTTP Destinations](http-destinations-42a0e6b.md "Find information about HTTP destinations for Internet and on-premise connections (Cloud Foundry environment).")

