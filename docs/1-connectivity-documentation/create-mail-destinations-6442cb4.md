<!-- loio6442cb4f8b0f41178abce14c35f5def4 -->

# Create Mail Destinations

Create mail destinations in the *Destinations* editor \(SAP BTP cockpit\).



## Prerequisites

You have logged into the cockpit and opened the *Destinations* editor.



<a name="loio6442cb4f8b0f41178abce14c35f5def4__steps_j4g_jfb_pn"/>

## Procedure

1.  Choose *New Destination*.

    > ### Note:  
    > In section **Destination Configuration**, do not change the default tab *Blank Template*. Tab *Service Instance* only applies for HTTP destinations.

2.  Enter a destination name.

3.  From the *Type* dropdown menu, choose `MAIL`.

4.  The *Description* field is optional.

5.  From the *Proxy Type* dropdown box, select `Internet` or `OnPremise`, depending on the connection you need to provide for your application.

    > ### Note:  
    > To access a mail server located in your own network \(via Cloud Connector\), choose `OnPremise`. To access an external mail server, choose `Internet`.

6.  Optional: You can enter additional properties.

    1.  In the *Additional Properties* panel, choose *New Property*.

    2.  Enter a key \(name\) or choose one from the dropdown menu and specify a value for the property. You can add as many properties as you need. Each key of an additional property must start with "`mail.`".

    3.  To delete a property, choose the ![](images/Delete_property_cockpit_321c7c7.png) button next to it.


7.  When you are ready, choose the *Save* button.


**Related Information**  


[Edit and Delete Destinations](edit-and-delete-destinations-372dee2.md "How to edit and delete destinations in the Destinations editor (SAP BTP cockpit).")

[Destination Examples](destination-examples-3a2d575.md "Find configuration examples for HTTP and RFC destinations in the Cloud Foundry environment, using different authentication types.")

[Cloud Connector](cloud-connector-e6c7616.md "Learn more about the Cloud Connector: features, scenarios and setup.")

