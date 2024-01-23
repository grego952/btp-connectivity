<!-- loio60f00ec5724e4875b51a2cadfb2364b2 -->

# Destination Java APIs

Use Destination service Java APIs to optimize application development in the Cloud Foundry environment.

When running your cloud application with *SAP Java Buildpack*, you can use the following Java APIs to optimize the application development:

-   [ConnectivityConfiguration API](connectivityconfiguration-api-d31bdd5.md): Retrieve destination configurations.
-   [AuthenticationHeaderProvider API](authenticationheaderprovider-api-2959ab8.md): Retrieve prepared authentication headers, ready to be used towards the remote target system.

Add the *Connectivity Apiext* dependency in the `pom.xml` file:

```
<dependency>
    <groupId>com.sap.cloud.connectivity.apiext</groupId>
    <artifactId>com.sap.cloud.connectivity.apiext</artifactId>
    <version>${connectivity-apiext.version}</version>
    <scope>provided</scope>
</dependency>
```

For more information on *SAP Java Buildpack*, see [Developing Java in the Cloud Foundry Environment](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/a3f90069d6cd41da82f34a6123d82ce6.html "Find selected information for Java development on SAP BTP, Cloud Foundry and references to more detailed sources.") :arrow_upper_right:.

