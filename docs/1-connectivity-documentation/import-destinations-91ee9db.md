<!-- loio91ee9db4737d43b798997ab93e7f3d6e -->

# Import Destinations

How to import destinations in the *Destinations* editor \(SAP BTP cockpit\).



## Prerequisites

You have previously created an HTTP destination.

> ### Note:  
> The *Destinations* editor allows importing destination files with extension `.props`, `.properties`, `.jks`, and `.txt`, as well as files with no extension. Destination files must be encoded in **ISO 8859-1** character encoding.



## Procedure

1.  Log into the cockpit and open the *Destinations* editor.

2.  Choose *Import from File*.

3.  Browse to a configuration file that contains destination configuration.

    -   If the configuration file contains valid data, it is displayed in the *Destinations* editor with no errors. The *Save* button is enabled so that you can successfully save the imported destination.
    -   If the configuration file contains invalid properties or values, under the relevant fields in the *Destinations* editor are displayed error messages in red which prompt you to correct them accordingly.


**Related Information**  


[Edit and Delete Destinations](edit-and-delete-destinations-372dee2.md "How to edit and delete destinations in the Destinations editor (SAP BTP cockpit).")

[Destination Examples](destination-examples-3a2d575.md "Find configuration examples for HTTP and RFC destinations in the Cloud Foundry environment, using different authentication types.")

