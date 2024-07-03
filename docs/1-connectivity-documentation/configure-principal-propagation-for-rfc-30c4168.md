<!-- loio30c416836a2e4466a10dbf36da9b5853 -->

# Configure Principal Propagation for RFC

Enable single sign-on \(SSO\) via RFC by forwarding the identity of cloud users to an on-premise system.



<a name="loio30c416836a2e4466a10dbf36da9b5853__section_hdk_pvt_wpb"/>

## Prerequisites

You have set up the Cloud Connector and the relevant backend system for principal propagation. For more informatioon, see [Configuring Principal Propagation](configuring-principal-propagation-c84d4d0.md).



<a name="loio30c416836a2e4466a10dbf36da9b5853__section_ix2_4vt_wpb"/>

## Procedure

-   Make sure your RFC destination is configured with `jco.destination.auth_type=PrincipalPropagation`. For more informatioon, see [User Logon Properties](user-logon-properties-8b1e1c3.md).

-   For your Java application, use an application router to forward a user token which is used by the Java Connector \(JCo\) for principal propagation. For more informatioon, see [Set Up an Application Router](set-up-an-application-router-b14eeb9.md).


