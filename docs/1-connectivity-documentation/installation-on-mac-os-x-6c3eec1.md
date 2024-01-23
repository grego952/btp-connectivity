<!-- loio6c3eec1350e04d4fab801263e26ad939 -->

# Installation on Mac OS X

Installing the Cloud Connector on a Mac OS X operating system.



## Prerequisites

> ### Note:  
> Mac OS X is not supported for productive scenarios. The developer version described below must not be used as productive version.

> ### Caution:  
> The Cloud Connector does not natively support the M1/M2 architecture yet. Make sure you use a JVM based on the *x64* CPU architecture, and not the *aarch64* one.

-   You have one of the supported 64-bit operating systems. For more information, see [Product Availability Matrix](prerequisites-e23f776.md#loioe23f776e4d594fdbaeeb1196d47bbcc0__matrix).
-   You have downloaded the `tar.gz` archive for the developer use case on Mac OS X from [SAP Development Tools for Eclipse](https://tools.hana.ondemand.com/#cloud).
-   A supported Java version must be installed. For more information, see [JDKs](prerequisites-e23f776.md#loioe23f776e4d594fdbaeeb1196d47bbcc0__jdk).

    If you want to use SAP JVM, you can download it from the [SAP Development Tools for Eclipse](https://tools.hana.ondemand.com/#cloud) page.

-   Environment variable *<JAVA\_HOME\>* must be set to the Java installation directory so that the `bin` subdirectory can be found. Alternatively, you can add the Java installation's `bin` subdirectory to the *<PATH\>* variable.



## Procedure

1.  Extract the `tar.gz` file to an arbitrary directory on your local file system using the following command:

    ```
    tar -xzof sapcc-<version>-macosx-x64.tar.gz 
    ```

2.  Go to this directory and start Cloud Connector using the `go.sh` script.

3.  Continue with the `Next Steps` section.

    > ### Note:  
    > The Cloud connector is not started as a daemon, and therefore will not automatically start after a reboot of your system. Also, the Mac OS X version of Cloud Connector does not support the automatic upgrade procedure.




## Next Steps

1.  Open a browser and enter: `https://<hostname>:8443`. *<hostname\>* is the host name of the machine on which you installed the Cloud Connector.

    If you access the Cloud Connector locally from the same machine, you can simply enter `localhost`.

2.  Continue with the initial configuration of the Cloud Connector, see [Initial Configuration](initial-configuration-db9170a.md).

**Related Information**  


[Recommendations for Secure Setup](recommendations-for-secure-setup-e7ea82a.md "For the Connectivity service and the Cloud Connector, you should apply the following guidelines to guarantee the highest level of security for these components.")

