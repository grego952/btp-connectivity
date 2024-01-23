<!-- loio1dfef61d37fe4c36937a73d018232c48 -->

# Solution Management Integration

> ### Sample Code:  
> ```
> package com.sap.scc.examples
> import com.github.kittinunf.fuel.Fuel
> import com.github.kittinunf.fuel.core.FuelManager
> import com.github.kittinunf.fuel.core.extensions.authentication
> import com.github.kittinunf.fuel.gson.jsonBody
> import com.github.kittinunf.fuel.gson.responseObject
> import com.github.kittinunf.result.Result
> import java.io.File
> /*
>  This example shows how to use REST APIs to configure the integration with SAP solution management.
>  In most cases it should be only necessary to pass a boolean flag in order to enable or
>  disable solution management integration. It is expected that SAP host agent is already
>  installed on the host as prerequisite for solution management integration.
>  
>  This example executes requests against master and shadow instances. 
>  The shadow instance is optional. Ignore the requests to shadow instance if there is only
>  a master instance in your environment.
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
>     //First we check the current configuration of solution management
>     Fuel.get("${config.master!!.url}/api/v1/configuration/connector/solutionManagement")
>         .authentication().basic(config.master!!.user, config.master!!.password)
>         .responseObject<SolutionManagementConfiguration> { _, _, result ->
>             when (result) {
>                 is Result.Success -> println("response: ${result.get()}")
>                 is Result.Failure -> processRequestError(result.error)
>             }
>         }
>         .join()
>     //Configure the hostAgent path on the shadow instance
>     //Invoking this API on a shadow instance changes only the configuration.
>     //Only when invoking it on a master instance it also activates solution management integration.
>     //Note: This step is not required if host agent is installed at the default location
>     Fuel.post("${config.shadow!!.url}/api/v1/configuration/connector/solutionManagement")
>         .authentication().basic(config.shadow!!.user, config.shadow!!.password)
>         .jsonBody(SolutionManagementConfiguration(hostAgentPath = "/path/to/hostAgent"))
>         .response { _, _, result ->
>             when (result) {
>                 is Result.Success -> println("new path to host agent was set")
>                 is Result.Failure -> processRequestError(result.error)
>             }
>         }
>         .join()
>     //Turns on the solution management integration.
>     //Note: this operation is possible only on the master instance.
>     //In case of an HA setup, the flag enabled is propagated to the shadow automatically.
>     //Note: optionally you can set here the new path for host agent and enable DSR.
>     Fuel.post("${config.master!!.url}/api/v1/configuration/connector/solutionManagement")
>         .authentication().basic(config.master!!.user, config.master!!.password)
>         .jsonBody(SolutionManagementConfiguration())
>         .response { _, _, result ->
>             when (result) {
>                 is Result.Success -> println("solution management is activated")
>                 is Result.Failure -> processRequestError(result.error)
>             }
>         }
>         .join()
>     //Turns off the solution management integration.
>     //Note: this operation is possible only on the master instance.
>     //In case of an HA setup, the flag not enabled is propagated to the shadow automatically
>     Fuel.delete("${config.master!!.url}/api/v1/configuration/connector/solutionManagement")
>         .authentication().basic(config.master!!.user, config.master!!.password)
>         .response { _, _, result ->
>             when (result) {
>                 is Result.Success -> println("solution management is deactivated")
>                 is Result.Failure -> processRequestError(result.error)
>             }
>         }
>         .join()
>     //Registration file with LMDB model can be downloaded by following request.
>     //This file can be used for a manual upload to solution management.
>     //If solution management integration is active,the updates are triggered by configuration changes automatically.
>     Fuel.get("${config.master!!.url}/api/v1/configuration/connector/solutionManagement/registrationFile")
>         .authentication().basic(config.master!!.user, config.master!!.password)
>         .response { _, _, result ->
>             when (result) {
>                 is Result.Success -> File("lmdbModel.zip").writeBytes(result.get())
>                 is Result.Failure -> processRequestError(result.error)
>             }
>         }
>         .join()
> }
> //Data structures used by REST calls in this scenario
> //Nullable properties are optional
> data class SolutionManagementConfiguration(
>     var hostAgentPath: String? = null,
>     var enabled: Boolean? = null,
>     var dsrEnabled: Boolean? = null
> )
> ```

