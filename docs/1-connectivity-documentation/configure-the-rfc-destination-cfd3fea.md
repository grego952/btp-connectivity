<!-- loiocfd3fea58f62411485519c26e5872403 -->

# Configure the RFC Destination

Configure an RFC destination on SAP BTP that you can use in your Web application to call the cloud ABAP system.

To configure the destination, you must use a WebSocket application server host name \(`<id>.abap.eu10.hana.ondemand.com`\) and a WebSocket port \(`443`\).

1.  Create a `.properties` file with the following settings:

    ```ini
    
     Name=JCoDemoSystem 
     Type=RFC 
     jco.client.wshost= <id>.abap.eu10.hana.ondemand.com 
     jco.client.wsport=443 
     jco.client.alias_user=<DEMOUSER> 
     jco.client.passwd=<Password> 
     jco.client.client=100 
     jco.client.lang=EN 
     jco.destination.pool_capacity=5
     jco.destination.proxy_type=Internet
    
    ```

2.  Go to your subaccount in the cloud cockpit.
    1.  From the subaccount menu, choose *Connectivity* \> *Destinations* \> *Import Destination* and upload this file.
    2.  Alternatively, you can create a destination for the service instance `destination_jco` to make it visible only for this instance. To do this, go to *<your space\>* \> *Services* \> *Service Instances* \> *<your destination\_instance\>* and choose *Destinations*.

3.  Specify a trust/key store or security information, see [WebSocket Connection](target-system-configuration-ab6eac9.md#loioab6eac92978f469e9eabe3d477ca2411__web).



<a name="loiocfd3fea58f62411485519c26e5872403__section_xsy_nkc_cgb"/>

## Next Steps

-   [Monitoring Your Web Application](monitoring-your-web-application-9bd8f7d.md) \(Optional\)

**Related Information**  


[Target System Configuration](target-system-configuration-ab6eac9.md "Learn about the JCo properties you can use to configure the target sytem information in an RFC destination.")

