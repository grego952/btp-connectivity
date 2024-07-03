<!-- loio2959ab89b768444cb2ff870c05c63688 -->

# AuthenticationHeaderProvider API

Use the `AuthenticationHeaderProvider` API for applications to retrieve prepared authentication headers that are ready to be used to towards a remote target system.



<a name="loio2959ab89b768444cb2ff870c05c63688__section_os1_5vf_wpb"/>

## Overview

The `AuthenticationHeaderProvider` API is visible by default from the web applications hosted on *SAP Java Buildpack*. You can access it via a JNDI lookup.

This API lets your applications use their own managed HTTP clients, as it provides them with automated authentication token retrieval, making it easy to implement *single sign-on* \(SSO\) towards the remote target.



<a name="loio2959ab89b768444cb2ff870c05c63688__section_a1h_yvf_wpb"/>

## Procedure

1.  To consume the authentication header provider API using JNDI, you need to define the `AuthenticationHeaderProvider` API as a resource in the *context.xml* file.

    Example of an `AuthenticationHeaderProvider` resource named `myAuthHeaderProvider`, which is described in the *context.xml* file:

    > ### Sample Code:  
    > ```
    > <?xml version='1.0' encoding='utf-8'?>
    >   
    > <Context>
    >     <Resource name="myAuthHeaderProvider" auth="Container"
    >               type="com.sap.core.connectivity.api.authentication.AuthenticationHeaderProvider"
    >               factory="com.sap.core.connectivity.api.jndi.ServiceObjectFactory"/>
    > </Context>
    > ```

2.  In your servlet code, you can look up the `AuthenticationHeaderProvider` API from the JNDI registry as follows:

    > ### Sample Code:  
    > ```
    > import javax.naming.Context;
    > import javax.naming.InitialContext;
    > import com.sap.core.connectivity.api.authentication.AuthenticationHeaderProvider;
    > ...
    >  
    > // look up the connectivity authentication header provider resource called "myAuthHeaderProvider"
    > Context ctx = new InitialContext();
    > AuthenticationHeaderProvider authHeaderProvider = (AuthenticationHeaderProvider) ctx.lookup("java:comp/env/myAuthHeaderProvider");
    > ```




<a name="loio2959ab89b768444cb2ff870c05c63688__section_ft3_zvf_wpb"/>

## Single Sign-On to On-Premise Systems

The Connectivity service supports a mechanism to enable SSO using the so-called *principal propagation* authentication type of a destination configuration. To propagate the logged-in user, the application can use the `AuthenticationHeaderProvider` API to retrieve a prepared HTTP header, which then embeds in the HTTP request to the on-premise system.

**Prerequisites**

To connect to on-premise systems and perform single sign-on, you must bind a Connectivity service instance to the cloud application.

**References**

For more information, see also:

-   [Principal Propagation SSO Authentication for HTTP](principal-propagation-sso-authentication-for-http-73194cc.md)
-   [Create and Bind a Connectivity Service Instance](create-and-bind-a-connectivity-service-instance-a2b88cf.md)
-   [Consuming the Connectivity Service (Java)](https://help.sap.com/viewer/b865ed651e414196b39f8922db2122c7/Cloud/en-US/e5c9867dbb571014957ef9d7a8846b1c.html "Connect your Java cloud applications to the Internet, make cloud-to-on-premise connections to SAP or non-SAP systems, or send and fetch e-mail.") :arrow_upper_right: \(Neo environment\)

**Example**

> ### Sample Code:  
> ```
> String proxyHost = <connectivity_service_credentials_onPremiseProxyHost>;
> int proxyPort = Integer.parseInt(<connectivity_service_credentials_onPremiseProxyPort>);
> String account = SecurityContext.getAccessToken().getZoneId();
>  
> // setup the on-premise HTTP proxy
> HttpClient httpClient = new DefaultHttpClient();
> httpClient.getParams().setParameter(ConnRoutePNames.DEFAULT_PROXY, new HttpHost(proxyHost, proxyPort));
>    
> // look up the connectivity authentication header provider resource called "authHeaderProvider" (must be defined in web.xml)
> Context ctx = new InitialContext();
> AuthenticationHeaderProvider authHeaderProvider = (AuthenticationHeaderProvider) ctx.lookup("java:comp/env/authHeaderProvider");
>    
> // get header for principal propagation
> AuthenticationHeader principalPropagationHeader = authHeaderProvider.getPrincipalPropagationHeader();
>    
> //insert the necessary headers in the request
> HttpGet request = new HttpGet("http://virtualhost:1234");
> request.addHeader(principalPropagationHeader.getName(), principalPropagationHeader.getValue());
>    
> // execute the request
> HttpResponse response = httpClient.execute(request);
> ```



<a name="loio2959ab89b768444cb2ff870c05c63688__section_gt3_zvf_wpb"/>

## OAuth2 SAML Bearer Assertion

The Destination service provides support for applications to use the SAML Bearer assertion flow for consuming OAuth-protected resources. In this way, applications do not need to deal with some of the complexities of OAuth and can reuse user data from existing identity providers.

Users are authenticated by using a SAML assertion against the configured and trusted OAuth token service. The SAML assertion is then used to request an access token from an OAuth token service. This access token is returned by the API and can be injected in the HTTP request to access the remote OAuth-protected resources via SSO.

> ### Tip:  
> Тhe access tokens are cached by `AuthenticationHeaderProvider` and are auto-updated: When a token is about to expire, a new token is created shortly before the expiration of the old one.

The `AuthenticationHeaderProvider` API provides the following method to retrieve such headers:

```
List<AuthenticationHeader> getOAuth2SAMLBearerAssertionHeaders(DestinationConfiguration destinationConfiguration);

```

For more information, see also [Principal Propagation SSO Authentication for HTTP](principal-propagation-sso-authentication-for-http-73194cc.md).



<a name="loio2959ab89b768444cb2ff870c05c63688__section_hm4_zvf_wpb"/>

## Client Credentials

The Destination service provides support for applications to use the OAuth client credentials flow for consuming OAuth-protected resources.

The client credentials are used to request an access token from an OAuth token service.

> ### Tip:  
> Тhe access tokens are cached by `AuthenticationHeaderProvider` and are auto-updated: When a token is about to expire, a new token is created shortly before the expiration of the old one.

The `AuthenticationHeaderProvider` API provides the following method to retrieve such headers:

```
AuthenticationHeader getOAuth2ClientCredentialsHeader (DestinationConfiguration destinationConfiguration);
```

For more information, see:

-   [Principal Propagation SSO Authentication for HTTP](principal-propagation-sso-authentication-for-http-73194cc.md)
-   [OAuth SAML Bearer Assertion Authentication](oauth-saml-bearer-assertion-authentication-c69ea6a.md)
-   [OAuth Client Credentials Authentication](oauth-client-credentials-authentication-4e1d742.md)

**Related Information**  


[Principal Propagation](principal-propagation-e2cbb48.md "Enable single sign-on (SSO) by forwarding the identity of cloud users to a remote system or service.")

