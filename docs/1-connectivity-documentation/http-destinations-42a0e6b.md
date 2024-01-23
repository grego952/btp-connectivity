<!-- loio42a0e6b966924f2e902090bdf435e1b2 -->

# HTTP Destinations

Find information about HTTP destinations for Internet and on-premise connections\(Cloud Foundry environment\).



<a name="loio42a0e6b966924f2e902090bdf435e1b2__section_N10024_N10011_N10001"/>

## Destination Levels

The runtime tries to resolve a destination in the order: *Subaccount Level* → *Service Instance Level*.



<a name="loio42a0e6b966924f2e902090bdf435e1b2__section_ojj_f1p_slb"/>

## Destinations for Subscribed Applications

In subscription-based scenarios, it is not always possible to consume a service instance by binding it to your application. In this case, you must create a destination pointing to your service instance. For more information, see [Destinations Pointing to Service Instances](destinations-pointing-to-service-instances-685f383.md).



<a name="loio42a0e6b966924f2e902090bdf435e1b2__section_34CAB926317746379CFEDF0DC89F0242"/>

## Proxy Types

The proxy types supported by the Connectivity service are:

-   **Internet** - The application can connect to an external REST or SOAP service on the Internet.
-   **OnPremise** - The application can connect to an on-premise back-end system through the Cloud Connector.

The proxy type used for a destination is specified by the destination property `ProxyType`. The default value is `Internet`.



<a name="loio42a0e6b966924f2e902090bdf435e1b2__section_38788239B8A74BBA8024B6F5CE821225"/>

## Proxy Settings for Your Local Runtime

If you work in your local development environment behind a proxy server and want to use a service from the Internet, you need to configure your proxy settings on JVM level. To do this, proceed as follows:

1.  On the *Servers* view, double-click the added server and choose *Overview* to open the editor.
2.  Click the *Open Launch Configuration* link.
3.  Choose the *\(x\)=Arguments* tab page.
4.  In the *VM Arguments* box, add the following row:

    ```
    
    -Dhttp.proxyHost=yourproxyHost -Dhttp.proxyPort=yourProxyPort -Dhttps.proxyHost=yourproxyHost -Dhttps.proxyPort=yourProxyPort
    
    ```

5.  Choose *OK*.
6.  Start or restart your SAP HANA Cloud local runtime.





<a name="loio42a0e6b966924f2e902090bdf435e1b2__config"/>

## Configuring Authentication

When creating an HTTP destination, you can use different authentication types for access control:

-   [Server Certificate Authentication](server-certificate-authentication-e75d7f1.md)

-   [Principal Propagation SSO Authentication for HTTP](principal-propagation-sso-authentication-for-http-73194cc.md)

-   [OAuth SAML Bearer Assertion Authentication](oauth-saml-bearer-assertion-authentication-c69ea6a.md)

-   [Client Authentication Types for HTTP Destinations](client-authentication-types-for-http-destinations-4e13a04.md)

-   [OAuth Client Credentials Authentication](oauth-client-credentials-authentication-4e1d742.md)

-   [OAuth User Token Exchange Authentication](oauth-user-token-exchange-authentication-e3c333f.md)
-   [OAuth Password Authentication](oauth-password-authentication-452357c.md)
-   [OAuth JWT Bearer Authentication](oauth-jwt-bearer-authentication-283cd2d.md)
-   [SAML Assertion Authentication](saml-assertion-authentication-d81e168.md)
-   [OAuth with X.509 Client Certificates](oauth-with-x-509-client-certificates-2c162aa.md)
-   [OAuth Refresh Token Authentication](oauth-refresh-token-authentication-bff0136.md)
-   [OAuth Authorization Code Authentication](oauth-authorization-code-authentication-9f634f6.md)
-   [OAuth Technical User Propagation Authentication](oauth-technical-user-propagation-authentication-8634e21.md)
-   [Using Client Assertion with OAuth Flows](using-client-assertion-with-oauth-flows-789acee.md)



<a name="loio42a0e6b966924f2e902090bdf435e1b2__section_fgp_jxc_cvb"/>

## Custom Query Parameters and Headers

For most of these authentication types, you can add custom query parameters and headers to the URL of a destination. For more information, see the details of the respective authentication type.

**Related Information**  


[OAuth with X.509 Client Certificates](oauth-with-x-509-client-certificates-2c162aa.md "Use an X.509 certificate instead of a secret to authenticate against the authentication server.")

[Create HTTP Destinations](create-http-destinations-783fa1c.md "Create HTTP destinations in the Destinations editor (SAP BTP cockpit).")

