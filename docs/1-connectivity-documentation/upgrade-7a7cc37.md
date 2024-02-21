<!-- loio7a7cc373019b4b6eaab39b5ab7082b09 -->

# Upgrade

Upgrade your Cloud Connector and avoid connectivity downtime during the update.

The steps for upgrading your Cloud Connector are specific to the operating system that you use. Previous settings and configurations are automatically preserved.

> ### Caution:  
> Upgrade is supported only for *installer* versions, not for *portable* versions, see [Installation](installation-57ae3d6.md). Before upgrading, please check the [Prerequisites](prerequisites-e23f776.md) and make sure your environment fits the new version. We recommend that you create a [Configuration Backup](configuration-backup-abd1ba7.md) before starting an upgrade.



## Avoid Connectivity Downtime

If you have a single-machine Cloud Connector installation, a short downtime is unavoidable during the upgrade process. However, if you have set up a master and a shadow instance, you can perform the upgrade without downtime by executing the following procedure:

1.  Shut down the shadow instance.
2.  Perform the upgrade on the shadow instance. \(Follow the relevant procedure below.\)
3.  Restart the shadow instance and wait until it has connected to the master instance.
4.  Perform a *Switch Roles* operation by pressing the corresponding button in the master administration UI. The master instance has now changed into a shadow instance.

    > ### Caution:  
    > After upgrading the former shadow instance from a version prior to 2.13 and having switched its role to be the new master instance, reset high availability settings in *both* instances *now*, before continuing to upgrade the second instance from a version prior to 2.13 as well. The master-shadow connection must be re-established after both instances have been upgraded from versions prior to 2.13 to versions 2.13 or higher.

5.  Shut down the new shadow instance and perform the upgrade procedure on it as well.
6.  Restart the new shadow instance and wait until it has connected to the already upgraded current master instance.
7.  Perform again the *Switch Roles* operation if you want the previous master instance to act as the new master instance again.

**Result**: Both instances have now been upgraded without connectivity downtime and without configuration loss.

For more information, see [Install a Failover Instance for High Availability](install-a-failover-instance-for-high-availability-c697705.md).



## Microsoft Windows OS

1.  Uninstall the Cloud Connector as described in [Uninstallation](uninstallation-d53395c.md) and make sure to retain the existing configuration.
2.  Reinstall the Cloud Connector within the same directory. For more information, see [Installation on Microsoft Windows OS](installation-on-microsoft-windows-os-204aaad.md).
3.  Before accessing the administration UI, clear your browser cache to avoid any unpredictable behavior due to the upgraded UI.



## Linux OS

1.  Execute the following command: :

    ```
    rpm -U com.sap.scc-ui-<version>.rpm
    ```

    > ### Note:  
    > **Daemon extensions**
    > 
    > All extensions to the daemon provided via `scc_daemon_extension.sh` mechanism will survive a version update. An upgrade to version 2.12.3 will already consider an existing file, even though previous versions were not supporting that feature.

2.  Before accessing the administration UI, clear your browser cache to avoid any unpredictable behavior due to the upgraded UI.

