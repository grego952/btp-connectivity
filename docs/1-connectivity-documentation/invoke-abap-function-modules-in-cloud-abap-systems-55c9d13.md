<!-- loio55c9d13251dd451caac129594ac6dd68 -->

# Invoke ABAP Function Modules in Cloud ABAP Systems

Call a function module in a cloud ABAP system via RFC, using a sample Web application.

This scenario performs a remote function call to invoke an ABAP function module, by using the Destination service in the Cloud Foundry environment, as well as a Cloud Foundry application router.

> ### Note:  
> For more information on invoking ABAP function modules via WebSocket RFC in SAP BTP, ABAP environment, see tutorial [WebSocket RFC to Cloud](https://developers.sap.com/tutorials/abap-websocket-rfc.html).



<a name="loio55c9d13251dd451caac129594ac6dd68__tasks_tutorial_rfc"/>

## Tasks


<table>
<tr>
<th valign="top">

Task Type

</th>
<th valign="top">

Task

</th>
</tr>
<tr>
<td valign="top" rowspan="4">

![](images/CS_TASK_Admin_Dev_7c2c6d8.png)

Operator and/or Developer

</td>
<td valign="top">

[Scenario Overview](invoke-abap-function-modules-in-cloud-abap-systems-55c9d13.md#loio55c9d13251dd451caac129594ac6dd68__Scenario) 

</td>
</tr>
<tr>
<td valign="top">

[Used Values](invoke-abap-function-modules-in-cloud-abap-systems-55c9d13.md#loio55c9d13251dd451caac129594ac6dd68__values) 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity User Roles](invoke-abap-function-modules-in-cloud-abap-systems-55c9d13.md#loio55c9d13251dd451caac129594ac6dd68__Roles) 

</td>
</tr>
<tr>
<td valign="top">

[Installation Prerequisites](invoke-abap-function-modules-in-cloud-abap-systems-55c9d13.md#loio55c9d13251dd451caac129594ac6dd68__Install) 

</td>
</tr>
<tr>
<td valign="top">

![](images/CS_TASK_Dev_a4c82d5.png)

Developer

</td>
<td valign="top">

[Develop a Sample Web Application](develop-a-sample-web-application-a799669.md) 

</td>
</tr>
<tr>
<td valign="top">

![](images/CS_TASK_Admin_Dev_7c2c6d8.png)

Operator and/or Developer

</td>
<td valign="top">

[Create and Bind Service Instances](create-and-bind-service-instances-67a42bb.md) 

</td>
</tr>
<tr>
<td valign="top">

![](images/CS_TASK_Dev_a4c82d5.png)

Developer

</td>
<td valign="top">

[Deploy the Application](deploy-the-application-3ab2b13.md) 

</td>
</tr>
<tr>
<td valign="top">

![](images/CS_TASK_Admin_219b363.png)

Operator

</td>
<td valign="top">

[Configure Roles and Trust](configure-roles-and-trust-a6ce7e7.md) 

</td>
</tr>
<tr>
<td valign="top">

![](images/CS_TASK_Admin_Dev_7c2c6d8.png)

Operator and/or Developer

</td>
<td valign="top">

[Set Up an Application Router](set-up-an-application-router-f9f8eb2.md) 

</td>
</tr>
<tr>
<td valign="top">

![](images/CS_TASK_Admin_219b363.png)

Operator

</td>
<td valign="top">

[Configure the RFC Destination](configure-the-rfc-destination-cfd3fea.md) 

</td>
</tr>
<tr>
<td valign="top">

![](images/CS_TASK_Admin_Dev_7c2c6d8.png)

Operator and/or Developer

</td>
<td valign="top">

[Monitoring Your Web Application](monitoring-your-web-application-9bd8f7d.md) \(Optional\)

</td>
</tr>
</table>



<a name="loio55c9d13251dd451caac129594ac6dd68__Scenario"/>

## Scenario Overview

**Control Flow for Using the Java Connector \(JCo\) with Basic Authentication**

![](images/CS_CF_RFC_Tutorial_-_Scenario_CLOUD_68db916.png)

**Process Steps:**

1.  Call through AppRouter \(entry point for business applications\).

    > ### Note:  
    > AppRouter is only required you want to use multitenancy or perform user-specific service calls. In all other cases, JCo uses [cloud-security-xsuaa-integration](https://github.com/SAP/cloud-security-xsuaa-integration/tree/master/token-client) with `ClientCredentialFlow`.

2.  Redirect to XSUAA for login. JSON Web Token \(JWT1\) is sent to AppRouter and cached there.
3.  AppRouter calls Web app and sends JWT1 with credentials.
4.  Buildpack/XSUAA interaction: Buildpack requests JWT2 to access the Destination service instance \(JCo call\).
5.  Buildpack requests destination configuration \(JWT2\).
6.  Buildpack sends request to the cloud ABAP system \(with JWT2 and Authorization Header\).

Since token exchanges are handled by the buildpack, you must only create and bind the service instances, see [Create and Bind Service Instances](create-and-bind-service-instances-6dd5e26.md).

Back to [Tasks](invoke-abap-function-modules-in-cloud-abap-systems-55c9d13.md#loio55c9d13251dd451caac129594ac6dd68__tasks_tutorial_rfc)



<a name="loio55c9d13251dd451caac129594ac6dd68__values"/>

## Used Values

This scenario uses:

-   A subaccount in region `Europe (Frankfurt)`, for which the API endpoint is `api.cf.eu10.hana.ondemand.com`.
-   The application name `jco-demo-<subaccount name>`, where *<subaccount name\>* is the subdomain name of the subaccount. For this example, we use `p1234`.

Back to [Tasks](invoke-abap-function-modules-in-cloud-abap-systems-55c9d13.md#loio55c9d13251dd451caac129594ac6dd68__tasks_tutorial_rfc)



<a name="loio55c9d13251dd451caac129594ac6dd68__Roles"/>

## Connectivity User Roles

Different user roles are involved in the cloud-to-cloud connectivity scenario. The particular steps for the relevant roles are described below:

**Application Developer**

Develops Web applications using destinations. Scenario steps:

1.  Installs Eclipse IDE, the Cloud Foundry Plugin for Eclipse and the Cloud Foundry CLI.
2.  Develops a Java EE application using the JCo APIs.
3.  Configures connectivity destinations via the SAP BTP cockpit.
4.  Deploys and tests the Java EE application on SAP BTP.

**Account Operator**

Deploys Web applications, creates application routers, creates and binds service instances, conducts tests. Scenario steps:

1.  Obtains a ready Java EE application WAR file.
2.  Deploys an application router with respective routes to the application.
3.  Creates an XSUAA service instance and binds it to the router.
4.  Deploys the Java EE application to an SAP BTP subaccount.
5.  Creates a Destination service instance, and binds it to the application.
6.  Creates and manages roles and role collections.

Back to [Tasks](invoke-abap-function-modules-in-cloud-abap-systems-55c9d13.md#loio55c9d13251dd451caac129594ac6dd68__tasks_tutorial_rfc)



<a name="loio55c9d13251dd451caac129594ac6dd68__Install"/>

## Installation Prerequisites

-   You have downloaded and set up your Eclipse IDE and the [Eclipse Tools for Cloud Foundry](https://projects.eclipse.org/projects/ecd.cft).
-   You have downloaded the Cloud Foundry CLI, see [Tools](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/abcae5b568c94e5391a74d15f5db9213.html "SAP BTP includes many tools to help you develop and manage applications, and connect them to your on-premise systems.") :arrow_upper_right:.

Back to [Tasks](invoke-abap-function-modules-in-cloud-abap-systems-55c9d13.md#loio55c9d13251dd451caac129594ac6dd68__tasks_tutorial_rfc)



<a name="loio55c9d13251dd451caac129594ac6dd68__section_xsy_nkc_cgb"/>

## Next Steps

-   [Develop a Sample Web Application](develop-a-sample-web-application-a799669.md)
-   [Create and Bind Service Instances](create-and-bind-service-instances-67a42bb.md)
-   [Deploy the Application](deploy-the-application-3ab2b13.md)
-   [Configure Roles and Trust](configure-roles-and-trust-a6ce7e7.md)
-   [Set Up an Application Router](set-up-an-application-router-f9f8eb2.md)
-   [Configure the RFC Destination](configure-the-rfc-destination-cfd3fea.md)
-   [Monitoring Your Web Application](monitoring-your-web-application-9bd8f7d.md) \(Optional\)

**Related Information**  


[Multitenancy for JCo Applications \(Advanced\)](multitenancy-for-jco-applications-advanced-93c1e03.md "Learn about the required steps to make your JCo application tenant-aware.")

