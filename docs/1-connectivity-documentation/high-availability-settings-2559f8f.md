<!-- loio2559f8f925b24146915892c67a096d93 -->

# High Availability Settings

> ### Sample Code:  
> ```
> package com.sap.scc.examples
> import com.github.kittinunf.fuel.Fuel
> import com.github.kittinunf.fuel.core.FuelManager
> import com.github.kittinunf.fuel.core.Headers
> import com.github.kittinunf.fuel.core.extensions.authentication
> import com.github.kittinunf.fuel.gson.jsonBody
> import com.github.kittinunf.fuel.gson.responseObject
> import com.github.kittinunf.result.Result
> import java.net.URL
> /*
>  This example shows how to use REST APIs to change high availability settings of the Cloud Connector instances.
>  As a prerequisite you need to install and start a shadow and a master instance.
>  Afterwards perform the initial configuration of the master instance (see InitialConfiguration.kt).
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
>     //Load configuration from property file
>     val config = loadScenarioConfiguration()
>     //The high-availability role 'master' in Cloud Connector instance 'master' is already set in the initial configuration.
>     //Set the high-availability role to 'shadow' in Cloud Connector instance 'shadow'
>     Fuel.put("${config.shadow!!.url}/api/v1/configuration/connector/haRole")
>         .authentication().basic(config.shadow!!.user, config.shadow!!.password)
>         .body("shadow")
>         .response { _, _, result ->
>             when (result) {
>                 is Result.Failure -> processRequestError(result.error)
>                 is Result.Success -> println("high-availability role successfully set to 'shadow'")
>             }
>         }
>         .join()
>     //Enable HA in the master instance and define the allowed shadow hosts
>     Fuel.put("${config.master!!.url}/api/v1/configuration/connector/ha/master/config")
>         .header(Headers.CONTENT_TYPE, "application/json")
>         .authentication().basic(config.master!!.user, config.master!!.password)
>         .body("""{"haEnabled":"true", "allowedShadowHost":"${URL(config.shadow!!.url).host}"}""")
>         .responseObject<HAMasterConfiguration> { _, _, result ->
>             when (result) {
>                 is Result.Failure -> processRequestError(result.error)
>                 is Result.Success -> {
>                     val masterConfig = result.get()
>                     println("Master configuration: $masterConfig ")
>                 }
>             }
>         }
>         .join()
>     //The configuration of the shadow instance
>     var shadowConfig: HAShadowConfiguration? = null
>     //Get the current configuration
>     Fuel.get("${config.shadow!!.url}/api/v1/configuration/connector/ha/shadow/config")
>         .authentication().basic(config.shadow!!.user, config.shadow!!.password)
>         .responseObject<HAShadowConfiguration> { _, _, result ->
>             when (result) {
>                 is Result.Failure -> processRequestError(result.error)
>                 is Result.Success -> shadowConfig = result.get()
>             }
>         }
>         .join()
>     //Edit the retrieved configuration and set it
>     shadowConfig!!.masterPort = "${URL(config.master!!.url).port}"
>     shadowConfig!!.masterHost = URL(config.master!!.url).host
>     shadowConfig!!.ownHost = URL(config.master!!.url).host
>     Fuel.put("${config.shadow!!.url}/api/v1/configuration/connector/ha/shadow/config")
>         .authentication().basic(config.shadow!!.user, config.shadow!!.password)
>         .jsonBody(shadowConfig!!)
>         .responseObject<HAShadowConfiguration> { _, _, result ->
>             when (result) {
>                 is Result.Failure -> processRequestError(result.error)
>                 is Result.Success -> shadowConfig = result.get()
>             }
>         }
>         .join()
>     //Set the HA link of both cloud connector instances to 'CONNECT'
>     Fuel.post("${config.shadow!!.url}/api/v1/configuration/connector/ha/shadow/state")
>         .header(Headers.CONTENT_TYPE, "application/json")
>         .authentication().basic(config.shadow!!.user, config.shadow!!.password)
>         .body("""{"op":"CONNECT", "user":"${config.master!!.user}", "password":"${config.master!!.password}"}""")
>         .response { _, _, result ->
>             when (result) {
>                 is Result.Failure -> processRequestError(result.error)
>                 is Result.Success -> println("Master (${config.master!!.url}) and shadow (${config.shadow!!.url}) successfully connected")
>             }
>         }
>         .join()
> }
> //Data structures used by REST calls in this scenario
> //Structure used  to read the high availability settings for a Cloud Connector master instance
> data class HAMasterConfiguration(
>     var haEnabled: Boolean? = null,
>     var allowedShadowHost: String? = null
> )
> //Structure used  to read and edit the high availability settings for a Cloud Connector shadow instance
> data class HAShadowConfiguration(
>     var masterPort: String,
>     var masterHost: String,
>     var ownHost: String? = null,
>     var checkIntervalInSeconds: Int?,
>     var takeoverDelayInSeconds: Int?,
>     var connectTimeoutInMillis: Int?,
>     var requestTimeoutInMillis: Int?
> )
> ```

