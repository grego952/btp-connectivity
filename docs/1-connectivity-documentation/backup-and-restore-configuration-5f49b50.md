<!-- loio5f49b505710844ad8c29e9b6a4a524dc -->

# Backup And Restore Configuration

> ### Sample Code:  
> ```
> package com.sap.scc.examples
> import com.github.kittinunf.fuel.Fuel
> import com.github.kittinunf.fuel.core.BlobDataPart
> import com.github.kittinunf.fuel.core.FuelManager
> import com.github.kittinunf.fuel.core.Headers
> import com.github.kittinunf.fuel.core.Method
> import com.github.kittinunf.fuel.core.extensions.authentication
> import com.github.kittinunf.result.Result
> import java.io.ByteArrayInputStream
> import java.io.File
> /*
>  This example shows how to use REST APIs to perform the Backup and Restore of the Cloud Connector configuration.
>  As a prerequisite you have a stable Cloud Connector configuration and you want to save the backup for later use.
>  
>  The configuration details can be found in scenario.json.
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
>     //Create the backup configuration of the cloud connector "master".
>     Fuel.post("${config.master!!.url}/api/v1/configuration/backup")
>         .header(Headers.CONTENT_TYPE, "application/json")
>         .authentication().basic(config.master!!.user, config.master!!.password)
>         .body("""{"password":"my-very-secret-password"}""")
>         .response { _, _, result ->
>             when (result) {
>                 is Result.Failure -> processRequestError(result.error)
>                 is Result.Success -> File("backup.zip").writeBytes(result.get())
>             }
>         }
>         .join()
>     //Restore the backup configuration if some fatal accidental changes should be reverted
>     val formData = listOf("password" to "my-very-secret-password")
>     Fuel.upload("${config.master!!.url}/api/v1/configuration/backup", Method.PUT, formData)
>         .add(BlobDataPart(ByteArrayInputStream(File("backup.zip").readBytes()), name = "backup"))
>         .authentication().basic(config.master!!.user, config.master!!.password)
>         .response { _, _, result ->
>             when (result) {
>                 is Result.Failure -> processRequestError(result.error)
>                 is Result.Success -> println("Backup configuration successfully restored in (${config.master!!.url}) ")
>             }
>         }
>         .join()
> }
> ```

