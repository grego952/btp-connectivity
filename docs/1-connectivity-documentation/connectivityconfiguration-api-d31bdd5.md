<!-- loiod31bdd53b57744fcb9eb9c93556cfddf -->

# ConnectivityConfiguration API

Use the `ConnectivityConfiguration` API to retrieve destination configurations and certificate configurations in the Cloud Foundry environment.



<a name="loiod31bdd53b57744fcb9eb9c93556cfddf__section_os1_5vf_wpb"/>

## Overview

The `ConnectivityConfiguration` API is visible by default from the web applications hosted on SAP Java Buildpack. You can access it via a JNDI lookup.

Besides managing destination configurations, you can also allow your applications to use their own managed HTTP clients. The `ConnectivityConfiguration` API provides you with direct access to the destination configurations of your applications.

To learn how to retrieve destination configurations, follow the procedure below.



## Procedure

1.  To consume a connectivity configuration using JNDI, you must define the `ConnectivityConfiguration` API as a resource in the *context.xml* file.

    Example of a `ConnectivityConfiguration` resource named `connectivityConfiguration`, which is described in the *context.xml* file:

    **src/main/webapp/META-INF/context.xml**

    > ### Sample Code:  
    > ```
    > <?xml version='1.0' encoding='utf-8'?>
    >  
    > <Context>
    >     <Resource name="connectivityConfiguration" auth="Container"
    >               type="com.sap.core.connectivity.api.configuration.ConnectivityConfiguration"
    >               factory="com.sap.core.connectivity.api.jndi.ServiceObjectFactory"/>
    > </Context>
    > ```

2.  You also need to enable Connectivity `ApiExt` with an environment variable and bind the appropriate services in `manifest.yml`:

    **manifest.yml** 

    > ### Sample Code:  
    > ```
    > applications:
    >   - ...
    >     env:
    >       USE_CONNECTIVITY_APIEXT: true
    >     services:
    >       - xsuaa-instance
    >       - destination-instance
    >       - connectivity-instance
    >       ...
    > ```

3.  In your servlet code, you can look up the `ConnectivityConfiguration` API from the JNDI registry as follows:

    > ### Sample Code:  
    > ```
    > import javax.naming.Context;
    > import javax.naming.InitialContext;
    > import com.sap.core.connectivity.api.configuration.ConnectivityConfiguration;
    > ...
    >  
    > // look up the connectivity configuration API "connectivityConfiguration"
    > Context ctx = new InitialContext();
    > ConnectivityConfiguration configuration = (ConnectivityConfiguration) ctx.lookup("java:comp/env/connectivityConfiguration");
    > 
    > ```

4.  With the retrieved `ConnectivityConfiguration` API, you can read all properties of any destination defined on subscription, application, or subaccount level.

    > ### Sample Code:  
    > ```
    > // get destination configuration for "myDestinationName"
    > DestinationConfiguration destConfiguration = configuration.getConfiguration("myDestinationName");
    >  
    > // get a single destination property
    > String authenticationType = destConfiguration.getProperty("Authentication");
    >  
    > // get all destination properties
    > Map<String, String> allDestinationPropeties = destConfiguration.getAllProperties();
    > ```

    > ### Note:  
    > If you have two destinations with the same name, for example, one configured on subaccount level and the other on service instance/subscription level, the `getConfiguration()` method will return the destination on instance/subscription level.
    > 
    > The preference order is:
    > 
    > 1.  Instance/subscription level
    > 2.  Subaccount level

5.  If a trust store and a key store are defined in the corresponding destination, you can access them by using the methods `getKeyStore` and `getTrustStore`.

    > ### Sample Code:  
    > ```
    >     // get destination configuration for "myDestinationName"
    > DestinationConfiguration destConfiguration = configuration.getConfiguration("myDestinationName");
    >  
    > // get the configured keystore
    > KeyStore keyStore = destConfiguration.getKeyStore();
    >  
    > // get the configured truststore
    > KeyStore trustStore = destConfiguration.getTrustStore();
    >   
    > // create sslcontext
    > TrustManagerFactory tmf = TrustManagerFactory.getInstance(TrustManagerFactory.getDefaultAlgorithm());
    > tmf.init(trustStore);
    >   
    > KeyManagerFactory keyManagerFactory = KeyManagerFactory.getInstance(KeyManagerFactory.getDefaultAlgorithm());
    >  
    > // get key store password from destination
    > String keyStorePassword = destConfiguration.getProperty("KeyStorePassword");
    > keyManagerFactory.init(keyStore, keyStorePassword.toCharArray());
    >   
    > SSLContext sslcontext = SSLContext.getInstance("TLSv1");
    > sslcontext.init(keyManagerFactory.getKeyManagers(), tmf.getTrustManagers(), null);
    > SSLSocketFactory sslSocketFactory = sslcontext.getSocketFactory();
    >   
    > // get the destination URL
    > String value = destConfiguration.getProperty("URL");
    > URL url = new URL(value);
    >   
    > // use the sslcontext for url connection
    > URLConnection urlConnection = url.openConnection();
    > ((HttpsURLConnection) urlConnection).setSSLSocketFactory(sslSocketFactory);
    > urlConnection.connect();
    > InputStream in = urlConnection.getInputStream();
    > ...
    > ```


