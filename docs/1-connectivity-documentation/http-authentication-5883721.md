<!-- loio5883721a1add44fbb385f812ad788d7c -->

# HTTP Authentication

HTTP authentication for the transparent proxy for Kubernetes.

The transparent proxy enriches your request by adding the credentials configured in the destination configuration. Depending on the configured authentication type, the transparent proxy propagates them via an `Authorization` or `SAP-Connectivity-Authentication` header. For more information, see [Configuring Authentication](http-destinations-42a0e6b.md#loio42a0e6b966924f2e902090bdf435e1b2__config).



<a name="loio5883721a1add44fbb385f812ad788d7c__section_h2y_kzf_rtb"/>

## HTTP Authentication Types

-   For all authentication types, except **ClientCertificateAuthentication**, the transparent proxy enriches the request by adding the necessary `Authorization` header to the request \(extracting the `authTokens` section from the Destination service response\).

    For more information on the fields in `authTokens`, see ["Find Destination" Response Structure](find-destination-response-structure-83a3f3b.md).


-   For the authentication types **BasicAuthentication**, **OAuth2TechnicalUserPropagation**, **OAuth2ClientCredentials**, and **OAuth2Password**, no additional `Authorization` headers have to be provided to the transparent proxy as all necessary data for authorization is present in the destination.



-   For the authentication types **OAuth2UserTokenExchange**, **OAuth2JWTBearer**, and **OAuth2SAMLBearerAssertion**, the cloud user identity must be passed to the transparent proxy as a token represented by a JSON Web token \(JWT\) via the `Authorization` header of scheme *Bearer*.

    The token is passed as an `X-User-Token` to the Destination service, which will return `authTokens`. They are processed by the transparent proxy and attached to the HTTP request as `Authorization` header.

-   For authentication type **OAuth2AuthorizationCode**, the code from the authorization service must be passed to the transparent proxy via `Authorization` header of scheme *Bearer*. You can also pass the optional headers `X-redirect-uri` and `X-code-verifier` to the request. The same can be configured in the destination.

    If any or both of the headers are present in the request as well as in the destination configuration, the transparent proxy uses the request headers with priority.

    For more information, see [OAuth Authorization Code Authentication](oauth-authorization-code-authentication-9f634f6.md).

-   For authentication type **OAuth2RefreshToken**, a refresh token must be passed to the transparent proxy via **Authorization** header of scheme *Bearer*.

    For more information, see [OAuth Refresh Token Authentication](oauth-refresh-token-authentication-bff0136.md).


*Client Assertion*

Client assertion OAuth flows are supported, and the transparent proxy propagates the required headers to the Destination service. For more information, see: [Using Client Assertion with OAuth Flows](using-client-assertion-with-oauth-flows-789acee.md).

*ClientCertificateAuthentication* 

> ### Note:  
> For general information, see [ClientCertificateAuthentication](client-authentication-types-for-http-destinations-4e13a04.md#loio4e13a04147314e8e9e54321f25d93fdc__clientCert).

For this authentication type, the transparent proxy manages the client certificate addition \(client certificates and CA certificates\) by getting them from the destination and adding them to the HTTP client that is used to establish the communication between client and server.



Limitations for usage:

-   Supported cert store types are `p12`, `pfx`, `pem`, `der`, `cer`, `crt`.
-   Only `RSA pkcs1` keys \(starting with header RSA PRIVATE KEY and having headers with encryption information\) are currently supported for decryption from *pem* format. The following encryption algorithms are supported:

    -   DES-CBC
    -   DES-EDE3-CBC
    -   AES-128-CBC
    -   AES-192-CBC
    -   AES-256-CBC

    All key types should be supported if no encryption is present.

-   `KeyStore.Source=ClientProvided` is not supported as the transparent proxy can manage only certificates stored in the Destination service.


*Principal Propagation*

Principal propagation, also known as user propagation, lets you perform single sign-on \(SSO\) of the cloud user towards an on-premise system.

The cloud user's identity is passed to the transparent proxy as a token represented by a JSON Web token \(JWT\) via `Authorization` header of scheme `Bearer`. It is forwarded via the transparent proxy to the connectivity proxy and then to the Cloud Connector, which validates and further processes it to establish SSO with the on-premise system. The user is propagated via `SAP-Connectivity-Authentication` header.

For more information, see [Authenticating Users against On-Premise Systems](authenticating-users-against-on-premise-systems-b643fbe.md) and [Set Up Trust](set-up-trust-a4ee70f.md).

*Managed Namespaces Mode*

The transparent proxy can operate in all namespaces in the cluster or only in namespaces labeled in the following way: *transparent-proxy.connectivity.api.sap/namespace:<namespace where Transparent Proxy is installed\>*.

For this feature, you can set the Helm property `config.managedNamespacesMode` to "all" or "labelSelector". The default value is "all". It means that the proxy operates with destination custom resources across all namespaces in the cluster.

For more information, see [Configuration Guide](configuration-guide-2a22cd7.md).

