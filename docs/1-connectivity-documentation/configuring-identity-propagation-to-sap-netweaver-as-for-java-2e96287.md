<!-- loio2e962873ace64b108a58b69d43f09a5e -->

# Configuring Identity Propagation to SAP NetWeaver AS for Java

Find step-by-step instructions on how to set up an application server for Java \(AS Java\) to enable identity propagation for HTTPS.

> ### Note:  
> The information in this section applies to both principal propagation and technical user propagation. These two types of user propagation are combined as *identity* propagation.



<a name="loio2e962873ace64b108a58b69d43f09a5e__section_gbb_hzx_tmb"/>

## Prerequisites

To perform the following steps, you must have the corresponding administrator authorizations in AS Java \(SAP NetWeaver Administrator\) as well as an administrator user for the Cloud Connector.

<a name="task_idd_s3f_5mb"/>

<!-- task\_idd\_s3f\_5mb -->

## Configure AS Java to Trust the Cloud Connector's System Certificate



<a name="task_idd_s3f_5mb__steps_arx_w3f_5mb"/>

## Procedure

1.  Go to *SAP NetWeaver Administrator* \> *Certificates and Keys* and import the Cloud Connector's system certificate into the *Trusted CAs* keystore view. See [Importing Certificate and Key From the File System](https://help.sap.com/viewer/1531c8a1792f45ab95a4c49ba16dc50b/7.5.latest/en-US/443503fab977660be10000000a1553f6.html).

2.  Configure the Internet Communication Manager \(ICM\) to trust the system certificate for identity propagation.

    1.  Add a new SSL access point. See [Adding New SSL Access Points](https://help.sap.com/viewer/a42446bded624585958a36a71903a4a7/7.5.latest/en-US/eede34e6754f4caaa5f73f38d9bde3f7.html).

    2.  Generate a certificate signing request and send it to the CA of your choice. See [Configuration of the AS Java Keystore Views for SSL](https://help.sap.com/viewer/a42446bded624585958a36a71903a4a7/7.5.latest/en-US/4a0189458d863132e10000000a421937.html).

    3.  Import the certificates and save the configuration.

        Import the certificate signing response, the root X.509 certificate of the trusted CA, and the Cloud Connector's system certificate into the new SSL access point from step 2a. Save the configuration and restart the ICM. See [Configuring the SSL Key Pair and Trusted X.509 Certificates](https://help.sap.com/viewer/a42446bded624585958a36a71903a4a7/7.5.latest/en-US/4a0142abaee3088ce10000000a421937.html).

    4.  Make sure the ICM trusts the system certificate for identity propagation. For more information, see [Using Client Certificates via an Intermediary Server](https://help.sap.com/docs/SAP_NETWEAVER_750/e815bb97839a4d83be6c4fca48ee5777/ea301e3e6217b40be10000000a114084.html).

    5.  Restart the ICM and test the SSL connection. For more information, see [Testing the SSL Connection](https://help.sap.com/viewer/a42446bded624585958a36a71903a4a7/7.5.latest/en-US/c1435a3e740be946e10000000a114084.html).



<a name="task_a3h_34f_5mb"/>

<!-- task\_a3h\_34f\_5mb -->

## Define Rules for User Mapping



<a name="task_a3h_34f_5mb__steps-unordered_mv3_xpf_5mb"/>

## Procedure

1.  Add the *ClientCertLoginModule* to the policy configuration that the Cloud Connector connects to. See [Configuring the Login Module on the AS Java](https://help.sap.com/viewer/7ece2b41e5234afb98052b6ad1ab3e2f/7.5.latest/en-US/48fdbdca9a8d2b34e10000000a421937.html).

2.  Define the rules to map users authenticated with their certificate to users that exist in the User Management Engine. See [Using Rules for User Mapping in Client Certificate Login Module](https://help.sap.com/viewer/e815bb97839a4d83be6c4fca48ee5777/7.5.latest/en-US/fa1f542978c64072880136003fb6b2bf.html).

    -   To map the user ID of the certificate’s subject name field to users, see [Using Rules Based on Client Certificate Subject Names](https://help.sap.com/viewer/e815bb97839a4d83be6c4fca48ee5777/7.5.latest/en-US/4a48baeaba4b044ee10000000a421937.html).
    -   To map the user ID based on rules for the certificate V3 extension *SubjectAlternativeName*, see [Using Rules Based on Client Certificate V3 Extensions](https://help.sap.com/viewer/e815bb97839a4d83be6c4fca48ee5777/7.5.latest/en-US/44124b03e5735308e10000000a11466f.html).
    -   To use client certificate filters, see [Defining Rules for Filtering Client Certificates](https://help.sap.com/viewer/e815bb97839a4d83be6c4fca48ee5777/7.5.latest/en-US/4a409526f6011c67e10000000a42189c.html).


**Related Information**  


[Configuring Transport Layer Security on SAP NetWeaver AS for Java](https://help.sap.com/viewer/a42446bded624585958a36a71903a4a7/7.5.latest/en-US/4a015cc68d863132e10000000a421937.html)

[Using X.509 Client Certificates](https://help.sap.com/viewer/e815bb97839a4d83be6c4fca48ee5777/7.5.latest/en-US/4f991d85b10c16c7e10000000a42189d.html)

[Configure Identity Propagation for HTTPS](configure-identity-propagation-for-https-a8bb87a.md "Find step-by-step instructions to configure principal propagation to an ABAP server for HTTPS.")

