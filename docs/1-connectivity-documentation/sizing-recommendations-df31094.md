<!-- loiodf31094259054c64a2c206166292d2fd -->

# Sizing Recommendations

When installing a transpartent proxy for Kubernetes, the first thing you need to decide is the sizing of the installation.



<a name="loiodf31094259054c64a2c206166292d2fd__section_ds4_4xm_t5b"/>

## Overview

To get the most out of the transparent proxy, you must configure it in a suitable way, fitting the scenarios in which it plays a role.



<a name="loiodf31094259054c64a2c206166292d2fd__section_gq3_pxm_t5b"/>

## Sizing Options

The following table gives basic sizing guidance. The values listed in the `CPU`, `Memory` and sections correspond to the properties, which should be defined in the `values.yaml`. For more information, see [Configuration Guide](configuration-guide-2a22cd7.md):

**HTTP Proxy Sizing**


<table>
<tr>
<th valign="top">

Size

</th>
<th valign="top">

CPU

</th>
<th valign="top">

Memory

</th>
</tr>
<tr>
<td valign="top">

S:

The expected load is small - request concurrency and size are low

</td>
<td valign="top">

-   `deployment.resources.http.requests.cpu: 0.2`
-   `deployment.resources.http.limits.cpu: 0.4`



</td>
<td valign="top">

-   `deployment.resources.http.requests.memory: 256 M`
-   `deployment.resources.http.limits.memory: 512 M`



</td>
</tr>
<tr>
<td valign="top">

M:

The expected load is medium - request concurrency and size are medium

</td>
<td valign="top">

-   `deployment.resources.http.requests.cpu: 0.4`
-   `deployment.resources.http.limits.cpu: 0.8`



</td>
<td valign="top">

-   `deployment.resources.http.requests.memory: 512 M`
-   `deployment.resources.http.limits.memory: 1024 M`



</td>
</tr>
<tr>
<td valign="top">

L:

The expected load is large - request concurrency and size are medium or high

</td>
<td valign="top">

-   `deployment.resources.http.requests.cpu: 0.8`
-   `deployment.resources.http.limits.cpu: 1.6`



</td>
<td valign="top">

-   `deployment.resources.http.requests.memory: 1024 M`
-   `deployment.resources.http.limits.memory: 2048 M`



</td>
</tr>
</table>

**TCP Proxy Sizing**


<table>
<tr>
<th valign="top">

Size

</th>
<th valign="top">

CPU

</th>
<th valign="top">

Memory

</th>
</tr>
<tr>
<td valign="top">

S:

The expected load is small - request concurrency and size are low

</td>
<td valign="top">

-   `deployment.resources.tcp.requests.cpu: 0.05`
-   `deployment.resources.tcp.limits.cpu: 0.1`



</td>
<td valign="top">

-   `deployment.resources.tcp.requests.memory: 32 M`
-   `deployment.resources.tcp.limits.memory: 64 M`



</td>
</tr>
<tr>
<td valign="top">

M:

The expected load is medium - request concurrency and size are medium

</td>
<td valign="top">

-   `deployment.resources.tcp.requests.cpu: 0.1`
-   `deployment.resources.tcp.limits.cpu: 0.2`



</td>
<td valign="top">

-   `deployment.resources.tcp.requests.memory: 64 M`
-   `deployment.resources.tcp.limits.memory: 128 M`



</td>
</tr>
<tr>
<td valign="top">

L:

The expected load is large - request concurrency and size are medium or high

</td>
<td valign="top">

-   `deployment.resources.tcp.requests.cpu: 0.2`
-   `deployment.resources.tcp.limits.cpu: 0.4`



</td>
<td valign="top">

-   `deployment.resources.tcp.requests.memory: 128 M`
-   `deployment.resources.tcp.limits.memory: 256 M`



</td>
</tr>
</table>

> ### Note:  
> **Relation to Connectivity Proxy**
> 
> The above-mentioned sizing recommendations for the TCP proxies are related to the connectivity proxy software component, which also acts as a tunnel server to the on-premise systems it connects to. This means that the connectivity proxy has to be properly sized as well, see [Sizing Recommendations](sizing-recommendations-204822a.md) \(connectivity proxy for Kubernetes\).

> ### Note:  
> **General Note**
> 
> These sizing recommendations are just a direction point. There are many factors that affect the performance offered by the transparent proxy, related to the specifics of your concrete scenarios, expected regular and intermittent load, and so on.

