<!-- loio4c4b83b73f0242f8b336dcdc1bc3a02e -->

# Repository Configuration

JCo properties that allow you to define the behavior of the repository that dynamically retrieves function module metadata.

All properties below are optional. Alternatively, you can create the metadata in the application code, using the metadata factory methods within the `JCo` class, to avoid additional round-trips to the on-premise system.


<table>
<tr>
<th valign="top">

Property

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

`jco.destination.repository_destination`

</td>
<td valign="top">

Specifies which destination should be used for repository queries. If the destination does not exist, an error occurs when trying to retrieve the repository. Defaults to itself.

</td>
</tr>
<tr>
<td valign="top">

`jco.destination.repository.user`

</td>
<td valign="top">

Optional property. If this property is set, and the repository destination is not set, it is used as the user for repository queries. This configuration option allows using a different user for repository lookups with a single destination configuration, and restricting this user's permissions accordingly. See also SAP Note [460089](https://me.sap.com/notes/460089).

> ### Note:  
> When working with the *Destinations* editor in the cockpit, enter the value in the *<Repository User\>* field. Do not enter it as additional property.



</td>
</tr>
<tr>
<td valign="top">

`jco.destination.repository.passwd`

</td>
<td valign="top">

Represents the password for a repository user. If you use such a user, this property is mandatory.

> ### Note:  
> When working with the *Destinations* editor in the cockpit, enter this password in the *<Repository Password\>* field. Do not enter it as additional property.



</td>
</tr>
</table>

