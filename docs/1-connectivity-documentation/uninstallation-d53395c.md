<!-- loiod53395c4692c427881220c161ba51732 -->

# Uninstallation

Uninstall an installer version or portable version of the Cloud Connector.

-   If you have installed an installer variant of the Cloud Connector, follow the steps for your operating system to uninstall the Cloud Connector.
-   To uninstall a developer version, proceed as described in section **Portable Variants**.



## Microsoft Windows OS

1.  In the Windows software administration tool, search for `Cloud Connector` \(formerly named `SAP HANA cloud connector 2.x`\).
2.  Select the entry and follow the appropriate steps to uninstall it.
3.  When you are uninstalling in the context of an upgrade, make sure to retain the configuration files.



## Linux OS

To uninstall Cloud Connector 2.x, execute the following command:

```
rpm -e com.sap.scc-ui
```

> ### Caution:  
> This command also removes the configuration files.



## Mac OS X

There is no installer variant for Mac OS X, only a `portable` one.



## Portable Variants

\(Microsoft Windows OS, Linux OS, Mac OS X\) If you have installed a portable version \(zip or tgz archive\) of the Cloud Connector, simply remove the directory in which you have extracted the Cloud Connector archive.

**Related Information**  


[Installation](installation-57ae3d6.md "Choose a procedure to install the Cloud Connector on your operating system.")

