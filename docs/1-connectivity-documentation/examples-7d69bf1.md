<!-- loio7d69bf1f457a45ad81b566e40fa9f4ac -->

# Examples

Find examples on how to use the Cloud Connector's configuration REST APIs.



<a name="loio7d69bf1f457a45ad81b566e40fa9f4ac__concept"/>

## Concept

The sample code in this section \([download](https://help.sap.com/doc/2cd0051606354018b1050fbc0eb297f0/Cloud/en-US/REST%20API%20Examples.zip) zip file\) demonstrates how to use the REST APIs provided by Cloud Connector to perform various configuration tasks.

Starting with a freshly installed Cloud Connector, the samples include initial configuration of the Cloud Connector instance, connectivity setup, high availability configuration, and common tasks like backup/restore operations, as well as integration with solution management.

The examples are implemented in *Kotlin*, a simple Java VM-based language. However, even if you are using a different language, they still show the basic use of the APIs and their parameters for specific configuration purposes.

If you are not familiar with Kotlin, find a brief introduction and some typical statements below.

[REST API Parameters](examples-7d69bf1.md#loio7d69bf1f457a45ad81b566e40fa9f4ac__parameters)

[REST API Invocation](examples-7d69bf1.md#loio7d69bf1f457a45ad81b566e40fa9f4ac__invocation)

[How To Use the Examples](examples-7d69bf1.md#loio7d69bf1f457a45ad81b566e40fa9f4ac__examples)



<a name="loio7d69bf1f457a45ad81b566e40fa9f4ac__parameters"/>

## REST API Parameters

In almost all requests and responses, structures are encoded in JSON format. To describe the parameter details, we use Kotlin data classes.

This class represents a structure that you can use as value in a request or response:

```
data class OnlyPropertiesNamesAreRelevant(
    val user: String, 
    val password: String
)
```

The JSON representation for that class is

```
{"user":<userValue>, "password":<passwordValue>}

```

Encoded in Kotlin this string looks like

```
"""{"user":"$userValue", "password":"$passwordValue"}""" 

```

or as an object:

```
val credentials = OnlyPropertiesNamesAreRelevant(userValue, passwordValue)

```

Back to [Concept](examples-7d69bf1.md#loio7d69bf1f457a45ad81b566e40fa9f4ac__concept)



<a name="loio7d69bf1f457a45ad81b566e40fa9f4ac__invocation"/>

## REST API Invocation

```
(a)	Fuel.put(url)
(b)     .header("Connection", "close")
(c)		.authentication().basic(user, password)
(d)		.jsonBody(credentials)
(e)		.responseObject<OnlyPropertiesNamesAreRelevant> { _, _, result ->
			when (result) {
(f)				is Result.Failure -> processRequestError(result.error)
				is Result.Success -> println("returned: ${result.get()}")
			}
		}
		.join()
```

-   \(a\) - *Fuel* is an HTTP framework used in the examples. Important is the verb after *Fuel* - it is the REST API method.
-   \(b\) - Adds a request header `Connection: close`, which forces a connection close after request. In the examples, this header is defined on *FuelManager* for all calls.
-   \(c\) - Basic authentication is used for the call with user and password.
-   \(d\) - HTTP requests with parameters require mostly JSON. The `jsonBody`-method adds the header `Content-Type: application/json` and serializes the provided object credentials to JSON. Requests without body like *DELETE* or *GET* omit body methods.
-   \(e\) - The `responseObject<ClassType>`-method adds the header `Accept: application/json` and de-serializes the response to the specified class type. Some APIs do not have any response or non-JSON response. In such cases, the method `response` is used instead of `responseObject<ClassType>`.
-   \(f\) - The way, how Kotlin decides between success \(2xx\) and failed responses. For details on the possible response status, see [Configuration REST APIs](configuration-rest-apis-cfb9d57.md).

Back to [Concept](examples-7d69bf1.md#loio7d69bf1f457a45ad81b566e40fa9f4ac__concept)



<a name="loio7d69bf1f457a45ad81b566e40fa9f4ac__examples"/>

## How To Use the Examples

Some common details, used by different examples, were extracted to the `scenario.json` configuration file. This lets you use meaningful names like `config.master!!.user` in the examples. The file is loaded by

```
val config = loadScenarioConfiguration()
```

Each example also invokes

```
disableTrustChecks()
```

This method disables all SSL-related checks.

> ### Caution:  
> `disableTrustChecks()` is only used for test purposes. *Do not* use it in a productive environment.

Both methods, as well as some common REST API parameter structures \(data classes\) are defined in the file [Scenario Configuration](scenario-configuration-a827186.md). This is the only help class under `sources/`.

When using the examples, start with [Initial Configuration](initial-configuration-83bab3a.md).

Prerequisite is a freshly installed Cloud Connector.

After a mandatory password change and defining the high availability role of the Cloud Connector instance \(master or shadow\), the example demonstrates how to provide a description for the instance and how to set up the UI and system certificates.

Once the initial configuration is done, you can optionally proceed with these steps:

-   Connect to your subaccount on BTP \([Subaccount Configuration](subaccount-configuration-276c756.md)\)
-   Create or restore a configuration backup \([Backup And Restore Configuration](backup-and-restore-configuration-5f49b50.md)\)
-   Configure and connect high availability instances \([High Availability Settings](high-availability-settings-2559f8f.md)\)
-   Integrate the Cloud Connector with the solution management infrastructure \([Solution Management Integration](solution-management-integration-1dfef61.md)\)

Back to [Concept](examples-7d69bf1.md#loio7d69bf1f457a45ad81b566e40fa9f4ac__concept)

**Related Information**  


[scenario.json](scenario-json-540b396.md "")

[Source Files](source-files-80f8da8.md "")

