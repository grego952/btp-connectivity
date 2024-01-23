<!-- loio4c8f678d84b94dfe9af539d040259837 -->

# Secure the Activation of Traffic Traces

For support purposes, you can trace HTTP and RFC network traffic that passes through the Cloud Connector.



## Context

Traffic data may include business-critical information or security-sensitive data, such as user names, passwords, address data, credit card numbers, and so on. Thus, by activating the corresponding trace level, a Cloud Connector administrator might see data that he or she is not meant to. To prevent this behavior, implement the four-eyes principle for your operating system as described below.

Once the four-eyes principle is applied, activating a trace level that dumps traffic data will require two separate users:

-   An operating system user on the machine where the Cloud Connector is installed;
-   An `Administrator` user of the Cloud Connector user interface.

By assigning these roles to two different people, you can ensure that both persons are needed to activate a traffic dump.



## Four-Eyes Principle for Microsoft Windows OS

1.  Create a file named `writeHexDump` in `<scc_install_dir>\scc_config`. The owner of this file must be a user other than the operating system user who runs the `cloud connector` process.

    > ### Note:  
    > Usually, this file owner is the user which is specified in the *Log On* tab in the properties of the `cloud connector` service \(in the Windows *Services* console\). We recommend that you do not use the *Local System* user, but a dedicated OS user for the `cloud connector` service.

    -   Only the file owner should have write permission for the file.
    -   The OS user who runs the `cloud connector` process needs read-only permissions for this file.
    -   Initially, the file should contain a line like `allowed=false`.
    -   In the security properties of the file `scc_config.ini`\(same directory\), make sure that only the OS user who runs the `cloud connector` process has write/modify permissions for this file. The most efficient way to do this is simply by removing all other users from the list.

2.  Once you've created this file, the Cloud Connector refuses any attempt to activate the *Payload Trace* or *SNC Payload Trace* flag.
3.  To set CPIC trace level 3 or activate any payload trace, first the owner of `writeHexDump` must change the file content from `allowed=false` to `allowed=true`. Thereafter, the *Administrator* user can activate any payload trace from the Cloud Connector administration screens.



## Four-Eyes Principle for Linux OS/Mac OS X

1.  Go to directory */opt/sap/scc/scc\_config* and create a file with name `writeHexDump`. The owner of this file must be different from the *scctunnel* user \(that is, the operating system user under which the Cloud Connector processes are running\) and not a member of the operating system user group *sccgroup*.
    -   Only the file owner should have write permission for the file.
    -   The `scctunnel` user needs read-only permissions for this file.
    -   Initially, the file should contain a line like `allowed=false`.

2.  Once you've created this file, the Cloud Connector refuses any attempt to activate the *Payload Trace* or *SNC Payload Trace* flag.
3.  To set CPIC trace level 3 or activate any payload trace, first the owner of the `writeHexDump` file mentioned above must change the file content from `allowed=false` to `allowed=true`. Then, the *Administrator* user can activate any payload trace from the Cloud Connector administration screens.

