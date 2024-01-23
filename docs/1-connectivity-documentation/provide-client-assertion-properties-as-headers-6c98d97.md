<!-- loio6c98d97155434f94a47597c04ab37737 -->

# Provide Client Assertion Properties as Headers

Provide client assertion properties as headers when using client assertion with OAuth flows for a destination.

You can provide the following headers to use client assertion authentication:


<table>
<tr>
<th valign="top">

Header

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

`X-client-assertion-type`

</td>
<td valign="top">

Absolute URI

</td>
<td valign="top">

Format of the assertion as defined by the authorization server. The value is an absolute URI. A URN of the form *urn:ietf:params:oauth:client-assertion-type:\** is suggested.

Examples:

-   "urn:ietf:params:oauth:client-assertion-type:saml2-bearer" =\> indicating a SAML Bearer assertion.
-   "urn:ietf:params:oauth:client-assertion-type:jwt-bearer" =\> indicating a JWT Bearer token.



</td>
</tr>
<tr>
<td valign="top">

`X-client-assertion`

</td>
<td valign="top">

Token

</td>
<td valign="top">

Assertion being used to authenticate the client.

</td>
</tr>
</table>



<a name="loio6c98d97155434f94a47597c04ab37737__section_hmw_c1l_cxb"/>

## Example: Destination for an OAuth Service Accepting Client Assertion instead of Client Secret

> ### Sample Code:  
> ```
> Name=sap_Destination
> Type=HTTP
> URL= https://xxxx.example.com
> ProxyType=Internet
> Authentication=OAuth2ClientCredentials
> clientId=clientId
> tokenServiceURL=https://authserver.example.com/oauth/token/
> ```



<a name="loio6c98d97155434f94a47597c04ab37737__section_uwj_c1l_cxb"/>

## Example: Client Assertion Properties as Headers

To use the client assertion mechanism in the *Find Destination* API, you must add two mandatory headers as shown in the following example:

> ### Sample Code:  
> ```
> curl --location --request GET 'https://<destination_service_host>/destination-configuration/v1/destinations/<destination-name>' \
> --header 'X-client-assertion-type: urn:ietf:params:oauth:client-assertion-type:jwt-bearer' \ # mandatory parameter
> --header 'X-client-assertion: eyJraWQiOiJKMWpC...' \ # mandatory parameter
> --header 'Authorization: Bearer <access_token>'
> ```

