<!-- loio9bd8f7d16c4b418fa8170a6ddbcc2e04 -->

# Monitoring Your Web Application

Monitor the state and logs of your Web application deployed on SAP BTP, using the Application Logging service.

For this purpose, create an instance of the Application Logging service \(as you did for the Destination service\) and bind it to your application, see [Create and Bind Service Instances](create-and-bind-service-instances-6dd5e26.md).

To activate JCo logging, set the following property in the *env* section of your manifest file:

```
SET_LOGGING_LEVEL: '{com.sap.conn.jco: INFO, com.sap.core.connectivity.jco: INFO}'
```

Now you can see and open the logs in the cloud cockpit or in the Kibana Dashboard in the tab *Logs*, if you are within your application.

For error analysis, you can activate more detailed JCo debug tracing:

```
SET_LOGGING_LEVEL: '{com.sap.conn.jco: DEBUG, com.sap.core.connectivity.jco: DEBUG}'
```

To include other relevant components for debug tracing, set:

```
SET_LOGGING_LEVEL: '{com.sap.conn.jco: DEBUG, com.sap.core.connectivity.jco: DEBUG, com.sap.core.connectivity.apiext: DEBUG, com.sap.cloud.security: DEBUG, com.sap.xs.security: DEBUG, com.sap.xs.env: DEBUG}'
```

