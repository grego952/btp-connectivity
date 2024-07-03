<!-- loio296f4576823a44e68a5fef515c27fa0f -->

# Configure the RFC Destination

Configure an RFC destination on SAP BTP that you can use in your Web application to call the on-premise ABAP system.

To configure the destination, you must use a virtual application server host name \(`abapserver.hana.cloud`\) and a virtual system number \(`42`\) that you will expose later in the Cloud Connector. Alternatively, you could use a load balancing configuration with a message server host and a system ID.

1.  Create a `.properties` file with the following settings:

    ```ini
    
    Name=JCoDemoSystem 
     Type=RFC 
     jco.client.ashost=abapserver.hana.cloud 
     jco.client.sysnr=42 
     jco.destination.proxy_type=OnPremise
     jco.client.user=<DEMOUSER> 
     jco.client.passwd=<Password> 
     jco.client.client=000 
     jco.client.lang=EN 
     jco.destination.pool_capacity=5
    
    ```

2.  Go to your subaccount in the cloud cockpit.
    1.  From the subaccount menu, choose *Connectivity* \> *Destinations* \> *Import Destination* and upload this file.
    2.  Alternatively, you can create a destination for the service instance `destination_jco` to make it visible only for this instance. To do this, go to *<your space\>* \> *Services* \> *Service Instances* \> *<your destination\_instance\>* and choose *Destinations*.

3.  Call again the URL that references the cloud application in the Web browser. The Web application should now return a different exception:

    ```
    
    
    Exception occurred while executing STFC_CONNECTION in system JCoDemoSystem 
    
    com.sap.conn.jco.JCoException: (102) JCO_ERROR_COMMUNICATION: Opening connection to backend failed: Opening connection to abapserver.hana.cloud:sapgw42 denied. Expose the system in your Cloud Connector in case it was a valid request.
    
        at com.sap.conn.jco.rt.MiddlewareJavaRfc.generateJCoException(MiddlewareJavaRfc.java:487)
        at com.sap.conn.jco.rt.MiddlewareJavaRfc$JavaRfcClient.connect(MiddlewareJavaRfc.java:1216)
        at com.sap.conn.jco.rt.ClientConnection.connect(ClientConnection.java:700)
        at com.sap.conn.jco.rt.RepositoryConnection.connect(RepositoryConnection.java:72)
        at com.sap.conn.jco.rt.PoolingFactory.init(PoolingFactory.java:113)
        at com.sap.conn.jco.rt.ConnectionManager.createFactory(ConnectionManager.java:426)
        at com.sap.conn.jco.rt.DefaultConnectionManager.createFactory(DefaultConnectionManager.java:46)
        at com.sap.conn.jco.rt.ConnectionManager.getFactory(ConnectionManager.java:376)
        at com.sap.conn.jco.rt.RfcDestination.getSystemID(RfcDestination.java:1101)
    
            ..... (cut rest of the call stack)
    
    ```

4.  This means that the Cloud Connector denied opening a connection to this system. As a next step, you must configure the system in your installed Cloud Connector.



<a name="loio296f4576823a44e68a5fef515c27fa0f__section_xsy_nkc_cgb"/>

## Next Steps

-   [Configure the Cloud Connector](configure-the-cloud-connector-783a96e.md)
-   [Monitoring Your Web Application](monitoring-your-web-application-e2ce724.md) \(Optional\)

**Related Information**  


[Target System Configuration](target-system-configuration-ab6eac9.md "Learn about the JCo properties you can use to configure the target sytem information in an RFC destination.")

