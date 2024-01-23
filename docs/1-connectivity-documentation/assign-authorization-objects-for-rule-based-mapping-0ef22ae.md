<!-- loio0ef22ae41b154cd5b78d6e04186a3ca3 -->

# Assign Authorization Objects for Rule-based Mapping

Assign authorizations to access transaction CERTRULE.

To access transaction CERTRULE, you need the following authorizations:

-   CC control center: System administration \(S\_RZL\_ADM\)
    -   `Activity 03` grants display authorizations.
    -   `Activity 01` grants change authorizations.

-   User Master Maintenance: User Groups \(S\_USER\_GRP\)
    -   `Activity 03` grants display authorizations.
    -   `Activity 02` grants change authorizations.
    -   `Class`: enter the names of user groups for which the administrator can maintain explicit mappings.


To assign these authorization objects, proceed as follows:

1.  Create a *Single Role* using transaction PFCG.
2.  To add the authorization objects `S_RZL_ADM` and `S_USER_GRP`, go to the *Authorizations* tab, choose *Change Authorization data* and select the *Manually* button .
3.  To generate the profile, choose *Generate* and save the changes.
4.  In the *User* tab, enter the user who should execute the transaction CERTRULE.
5.  To match the generated profile to the users, choose *User comparison* .

