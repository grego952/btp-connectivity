<!-- loioc697705179a24d2b8b6be038fae59c33 -->

# Install a Failover Instance for High Availability

The Cloud Connector lets you install a redundant instance that monitors the main instance.



<a name="loioc697705179a24d2b8b6be038fae59c33__context"/>

## Context

In a failover setup, when the main instance should go down for some reason, a redundant one can take over its role. The main instance of the Cloud Connector is called **master** and the redundant instance is called the **shadow**. The shadow has to be installed and connected to its master. During the setup of high availability, the master pushes the entire configuration to the shadow. Later on, during normal operation, the master also pushes configuration updates to the shadow. Thus, the shadow instance is kept synchronized with the master instance. The shadow pings the master regularly. If the master is not reachable for a while, the shadow tries to take over the master role and to establish the tunnel to SAP BTP.

> ### Note:  
> For detailed information about sizing of the master and the shadow instance, see also [Sizing Recommendations](sizing-recommendations-f008494.md).

<a name="concept_p4y_fhj_q4"/>

<!-- concept\_p4y\_fhj\_q4 -->

## Procedure



<a name="concept_p4y_fhj_q4__preparing"/>

## Preparing the Master Instance for High Availability

1.  Open the Cloud Connector UI and go to the master instance.
2.  From the main menu, choose *High Availability*.
3.  Choose *Enable*.

    ![](images/SCC_HA_-_Enable_f1b81ec.png)

    If this flag is not activated, no shadow instance can connect to this Cloud Connector. Additionally, when providing a concrete *Shadow Host*, you can ensure that only from this host a shadow instance can be connected.

    > ### Caution:  
    > Pressing the *Reset* button resets all high availability settings to their initial state. As a result, high availability is disabled and the shadow host is cleared. Reset only works if no shadow is connected.




<a name="concept_p4y_fhj_q4__install"/>

## Installing and Setting Up a Shadow Instance

Install the shadow instance in the same network segment as the master instance. Communication between master and shadow via proxy is not supported. The same distribution package is used for master and shadow instance.

> ### Note:  
> If you plan to use LDAP for the user authentication on both master and shadow, make sure you configure it **before** you establish the connection from shadow to master.

1.  On first start-up of a Cloud Connector instance, a UI wizard asks you whether the current instance should be master or shadow. Choose *Shadow* and *Save*:

    ![](images/SCC_HA_-_Installation_Type_fd13d62.png)

2.  From the main menu, choose *Shadow Connector* and provide connection data for the master instance, that is, the master host and port. As of version 2.8.1.1, you can choose from the list of known host names, to use the host name under which the shadow host is visible to the master. You can specify a host name manually, if the one you want is not on the list. For the first connection, you must log on to the master instance, using the user name and password for the master instance. The master and shadow instances exchange X.509 certificates, which will be used for mutual authentication.

    ![](images/SCC_HA_-_Shadow_Edit_5499f27.png)

    > ### Note:  
    > If you want to attach the shadow instance to a different master, press the *Reset* button. All your high availability settings will be removed, that is, reset to their initial state. This works only if the shadow is not connected.

3.  Upon a successful connection, the master instance pushes the entire configuration plus some information about itself to the shadow instance. You can see this information in the UI of the shadow instance, but you can't modify it.
4.  The UI on the master instance shows information about the connected shadow instance. From the main menu, choose *High Availability*:

    ![](images/SCC_HA_-_ShadowInfoMaster_f78b153.png)

5.  As of version **2.6.0**, the *High Availability* view includes an *Alert Messages* panel. It displays alerts if configuration changes have not been pushed successfully. This might happen, for example, if a temporary network failure occurs at the same time a configuration change is made. This panel lets an administrator know if there is an inconsistency in the configuration data between master and shadow that could cause trouble if the shadow needs to take over. Typically, the master recognizes this situation and tries to push the configuration change at a later time automatically. If this is successful, all failure alerts are removed and replaced by a warning alert showing that there had been trouble before. As of version **2.8.0.1**, these alerts have been integrated in the general *Alerting* section; there is no longer a separate *Alert Messages* panel.

    If the master doesn't recover automatically, disconnect, then reconnect the shadow, which triggers a complete configuration transfer.


**Related Information**  


[Initial Configuration](initial-configuration-db9170a.md "After installing and starting the Cloud Connector, log on to the administration UI and perform the required configuration to make your Cloud Connector operational.")

[Master and Shadow Administration](master-and-shadow-administration-7f57de1.md "")

