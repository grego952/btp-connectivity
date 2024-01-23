<!-- loio88efb23f2fc145f590eb1e4dcc09137a -->

# Network Zones

Choosing a network zone for the Cloud Connector installation.

A company network is usually divided into multiple network zones according to the security level of the contained systems. The DMZ network zone contains and exposes the external-facing services of an organization to an untrusted network, typically the Internet. Besides this, there can be one or multiple other network zones which contain the components and services provided in the company’s intranet.

You can set up the Cloud Connector either in the DMZ or in an inner network zone. Technical prerequisites for the Cloud Connector to work properly are:

-   The Cloud Connector must have access to the SAP BTP landscape host, either directly or via HTTPS proxy \(see also: [Prerequisites](prerequisites-e23f776.md)\).
-   The Cloud Connector must have direct access to the internal systems it shall provide access to. I.e. there must be transparent connectivity between the Cloud Connector and the internal system.

It’s a company’s decision, whether the Cloud Connector is set up in the DMZ and operated centrally by an IT department or set up in the intranet and operated by the line of business.

**Related Information**  


[Network Zones](network-zones-7b9d90c.md "Choose a network zone for your Cloud Connector installation.")

