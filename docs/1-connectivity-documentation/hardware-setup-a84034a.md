<!-- loioa84034a36e154e8c9f7a8f238b4062d6 -->

# Hardware Setup

How to choose the right sizing for your Cloud Connector installation.

Regarding the hardware, we recommend that you use different setups for master and shadow. One dedicated machine should be used for the master, another one for the shadow. Usually, a shadow instance takes over the master role only temporarily. During most of its lifetime, in the shadow state, it needs less resources compared to the master.

If the master instance is available again after a downtime, we recommend that you switch back to the actual master.

> ### Note:  
> The sizing recommendations refer to the overall load across all subaccounts that are connected via the Cloud Connector. This means that you need to accumulate the expected load of all subaccounts and should not only calculate separately per subaccount \(taking the one with the highest load as basis\).

**Related Information**  


[Sizing for the Master Instance](sizing-for-the-master-instance-89e5122.md "Learn more about the basic criteria for the sizing of your Cloud Connector master instance.")

[Sizing for the Shadow Instance](sizing-for-the-shadow-instance-92224c0.md "Learn more about the basic criteria for the sizing of your Cloud Connector shadow instance (high availability mode).")

