<!-- loio83bab3a3ed124d788b856a10764f36b0 -->

# Initial Configuration

> ### Sample Code:  
> ```
> package com.sap.scc.examples
> //import com.sap.scc.examples.SccCertificate
> import com.github.kittinunf.fuel.Fuel
> import com.github.kittinunf.fuel.core.BlobDataPart
> import com.github.kittinunf.fuel.core.FuelManager
> import com.github.kittinunf.fuel.core.Method
> import com.github.kittinunf.fuel.core.extensions.authentication
> import com.github.kittinunf.fuel.gson.responseObject
> import com.github.kittinunf.result.Result
> import java.io.ByteArrayInputStream
> import java.io.File
> /*
>  This example shows how to use REST APIs to perform the initial configuration of a master instance
>  after installing and starting the Cloud Connector.
>  As a prerequisite you need to install and start the Cloud Connector.
>  The example begins with changing the initial password, setting the instance to the master role, edit the description,
>  and upload UI and system certificates.
>  For the certificates used by Cloud Connector in order to access the UI and for the system certificate used to access backend systems,
>  we simply upload the already available PKCS#12 certificates uiCert.p12 and systemCert.p12 encrypted with the password "test1234".
>  Cloud Connector also provides other options for certificate management, please take a look at the documentation.
>  The configuration details for master and shadow instances can be found in scenario.json.
>  */
> fun main() {
> 	//Cloud Connector distribution generates only an untrusted self-signed certificate.
> 	//So for this demonstration use case we need to deactivate all trust checks.
> 	disableTrustChecks()
> 	//Use 'Connection: close' header, to make stateless communication more efficient
> 	FuelManager.instance.baseHeaders = mapOf("Connection" to "close")
> 	//Add output of cURL commands for revision
> 	//FuelManager.instance.addRequestInterceptor(LogRequestAsCurlInterceptor)
> 	//Load configuration from property file
> 	val config = loadScenarioConfiguration()
> 	//Change the initial password
> 	Fuel.put("${config.master!!.url}/api/v1/configuration/connector/authentication/basic")
> 		.authentication().basic(config.master!!.user, "manage")
> 		.body("""{"oldPassword":"manage", "newPassword":"${config.master!!.password}"}""")
> 		.response { _, _, result ->
> 			when (result) {
> 				is Result.Failure -> processRequestError(result.error)
> 				is Result.Success -> println("Password successfully set to ${config.master!!.password}")
> 			}
> 		}
> 		.join()
> 	//Set the High-Availability Role to master, use "shadow" if you want to set it to shadow
> 	Fuel.put("${config.master!!.url}/api/v1/configuration/connector/haRole")
> 		.authentication().basic(config.master!!.user, config.master!!.password)
> 		.body("master")
> 		.response { _, _, result ->
> 			when (result) {
> 				is Result.Failure -> processRequestError(result.error)
> 				is Result.Success -> println("high-availability role successfully set to 'master'")
> 			}
> 		}
> 		.join()
> 	//Edit Common Description
> 	Fuel.put("${config.master!!.url}/api/v1/configuration/connector")
> 		.authentication().basic(config.master!!.user, config.master!!.password)
> 		.body("""{"description":"<description of Cloud Connector instance>"}""")
> 		.responseObject<SccDescriptionResponse> { _, _, result ->
> 			when (result) {
> 				is Result.Failure -> processRequestError(result.error)
> 				is Result.Success -> println(result.get())
> 			}
> 		}
> 		.join()
> 	//Upload a PKCS#12 Certificate as UI Certificate
> 	val uiCertificateFormData = listOf("password" to "test1234", "keyPassword" to "test1234")
> 	Fuel.upload(
> 		"${config.master!!.url}/api/v1/configuration/connector/ui/uiCertificate",
> 		Method.PUT,
> 		uiCertificateFormData
> 	)
> 		.add(BlobDataPart(ByteArrayInputStream(File("uiCert.p12").readBytes()), name = "pkcs12"))
> 		.authentication().basic(config.master!!.user, config.master!!.password)
> 		.response { _, _, result ->
> 			when (result) {
> 				is Result.Failure -> processRequestError(result.error)
> 				is Result.Success -> println("PKCS#12 Certificate 'uiCert.p12'  successfully uploaded")
> 			}
> 		}
> 		.join()
> 	//Upload a PKCS#12 Certificate as as System Certificate
> 	val systemCertificateFormData = listOf("password" to "test1234", "keyPassword" to "test1234")
> 	Fuel.upload(
> 		"${config.master!!.url}/api/v1/configuration/connector/onPremise/systemCertificate",
> 		Method.PUT,
> 		systemCertificateFormData
> 	)
> 		.add(BlobDataPart(ByteArrayInputStream(File("systemCert.p12").readBytes()), name = "pkcs12"))
> 		.authentication().basic(config.master!!.user, config.master!!.password)
> 		.response { _, _, result ->
> 			when (result) {
> 				is Result.Failure -> processRequestError(result.error)
> 				is Result.Success -> println("PKCS#12 Certificate 'systemCert.p12'  successfully uploaded")
> 			}
> 		}
> 		.join()
> }
> //Data structures used by REST calls in this scenario
> data class SccDescriptionResponse(
> 	var role: String,
> 	var description: String
> )
> ```

