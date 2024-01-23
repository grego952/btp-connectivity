<!-- loio7c3b53187cc14eac9517aafec30c38df -->

# Release and Maintenance Strategy

Find information about SAP BTP Connectivity releases, versioning and upgrades.



<a name="loio7c3b53187cc14eac9517aafec30c38df__section_c1w_fp5_ggb"/>

## Release Cycles

Updates of the Connectivity service are published as required, within the regular, bi-weekly SAP BTP release cycle. 

New releases of the Cloud Connector are published when new features or important bug fixes are delivered, available on the [Cloud Tools](https://tools.hana.ondemand.com/#cloud) page.



<a name="loio7c3b53187cc14eac9517aafec30c38df__section_fxy_fp5_ggb"/>

## Cloud Connector Versions

Cloud Connector versions follow the `<major>.<minor>.<micro>` versioning schema. The Cloud Connector stays fully compatible within a major version. Within a minor version, the Cloud Connector will stay with the same feature set. Higher minor versions usually support additional features compared to lower minor versions. Micro versions generally consist of patches to a `<master>.<minor>` version to deliver bug fixes.

For each supported major version of the Cloud Connector, only one `<major>.<minor>.<micro>` version will be provided and supported on the Cloud Tools page. This means that users must upgrade their existing Cloud Connectors to get a patch for a bug or to make use of new features.

For detailed support strategy information, check SAP note [3302250](https://me.sap.com/notes/3302250).



<a name="loio7c3b53187cc14eac9517aafec30c38df__section_gb1_gp5_ggb"/>

## Cloud Connector Upgrade

New versions of the Cloud Connector are announced in the [Release Notes](https://help.sap.com/doc/43b304f99a8145809c78f292bfc0bc58/Cloud/en-US/98bf747111574187a7c76f8ced51cfeb.html?sel1=Connectivity) of SAP BTP. We recommend that Cloud Connector administrators regularly check the release notes for Cloud Connector updates. New versions of the Cloud Connector can be applied by using the Cloud Connector upgrade capabilities. For more information, see [Upgrade](upgrade-7a7cc37.md).

> ### Note:  
> We recommend that you first apply upgrades in a test landscape to validate that the running applications are working.

There are no manual user actions required in the Cloud Connector when the SAP BTP is updated.

