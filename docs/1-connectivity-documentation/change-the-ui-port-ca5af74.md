<!-- loioca5af74ccdfc4b91b530ae498fc58e5e -->

# Change the UI Port



## Context

By default, the Cloud Connector uses port `8443` for its administration UI. If this port is blocked by another process, or if you want to change it after the installation, you can use the `changeport` tool, provided with Cloud Connector version **2.6.0** and higher.

> ### Note:  
> On Windows, you can also choose a different port during installation.



## Procedure

1.  Change to the installation directory of the Cloud Connector. To adjust the port and execute one of the following commands:

    -   Microsoft Windows OS:

        ```
        changeport <desired_port>
        ```

    -   Linux OS, Mac OS X:

        ```
        ./changeport.sh <desired_port>
        ```


2.  When you see a message stating that the port has been successfully modified, restart the Cloud Connector to activate the new port.


