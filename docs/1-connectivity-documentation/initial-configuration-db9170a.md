<!-- loiodb9170a7d97610148537d5a84bf79ba2 -->

# Initial Configuration

After installing and starting the Cloud Connector, log on to the administration UI and perform the required configuration to make your Cloud Connector operational.



<a name="loiodb9170a7d97610148537d5a84bf79ba2__context"/>

## Tasks

[Prerequisites](initial-configuration-db9170a.md#loiodb9170a7d97610148537d5a84bf79ba2__prereq)

[Log on to the Cloud Connector](initial-configuration-db9170a.md#loiodb9170a7d97610148537d5a84bf79ba2__log_in)

[Initial Setup](initial-configuration-db9170a.md#loiodb9170a7d97610148537d5a84bf79ba2__change_password)

[Set up Connection Parameters and HTTPS Proxy](initial-configuration-db9170a.md#loiodb9170a7d97610148537d5a84bf79ba2__configure_proxy)

[Establish Connections to SAP BTP](initial-configuration-db9170a.md#loiodb9170a7d97610148537d5a84bf79ba2__establish_cloud_conection)



<a name="loiodb9170a7d97610148537d5a84bf79ba2__prereq"/>

## Prerequisites

-   You have downloaded and installed the Cloud Connector, see [Installation](installation-57ae3d6.md).
-   You have assigned one of these roles/role collections to the subaccount user that you use for initial Cloud Connector setup, depending on the SAP BTP environment in which your subaccount is running:

    > ### Note:  
    > For the **Cloud Foundry** environment, you must know on which cloud management tools feature set \(A or B\) your account is running. For more information on feature sets, see [Cloud Management Tools — Feature Set Overview](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/caf4e4e23aef4666ad8f125af393dfb2.html "Cloud management tools represent the group of technologies designed for managing SAP BTP.") :arrow_upper_right:.


    <table>
    <tr>
    <th valign="top">

    Environment
    
    </th>
    <th valign="top">

    Required Roles/Role Collections
    
    </th>
    <th valign="top">

    More Information
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    **Cloud Foundry** \[feature set **A**\]
    
    </td>
    <td valign="top">
    
    The user must be a *member of the global account* that the subaccount belongs to.

    Alternatively, you can assign the user as *Security Administrator*.
    
    </td>
    <td valign="top">
    
    [Add Members to Your Global Account](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/4a0491330a164f5a873fa630c7f45f06.html "Add users as global account members using the SAP BTP cockpit.") :arrow_upper_right: 

    [Managing Security Administrators in Your Subaccount \[Feature Set A\]](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/6752c4b8435c456ebf67a97ddbbcb267.html "Running on the cloud management tools feature set A: When you create a subaccount, SAP BTP automatically grants your user the role for the administration of business users and their authorizations in the subaccount. Having this role, you can also add or remove other users who will then also be user and role administrators of this subaccount.") :arrow_upper_right:
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    **Cloud Foundry** \[feature set **B**\]
    
    </td>
    <td valign="top">
    
    Assign at least one of these *default role collections* \(all of them including the role `Cloud Connector Administrator`\):

    -   `Subaccount Administrator`
    -   `Cloud Connector Administrator`
    -   `Connectivity and Destination Administrator`

    Alternatively, you can assign a *custom role collection* to the user that includes the role `Cloud Connector Administrator`.
    
    </td>
    <td valign="top">
    
    [Default Role Collections \[Feature Set B\]](what-is-sap-btp-connectivity-daca64d.md#loiodaca64dacc6148fcb5c70ed86082ef91__table_default_role_collections_setB) 

    [Role Collections and Roles in Global Accounts, Directories, and Subaccounts \[Feature Set B\]](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/0039cf082d3d43eba9200fe15647922a.html "In the cloud management tools feature set B, SAP BTP provides a set of role collections to set up administrator access to your global account and subaccounts.") :arrow_upper_right:
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    **Neo**
    
    </td>
    <td valign="top">
    
    Assign at least one of these *default roles*:

    -   `Cloud Connector Admin` 
    -   `Administrator`

    Alternatively, you can assign a *custom role* to the user that includes the permission `manageSCCTunnels`.
    
    </td>
    <td valign="top">
    
    [Managing Member Authorizations in the Neo Environment](https://help.sap.com/viewer/ea72206b834e4ace9cd834feed6c0e09/Cloud/en-US/a1ab5c4cc117455392cd0a512c7f890d.html "SAP BTP includes predefined platform roles that support the typical tasks performed by users when interacting with the platform. In addition, subaccount administrators can combine various scopes into a custom platform role that addresses their individual requirements.") :arrow_upper_right:
    
    </td>
    </tr>
    </table>
    
    After establishing the Cloud Connector connection, this user is not needed any more, since it serves only for initial connection setup. You may revoke the corresponding role assignment then and remove the user from the *Members* list \( **Neo** environment\), or from the *Users* list \(**Cloud Foundry** environment\).

    > ### Note:  
    > If the Cloud Connector is installed in an environment that is operated by SAP, SAP provides a user that you can add as member in your SAP BTP subaccount and assign the required role.

-   We strongly recommend that you read and follow the steps described in [Recommendations for Secure Setup](recommendations-for-secure-setup-e7ea82a.md). For operating the Cloud Connector securely, see also [Security Guidelines](security-guidelines-8db6945.md).

Back to[Tasks](initial-configuration-db9170a.md#loiodb9170a7d97610148537d5a84bf79ba2__context) 



<a name="loiodb9170a7d97610148537d5a84bf79ba2__log_in"/>

## Log on to the Cloud Connector

To administer the Cloud Connector, you need a Web browser. To check the list of supported browsers, see [Prerequisites and Restrictions](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/e6ddaefcbb571014b70fa01fc6a3f818.html "Find a list of the product prerequisites and restrictions for SAP BTP.") :arrow_upper_right: → section *Browser Support*.

1.  In a Web browser, enter: `https://<hostname>:<port>` 
    -   *<hostname\>* refers to the machine on which the Cloud Connector is installed. If installed on your machine, you can simply enter `localhost`.
    -   *<port\>* is the Cloud Connector port specified during installation \(the default port is `8443`\).

2.  On the logon screen, enter `Administrator` / `manage` \(case sensitive\) for *<User Name\>* / *<Password\>*.

    > ### Note:  
    > By default, the Cloud Connector includes a self-signed UI certificate. Browsers may show a security warning because they don't trust the issuer of this certificate. In this case, you can skip the warning message.


Back to[Tasks](initial-configuration-db9170a.md#loiodb9170a7d97610148537d5a84bf79ba2__context) 



<a name="loiodb9170a7d97610148537d5a84bf79ba2__change_password"/>

## Initial Setup

1.  When you first log in, you must change the password before you continue, regardless of the installation type you have chosen.
2.  Choose between master and shadow installation. Use *Master* if you are installing a single Cloud Connector instance or a main instance from a pair of Cloud Connector instances. See [Install a Failover Instance for High Availability](install-a-failover-instance-for-high-availability-c697705.md).

    ![](images/SCC_InitialConfig_-_MandatoryPWChange_InstallType_76126d2.png)

3.  \(Optional\): When configuring a master, you can provide a \(free-text\) *Description* for this Cloud Connector instance that helps you distinguish different Cloud Connectors. This information will also be shown in the *Cloud Connectors* view in the SAP BTP cockpit.


**User Administration**

To edit the password for the `Administrator` user, choose *Configuration* from the main menu, tab *User Interface*, section *User Administration*:

![](images/SCC_InitialConfig_-_AdminPW_761273d.png)

> ### Note:  
> User name and password cannot be changed at the same time. If you want to change the user name, you must enter only the current password in a first step. Do not enter values for *<New Password\>* or *<Repeat New Password\>* when changing the user name. To change the password in second step, enter the old password, the new one, and the repeated \(new\) password, but leave the user name unchanged.

Back to[Tasks](initial-configuration-db9170a.md#loiodb9170a7d97610148537d5a84bf79ba2__context) 



<a name="loiodb9170a7d97610148537d5a84bf79ba2__configure_proxy"/>

## Set up Connection Parameters and HTTPS Proxy



When logging in for the first time, the following screen is displayed every time you choose an option from the main menu that requires a configured subaccount:

![](images/SCC_InitialConfig_-_DefineSubaccount_b356833.png)

If your internal landscape is protected by a firewall that blocks any outgoing TCP traffic, you must specify an HTTPS proxy that the Cloud Connector can use to connect to SAP BTP. Normally, you must use the same proxy settings as those being used by your standard Web browser. The Cloud Connector needs this proxy for two operations:

-   Download the correct connection configuration corresponding to your subaccount ID in SAP BTP.
-   Establish the SSL tunnel connection from the Cloud Connector user to your SAP BTP subaccount.

> ### Note:  
> If you want to skip the initial configuration, you can click the ![](images/Skip_initial_configuration_000bd0a.png) icon in the upper right corner. You might need this in case of connectivity issues shown in your logs. You can add subaccounts later as described in [Managing Subaccounts](managing-subaccounts-f16df12.md).

The Cloud Connector collects the following required information for your subaccount connection:

1.  For *<Region\>*, specify the SAP BTP region that should be used. You can choose it from the drop-down list, see [Regions](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/350356d1dc314d3199dca15bd2ab9b0e.html "You can deploy applications in different regions. Each region represents a geographical location (for example, Europe, US East) where applications, data, or services are hosted.") :arrow_upper_right:. 

    > ### Note:  
    > You can also configure a region yourself, if it is not part of the standard list. Either insert the region host manually, or create a custom region, as described in [Configure Custom Regions](configure-custom-regions-a994a75.md).

2.  For *<Subaccount\>*, *<Subaccount User\>* and *<Password\>*, enter the values you obtained when you registered your subaccount on SAP BTP.

    > ### Note:  
    > For a subaccount in the **Cloud Foundry** environment, you must enter the subaccount **ID** as *<Subaccount\>*, rather than its actual \(technical\) name. For information on getting the subaccount ID, see [Find Your Subaccount ID \(Cloud Foundry Environment\)](find-your-subaccount-id-cloud-foundry-environment-b43eff2.md). As *<Subaccount User\>* you must provide your `Login E-mail` instead of a user ID. The user must be a member of the global account the subaccount belongs to.

    You can also add a new subaccount user with the role `Cloud Connector Admin` in the SAP BTP cockpit and use the new user and password.

    > ### Note:  
    > The Cloud Connector does not yet support *SAP Universal ID*. Please use your S-user or P-user credentials for the *<subaccount user\>* and *<password\>* fields instead.
    > 
    > For more information, see SAP note [3085908](https://me.sap.com/notes/3085908).

    For the **Neo** environment, see [Add Members to Your Neo Subaccount](https://help.sap.com/viewer/ea72206b834e4ace9cd834feed6c0e09/Cloud/en-US/a253570f081e448d9f78fc2bfeedfdc3.html "Add users as members to a subaccount in the Neo environment and assign roles to them using the SAP BTP cockpit.") :arrow_upper_right:.

    For the **Cloud Foundry** environment, see [Add Org Members Using the Cockpit](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/a4eeaf179ee646b99558f27c0bae7b3e.html "Add users as org members and assign roles to grant the users access to information, such as user and quota information in a Cloud Foundry org.") :arrow_upper_right:.

    > ### Tip:  
    > When using SAP Cloud Identity Services - Identity Authentication \(IAS\) as platform identity provider with two-factor authentication for your subaccount, you can simply append the required token to the regular password.

    > ### Tip:  
    > For a subaccount in the **Cloud Foundry** environment, the Cloud Connector supports the use of a custom identity provider \(IDP\) via single sign-on \(SSO\) passcode. For more information, see [Use a Custom IDP for Subaccount Configuration](use-a-custom-idp-for-subaccount-configuration-2022612.md).

3.  \(Optional\) You can define a *<Display Name\>* that lets you easily recognize a specific subaccount in the UI compared to the technical subaccount name.
4.  \(Optional\) You can define a *<Location ID\>* identifying the location of this Cloud Connector for a specific subaccount. As of Cloud Connector release **2.9.0**, the location ID is used as routing information and therefore you can connect multiple Cloud Connectors to a single subaccount. If you don't specify any value for *<Location ID\>*, the default is used, which represents the behavior of previous Cloud Connector versions. The location ID must be unique per subaccount and should be an identifier that can be used in a URI. To route requests to a Cloud Connector with a location ID, the location ID must be configured in the respective destinations.

    > ### Note:  
    > Location IDs provided in older versions of the Cloud Connector are discarded during upgrade to ensure compatibility for existing scenarios.

5.  Enter a suitable proxy host from your network and the port that is specified for this proxy. If your network requires an authentication for the proxy, enter a corresponding proxy user and password. You must specify a proxy server that supports SSL communication \(a standard HTTP proxy does not suffice\).

    > ### Note:  
    > These settings strongly depend on your specific network setup. If you need more detailed information, please contact your local system administrator.

6.  \(Optional\) You can provide a *<Description\>* \(free-text\) of the subaccount that is shown when choosing the *Details* icon in the *Actions* column of the *Subaccount Dashboard*. It lets you identify the particular Cloud Connector you use.
7.  Choose *Save*.

The Cloud Connector now starts a handshake with SAP BTP and attempts to establish a secure SSL tunnel to the server that hosts the subaccount in which your on-demand applications are running. However, no requests are yet allowed to pass from the cloud side to any of your internal back-end systems. To allow your on-demand applications to access specific internal back-end systems, proceed with the access configuration described in the next section.

> ### Note:  
> The internal network must allow access to the port. Specific configuration for opening the respective port\(s\) depends on the firewall software used. The default ports are `80` for HTTP and `443` for HTTPS. For RFC communication, you must open a gateway port \(default: `33+<instance number>` and an arbitrary message server port. For a connection to a HANA Database \(on SAP BTP\) via JDBC, you must open an arbitrary *outbound* port in your network. Mail \(SMTP\) communication is not supported.

-   If you later want to change your proxy settings \(for example, because the company firewall rules have changed\), choose *Configuration* from the main menu and go to the *Cloud* tab, section*HTTPS Proxy*. Some proxy servers require credentials for authentication. In this case, you must provide the relevant user/password information.

    ![](images/SCC_InitialConfig_-_HTTPS_Proxy_169e625.png)

-   If you want to change the description for your Cloud Connector, choose *Configuration* from the main menu, go to the *Cloud* tab, section *Connector Info* and edit the description:

    ![](images/SCC_InitialConfig_-_ConnectorInfo_8898b57.png)


Back to[Tasks](initial-configuration-db9170a.md#loiodb9170a7d97610148537d5a84bf79ba2__context) 



<a name="loiodb9170a7d97610148537d5a84bf79ba2__establish_cloud_conection"/>

## Establish Connections to SAP BTP

As soon as the initial setup is complete, the tunnel to the cloud endpoint is open, but no requests are allowed to pass until you have performed the *Access Control* setup, see [Configure Access Control](configure-access-control-f42fe44.md).

To manually close \(and reopen\) the connection to SAP BTP, choose your subaccount from the main menu and select the *Disconnect* button \(or the *Connect* button to reconnect to SAP BTP\).

![](images/SCC_InitialConfig_-_ConnectorState_761280b.png)

-   The green icon next to *Region Host* indicates that it is valid and can be reached.
-   If an *HTTPS Proxy* is configured, its availability is shown the same way. In the screenshot, the grey diamond icon next to *HTTPS Proxy* indicates that connectivity is possible without proxy configuration.

In case of a timeout or a connectivity issue, these icons are yellow \(warning\) or red \(error\), and a tooltip shows the cause of the problem. *Initiated By* refers to the user that has originally established the tunnel. During normal operations, this user is no longer needed. Instead, a certificate is used to open the connection to a subaccount.

-   The status of the certificate is shown next to *Subaccount Certificate*. It is shown as valid \(green icon\), if the expiration date is still far in the future, and turns to yellow if expiration approaches according to your alert settings. It turns red as soon as it has expired. This is the latest point in time, when you should [Update the Certificate for Your Subaccount](update-the-certificate-for-a-subaccount-071708a.md).

> ### Note:  
> When connected, you can monitor the Cloud Connector also in the *Connectivity* section of the SAP BTP cockpit. There, you can track attributes like version, description and high availability set up. Every Cloud Connector configured for your subaccount automatically appears in the *Connectivity* section of the cockpit.

Back to[Tasks](initial-configuration-db9170a.md#loiodb9170a7d97610148537d5a84bf79ba2__context) 

**Related Information**  


[Managing Subaccounts](managing-subaccounts-f16df12.md "Add and connect your SAP BTP subaccounts to the Cloud Connector.")

[Initial Configuration \(HTTP\)](initial-configuration-http-3f974ea.md "Configure the Cloud Connector for HTTP communication.")

[Initial Configuration \(RFC\)](initial-configuration-rfc-f09eefe.md "Configure a Secure Network Connection (SNC) to set up the Cloud Connector for RFC communication to an ABAP backend system.")

[Configuring the Cloud Connector for LDAP](configuring-the-cloud-connector-for-ldap-f94810a.md "Configure the Cloud Connector to support LDAP in different scenarios (cloud applications using LDAP or Cloud Connector authentication).")

[Managing Member Authorizations in the Neo Environment](https://help.sap.com/viewer/ea72206b834e4ace9cd834feed6c0e09/Cloud/en-US/a1ab5c4cc117455392cd0a512c7f890d.html "SAP BTP includes predefined platform roles that support the typical tasks performed by users when interacting with the platform. In addition, subaccount administrators can combine various scopes into a custom platform role that addresses their individual requirements.") :arrow_upper_right:

[Use a Custom IDP for Subaccount Configuration](use-a-custom-idp-for-subaccount-configuration-2022612.md "Enable custom identity provider (IDP) authentication to configure a Cloud Foundry subaccount in the Cloud Connector by using a one-time passcode.")

