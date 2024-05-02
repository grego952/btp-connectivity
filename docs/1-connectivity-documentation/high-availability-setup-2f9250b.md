<!-- loio2f9250b0e6ac488286266461a82518e8 -->

# High Availability Setup

You can operate the Cloud Connector in a high availability mode, in which a master and a shadow instance are installed.



## Context

In a failover setup, when the main instance should go down for some reason, a redundant one can take over its role. The main instance of the Cloud Connector is called **master** and the redundant instance is called the **shadow**. The shadow must be installed separately and connected to the master.

During high availability setup, the master pushes the entire configuration to the shadow. Later on, during normal operation, the master also pushes configuration updates to the shadow to keep both instances synchronized. The shadow pings the master regularly. If the master is not reachable for a while, the shadow takes over the master role and establishes the tunnel to SAP BTP.

> ### Caution:  
> Master and shadow communicate outside the cloud \(SAP BTP\). Therefore, a communication breakdown between master and shadow may trigger a takeover although the original master is still operational, and in particular still connected to SAP BTP.
> 
> This may lead to a temporary *double-master* scenario that will be rectified as soon as both instances reestablish communication. During the blackout between the original master and the shadow that became the actual master instance, and the ensuing master-master situation, the behavior is undefined and may lead to issues.
> 
> It is therefore imperative to choose a **stable and reliable network environment** for the master and shadow instances.

> ### Note:  
> For detailed information about sizing of the master and the shadow instance, see also [Sizing Recommendations](sizing-recommendations-f008494.md).

**Related Information**  


[Install a Failover Instance for High Availability](install-a-failover-instance-for-high-availability-c697705.md "Install a redundant Cloud Connector instance (shadow instance) that monitors the main instance.")

[Master and Shadow Administration](master-and-shadow-administration-7f57de1.md "Manage the Cloud Connector master and shadow instances in a high availability setup.")

