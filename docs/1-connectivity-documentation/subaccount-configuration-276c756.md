<!-- loio276c756da5b14d82b8e410ef9d445cec -->

# Subaccount Configuration

> ### Sample Code:  
> ```
> package com.sap.scc.examples
> import com.github.kittinunf.fuel.Fuel
> import com.github.kittinunf.fuel.core.FuelManager
> import com.github.kittinunf.fuel.core.extensions.authentication
> import com.github.kittinunf.fuel.gson.jsonBody
> import com.github.kittinunf.fuel.gson.responseObject
> import com.github.kittinunf.result.Result
> /*
>  This example shows how to use REST APIs to configure and connect a subaccount in cloud connector.
>  The example begins with (1) connecting of the subaccount, then we create a system (2) for an HTTP service
>  and (3) for an RFC service.
>  
>  The configuration details for master and shadow instances can be found in scenario.json.
>  */
> fun main() {
>     //Cloud Connector distribution generates only an untrusted self-signed certificate.
>     //So for this demonstration use case we need to deactivate all trust checks.
>     disableTrustChecks()
>     //Use 'Connection: close' header, to make stateless communication more efficient
>     FuelManager.instance.baseHeaders = mapOf("Connection" to "close")
>     //Add output of cURL commands for revision
>     //FuelManager.instance.addRequestInterceptor(LogRequestAsCurlInterceptor)
>     //1.1. Create and connect subaccount
>     //Load configuration from property file
>     val config = loadScenarioConfiguration()
>     //Some cloud regions require 2-Factor-Authentication
>     println("Enter MFA (aka 2FA) token, if required: ")
>     var token = readLine() ?: ""
>     //Parameters required to establish the connection to the subaccount (aka the secure tunnel)
>     var subaccountCreateData = SubaccountConfiguration(
>         config.subaccount!!.regionHost, config.subaccount!!.subaccount,
>         config.subaccount!!.user, "" + config.subaccount!!.password + token, locationId = config.subaccount!!.locationId
>     )
>     //Optional: Initialize the map to work with generated _links
>     //If you don't like to use _links, you can easily compute the entity links
>     var subaccountLinks: Map<String, HalLink> = mapOf()
>     Fuel.post("${config.master!!.url}/api/v1/configuration/subaccounts")
>         .authentication().basic(config.master!!.user, config.master!!.password)
>         .jsonBody(subaccountCreateData)
>         .responseObject<SubaccountInfo> { _, response, result ->
>             when (result) {
>                 is Result.Success -> {
>                     val subaccountLocation = response.header("Location").first()
>                     println("1.1. subaccount was created under: $subaccountLocation")
>                     println("subaccount: ${result.get()} ")
>                     //GET details as SubaccountInfo every time possible by invoking
>                     //https://<SCC>/api/v1/configuration/subaccounts/<regionHost>/<subaccountId>
>                     subaccountLinks = result.get()._links
>                 }
>                 is Result.Failure -> processRequestError(result.error)
>             }
>         }
>         .join()
>     //1.2. From time to time it is necessary to extend the validity of the subaccount - refresh subaccount
>     //Again some cloud landscapes require 2-Factor-Authentication
>     println("Enter MFA (aka 2FA) token for refresh, if required: ")
>     token = readLine() ?: ""
>     Fuel.post(subaccountLinks["validity"]!!.href)
>         .authentication().basic(config.master!!.user, config.master!!.password)
>         .jsonBody(SubaccountRefreshCred(config.subaccount!!.user, "" + config.subaccount!!.password + token))
>         .responseObject<SubaccountInfo> { _, _, result ->
>             when (result) {
>                 is Result.Success -> println("1.2. validity of the subaccount was extended")
>                 is Result.Failure -> processRequestError(result.error)
>             }
>         }
>         .join()
>     //2.1. Create a system mapping (aka access control) for an HTTP service
>     val httpSystem = SystemMapping(
>         "virtual.host", "vport", "local", "lport", CommunicationProtocol.HTTPS,
>         BackendType.abapSys, hostInHeader = HostInHeader.INTERNAL
>     )
>     var httpSystemLinks: Map<String, HalLink> = mapOf()
>     Fuel.post(subaccountLinks["systemMappings"]!!.href)
>         .authentication().basic(config.master!!.user, config.master!!.password)
>         .jsonBody(httpSystem)
>         .responseString { _, response, result ->
>             when (result) {
>                 is Result.Success -> {
>                     val httpSystemMappingLocation = response.header("Location").first()
>                     println("2.1. system mapping was created under: $httpSystemMappingLocation")
>                     //GET the details about the system mapping by invoking
>                     //https://<SCC>/api/v1/configuration/subaccounts/<regionHost>/<subaccountId>/systemMappings/<vhost>:<vport>
>                     Fuel.get(httpSystemMappingLocation)
>                         .authentication().basic(config.master!!.user, config.master!!.password)
>                         .responseObject<SystemMapping> { _, _, result ->
>                             when (result) {
>                                 is Result.Success -> {
>                                     println("system mapping: ${result.get()}")
>                                     httpSystemLinks = result.get()._links
>                                 }
>                                 is Result.Failure -> processRequestError(result.error)
>                             }
>                         }
>                         .join()
>                 }
>                 is Result.Failure -> processRequestError(result.error)
>             }
>         }
>         .join()
>     //2.2 Add an allowed resource to the system mapping. Since this system mapping points to an HTTP service, use HTTP resource parameters
>     Fuel.post(httpSystemLinks["resources"]!!.href)
>         .authentication().basic(config.master!!.user, config.master!!.password)
>         .jsonBody(HttpResource("/", exactMatchOnly = false))
>         .responseString { _, response, result ->
>             when (result) {
>                 is Result.Success -> {
>                     val httpResourceLocation = response.header("Location").first()
>                     println("2.2. http resource was created under: $httpResourceLocation")
>                     //GET the details about the resource by invoking
>                     //https://<SCC>/api/v1/configuration/subaccounts/<regionHost>/<subaccountId>/systemMappings/<vhost>:<vport>/<encoded-id>
>                     //<encoded-id> -> replace '/' with '-'
>                     Fuel.get(httpResourceLocation)
>                         .authentication().basic(config.master!!.user, config.master!!.password)
>                         .responseObject<HttpResource> { _, _, result ->
>                             when (result) {
>                                 is Result.Success -> println("http resource: ${result.get()}")
>                                 is Result.Failure -> processRequestError(result.error)
>                             }
>                         }
>                         .join()
>                 }
>                 is Result.Failure -> processRequestError(result.error)
>             }
>         }
>         .join()
>     //3.1 Create a system mapping for an RFC service
>     var rfcSystemLinks: Map<String, HalLink> = mapOf()
>     Fuel.post(subaccountLinks["systemMappings"]!!.href)
>         .authentication().basic(config.master!!.user, config.master!!.password)
>         .jsonBody(
>             SystemMapping(
>                 "virtual.host",
>                 "rfcport",
>                 "local",
>                 "rfcport",
>                 CommunicationProtocol.RFCS,
>                 BackendType.abapSys
>             )
>         )
>         .responseString { _, response, result ->
>             when (result) {
>                 is Result.Success -> {
>                     val rfcSystemMappingLocation = response.header("Location").first()
>                     println("3.1. system mapping was created under: $rfcSystemMappingLocation")
>                     //GET the details about the system mapping by invoking
>                     //https://<SCC>/api/v1/configuration/subaccounts/<regionHost>/<subaccountId>/systemMappings/<vhost>:<vport>
>                     Fuel.get(rfcSystemMappingLocation)
>                         .authentication().basic(config.master!!.user, config.master!!.password)
>                         .responseObject<SystemMapping> { _, _, result ->
>                             when (result) {
>                                 is Result.Success -> {
>                                     println("system mapping: ${result.get()}")
>                                     rfcSystemLinks = result.get()._links
>                                 }
>                                 is Result.Failure -> processRequestError(result.error)
>                             }
>                         }
>                         .join()
>                 }
>                 is Result.Failure -> processRequestError(result.error)
>             }
>         }
>         .join()
>     //3.2 Now add the function module RFC_SYSTEM_INFO as an allowed resource to the system mapping
>     val rfcResource = RfcResource("RFC_SYSTEM_INFO")
>     Fuel.post(rfcSystemLinks["resources"]!!.href)
>         .authentication().basic(config.master!!.user, config.master!!.password)
>         .jsonBody(rfcResource)
>         .responseString { _, response, result ->
>             when (result) {
>                 is Result.Success -> {
>                     val resourceLocation = response.header("Location").first()
>                     println("3.2. rfc resource was created under: $resourceLocation")
>                     //GET the details about the resource by invoking
>                     //https://<SCC>/api/v1/configuration/subaccounts/<regionHost>/<subaccountId>/systemMappings/<vhost>:<vport>/<encoded-id>
>                     //<encoded-id> -> replace '/' with '-'
>                     Fuel.get(resourceLocation)
>                         .authentication().basic(config.master!!.user, config.master!!.password)
>                         .responseObject<RfcResource> { _, _, result ->
>                             when (result) {
>                                 is Result.Success -> println("rfc resource: ${result.get()}")
>                                 is Result.Failure -> processRequestError(result.error)
>                             }
>                         }
>                         .join()
>                 }
>                 is Result.Failure -> processRequestError(result.error)
>             }
>         }
>         .join()
> }
> //Data structures used by REST calls in this scenario
> //Nullable properties are optional
> data class SubaccountConfiguration(
>     var regionHost: String,
>     var subaccount: String,
>     var cloudUser: String,
>     var cloudPassword: String,
>     var displayName: String? = null,
>     var locationId: String? = null
> )
> data class SubaccountInfo(
>     val displayName: String,
>     val regionHost: String,
>     val subaccount: String,
>     val tunnel: SubaccountTunnelInfo,
>     val user: String,
>     val _links: Map<String, HalLink>
> )
> data class SubaccountTunnelInfo(
>     val state: String, //Connected
>     val connectedSince: String, //timestamp formatted with client locale
>     val connections: Int,
>     val applicationConnections: List<String>,
>     val serviceChannels: List<String>,
>     val subaccountCertificate: X509CertificateInfo,
>     )
> data class X509CertificateInfo(
>     val notAfter: String,
>     val notBefore: String,
>     val subjectDN: String,
>     val issuer: String
> )
> data class HalLink(val href: String)
> data class SubaccountRefreshCred(
>     var cloudUser: String,
>     var cloudPassword: String
> )
> data class SystemMapping(
>     val virtualHost: String,
>     val virtualPort: String,
>     val localHost: String,
>     val localPort: String,
>     val protocol: CommunicationProtocol,
>     val backendType: BackendType,
>     val sncPartnerName: String? = null,
>     val hostInHeader: HostInHeader? = null,
>     val sapRouter: String? = null,
>     val authenticationMode: AuthenticationMode = AuthenticationMode.NONE,
>     val description: String = "",
> ) {
>     val _links: Map<String, HalLink> = mapOf()
> }
> enum class CommunicationProtocol {
>     HTTP, HTTPS, RFC, RFCS, LDAP, LDAPS, TCP, TCPS
> }
> enum class BackendType {
>     abapSys, netweaverCE, applServerJava, BC, PI, hana, netweaverGW, otherSAPsys, nonSAPsys
> }
> enum class HostInHeader {
>     INTERNAL, VIRTUAL
> }
> enum class AuthenticationMode {
>     NONE, X509_CERTIFICATE, X509_CERTIFICATE_LOCAL, KERBEROS
> }
> data class HttpResource(
>     val id: String, //URI path
>     val enabled: Boolean = true,
>     val exactMatchOnly: Boolean = true,
>     val webSocketUpgradeAllowed: Boolean = true,
>     val description: String = ""
> )
> data class RfcResource(
>     val id: String, //Function module or prefix for function module
>     val enabled: Boolean = true,
>     val exactMatchOnly: Boolean = true,
>     val description: String = ""
> )
> 
> ```

