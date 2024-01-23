<!-- loio7b9d90cb3049445c9b4454c6c044cc62 -->

# Network Zones

Choose a network zone for your Cloud Connector installation.

A customer network is usually divided into multiple network zones or subnetworks according to the security level of the contained components. For example, the DMZ that contains and exposes the external-facing services of an organization to an untrusted network, usually the Internet, and there are one or more other network zones which contain the components and services provided in the company’s intranet.

You can generally choose the network zone in which to set up the Cloud Connector:

-   Internet access to the SAP BTP region host, either directly or via HTTPS proxy.
-   Direct access to the internal systems it provides access to, which means that there is transparent connectivity between the Cloud Connector and the internal system.

The Cloud Connector can be set up either in the DMZ and operated centrally by the IT department, or set up in the intranet and operated by the appropriate line of business.

> ### Note:  
> The internal network must allow access to the required ports; the specific configuration depends on the firewall software used.
> 
> The default ports are `80` for HTTP and `443` for HTTPS. For RFC communication, you need to open a gateway port \(default: `33+<instance number>` and an arbitrary message server port. For a connection to a HANA Database \(on SAP BTP\) via JDBC, you need to open an arbitrary *outbound* port in your network. Mail \(SMTP\) communication is not supported.

