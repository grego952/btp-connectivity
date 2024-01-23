<!-- loioa8271863020a4b9483419c46d2fbe018 -->

# Scenario Configuration

> ### Sample Code:  
> ```
> package com.sap.scc.examples
> import com.github.kittinunf.fuel.core.FuelError
> import com.google.gson.Gson
> import java.io.File
> import java.security.SecureRandom
> import java.security.cert.X509Certificate
> import javax.net.ssl.*
> data class CloudConnector(
> 	val url: String,
> 	var user: String,
> 	var password: String
> )
> fun disableTrustChecks() {
> 	try {
> 		HttpsURLConnection.setDefaultHostnameVerifier { hostname: String, session: SSLSession -> true }
> 		val context: SSLContext = SSLContext.getInstance("TLS")
> 		val trustAll: X509TrustManager = object : X509TrustManager {
> 			override fun checkClientTrusted(chain: Array<X509Certificate>, authType: String) {}
> 			override fun checkServerTrusted(chain: Array<X509Certificate>, authType: String) {}
> 			override fun getAcceptedIssuers(): Array<X509Certificate> {
> 				return arrayOf()
> 			}
> 		}
> 		context.init(null, arrayOf(trustAll), SecureRandom())
> 		HttpsURLConnection.setDefaultSSLSocketFactory(context.socketFactory)
> 	} catch (e: Exception) {
> 		e.printStackTrace()
> 	}
> }
> class ScenarioConfiguration {
> 	var subaccount: SubaccountParameters? = null
> 	var master: CloudConnector? = null
> 	var shadow: CloudConnector? = null
> }
> data class SubaccountParameters(
> 	val regionHost: String,
> 	val subaccount: String,
> 	val user: String,
> 	val password: String,
> 	var locationId: String? = null
> )
> data class SccCertificate(
> 	var subjectDN: String? = null,
> 	var issuer: String? = null,
> 	var notAfter: String? = null,
> 	var notBefore: String? = null,
> 	var subjectAltNames: List<SubjectAltName>? = null
> )
> data class SubjectAltName(
> 	var type: String? = null,
> 	var value: String? = null
> )
> internal fun loadScenarioConfiguration(): ScenarioConfiguration {
> 	println("scenario.json will be loaded from ${File("scenario.json").absolutePath}")
> 	return Gson().fromJson(File("scenario.json").readText(), ScenarioConfiguration::class.java)
> }
> internal fun processRequestError(error: FuelError) {
> 	println("failed with ${error.message} ${String(error.errorData)}")
> 	throw RuntimeException("Stop here. ")
> }
> ```

