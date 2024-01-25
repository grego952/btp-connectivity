<!-- loiodaa547fae1f4402e9a0b6d82da9f007a -->

# Logon to the Cloud Connector via Client Certificate

Switch from default logon to client certificate logon to access the Cloud Connector.

> ### Restriction:  
> Limitation for Cloud Connector version 2.16.0: This feature does not work if *high availability* setup is active. A Cloud Connector shadow instance cannot connect due to missing trust with error: *There is no trust with Cloud Connector on https://<host\>:<port\>. Reset shadow configuration and try to connect shadow again*.

> ### Restriction:  
> Configuring the logon with a certificate is not allowed for SAP-operated Cloud Connectors, for example in the context of *Enterprise Cloud Services* or *S/4HANA Private Cloud Edition*.

Instead of authenticating with user and password as configured by default \(see [Initial Configuration](initial-configuration-db9170a.md)\), you can switch to client certificate authentication and logon. To do so, choose *Configuration* \(or *Shadow Configuration*\) from the main menu, and tab *User Interface*, section *Authentication*.

![](images/SCC_Logon_to_the_Cloud_Connector_with_a_Client_Certificate_1_8c7b9a2.png)

In the next prompt, specify an object identifier \(OID\) to extract the user name from subject of any given client certificate.

![](images/SCC_Logon_to_the_Cloud_Connector_with_a_Client_Certificate_2_39b7a67.png)

You must add at least one CA certificate to the *Authentication Allowlist*. These certificates are used by Cloud Connector to validate an incoming client certificate. Typically, these are the root or issuer certificates of eligible client certificates, or the client certificates themselves if they are self-signed.

After activation, a restart is required.

The login works as follows:

1.  \(Prerequisite\): Your browser \(or your REST client\) must provide a suitable client certificate. In particular, the user extracted from such a client certificate as per the selected *User Mapping \(OID\)* must be a member of the current user store \(local or LDAP\).
2.  When accessing the Cloud Connector, an mTLS handshake is performed, that is, the Cloud Connector checks your selected client certificate against the CAs from the authentication allowlist.

    > ### Caution:  
    > If your client certificate is not self-signed, you must provide \(one of\) the issuer certificates in the *authentication allowlist*, not the client certificate from your browser.

3.  If trust can be established, the Cloud Connector extracts the user from the subject as per the specified user mapping OID. This user will be logged on if it can be found in the current user store. If LDAP is used, the respective roles are checked and assigned.

If you select, for example, *CN* as OID, and have a client certificate with a subject containing *CN=Administrator*, the user *Administrator* is used after mutual trust was established.

