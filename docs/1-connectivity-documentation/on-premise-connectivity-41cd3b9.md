<!-- loio41cd3b916fcf49e28661d205a85b88cb -->

# On-Premise Connectivity

Use the transparent proxy for Kubernetes to set up connections of type `on-premise`.

The transparent proxy handles both HTTP and TCP communication protocols for on-premise destinations. As an application developer, you must create an SAP BTP destination of proxy type `OnPremise`, for example:

> ### Sample Code:  
> ```
> {
>     "Name": "example-dest-onprem",
>     "Type": "HTTP",
>     "ProxyType": "OnPremise",
>     "URL": "http://virtualhost:4321",
>     "Authentication": "PrincipalPropagation"
> }
> ```

To target the destination with name “example-dest-onprem” for handling by the transparent proxy, you should create the following Kubernetes resource in a namespace of your choice:



```
apiVersion: destination.connectivity.api.sap/v1
kind: Destination 
metadata: 
  name: example-dest 
spec:    
  destinationRef:
    name: "example-dest-onprem"
  destinationServiceInstanceName: dest-service-instance-example // can be ommited if config.destinationService.defaultInstanceName is provided 
```



After the transparent proxy executes successfully all necessary operations on the given SAP BTP destination, the status of the `destinations.destination.connectivity.api.sap` Kubernetes resource will be updated as shown below, and the DNS record "example-dest" will route to the configured URL in the destination:



```
apiVersion: destination.connectivity.api.sap/v1
kind: Destination 
metadata: 
  name: example-dest 
spec:  
  destinationRef:
    name: "example-dest-onprem"
  destinationServiceInstanceName: dest-service-instance-example // can be ommited if config.destinationService.defaultInstanceName is provided
status:    
  conditions:
  - lastUpdateTime: "2022-09-28T07:26:46Z"
    message: Transparent Proxy is configured and Kubernetes service with name "example-dest" is created.
    reason: ConfigurationSuccessful
    status: "True"
    type: Available 
```



Once done, the application can start consuming the destination from within the Kubernetes cluster, for example:

> ### Sample Code:  
> ```
> curl example-dest.<destination-cr-namespace>
> ```

> ### Note:  
> The namespace is optional if you have created the destination custom resource \(CR\) in the namespace of the application that will request it. For more information, see [Kubernetes Namespaces and DNS](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#namespaces-and-dns).



<a name="loio41cd3b916fcf49e28661d205a85b88cb__section_mmb_nyf_rtb"/>

## HTTP

Mandatory destination configuration fields:


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

`Name`

</td>
<td valign="top">

Destination name. Must be unique for the destination level and must contain only letters, numbers, or hyphen “-“.

</td>
</tr>
<tr>
<td valign="top">

`Type`

</td>
<td valign="top">

Destination type. Use HTTP for all HTTP\(S\) destinations.

</td>
</tr>
<tr>
<td valign="top">

`URL`

</td>
<td valign="top">

Virtual URL of the protected on-premise application.

</td>
</tr>
<tr>
<td valign="top">

`Authentication`

</td>
<td valign="top">

One of the listed authentication types in [HTTP Destinations](http-destinations-42a0e6b.md#loio42a0e6b966924f2e902090bdf435e1b2__config)

</td>
</tr>
<tr>
<td valign="top">

`ProxyType`

</td>
<td valign="top">

`Internet` or `OnPremise`

</td>
</tr>
</table>

Additional destination configuration fields:


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

`URL.connectionTimeoutInSeconds`

</td>
<td valign="top">

Period of time in which the HTTP client expects a confirmation after it initiated a new TCP connection.

It must be in the range of 1 second to 5 minutes\(300 seconds\).

> ### Note:  
> If you do not use it, the default value is 30 seconds. If you decide to use it, the total timeout of the initial request may be a bit longer than your chosen value, depending on the latency of calls to the Destination Service, which are needed to proxy the request.



</td>
</tr>
<tr>
<td valign="top">

`URL.socketReadTimeoutInSeconds`

</td>
<td valign="top">

Period of time the HTTP client will wait for receiving a response \(data\) from the server.

It must be in the range of 1 second to 12 hours \(43200 seconds\).

> ### Note:  
> If you do not use it, the default value is 30 seconds. If you decide to use it, the total timeout of the initial request may be a bit longer than your chosen value, depending on the latency of calls to the Destination Service, which are needed to proxy the request.



</td>
</tr>
<tr>
<td valign="top">

`URL.headers.<header-key>`

</td>
<td valign="top">

A static key prefix is used as a namespace grouping of the URL's HTTP headers. Its values are sent to the target endpoint. For each HTTP header's key, you must add a 'URL.headers' prefix separated by dot-delimiter.

For example:

> ### Sample Code:  
> ```
> {
>     ...
>     "URL.headers.<header-key-1>" : "<header-value-1>",
>     ...
>     "URL.headers.<header-key-N>": "<header-value-N>",
> }
> ```

> ### Caution:  
> If there are duplicate header keys passed from the request and contained in the destination, they are both added to the request against the target system.
> 
> > ### Sample Code:  
> > ```
> > {
> > /// other destination properties
> >   "URL.headers.foo": "bar"
> > }
> > ```
> 
> > ### Sample Code:  
> > ```
> > curl -H "foo: bar2" targetsystem -vvv
> > *   Trying <some ip>...
> > * Connected to targetsystem (<some ip>) port 80 (#0)
> > > GET / HTTP/1.1
> > > Host: targetsystem
> > > User-Agent: curl/7.84.0
> > > foo: bar2
> > > foo: bar
> > ```



</td>
</tr>
<tr>
<td valign="top">

`URL.queries.<query-key>`

</td>
<td valign="top">

A static key prefix is used as namespace grouping of the URL's query parameters. Their values are sent to the target endpoint. For each query parameter's key you must add to a 'URL.queries' prefix, separated by dot-delimiter.

For example:

> ### Sample Code:  
> ```
> {
>     ...
>     "URL.queries.<query-key-1>" : "<query-value-1>",
>     ...
>     "URL.queries.<query-key-N>": "<query-value-N>",
> }
> ```

> ### Caution:  
> If there are duplicate header keys passed from the request and contained in the destination, they are both added to the request against the target system.
> 
> > ### Sample Code:  
> > ```
> > {
> > /// other destination properties
> >   "URL.queries.foo": "bar"
> > }
> > ```
> 
> > ### Sample Code:  
> > ```
> > curl targetsystem?foo=bar2 // will result to the following final URL : targetsystem?foo=bar2&foo=bar
> > ```



</td>
</tr>
</table>



<a name="loio41cd3b916fcf49e28661d205a85b88cb__section_e5l_dzd_25b"/>

## TCP

Mandatory destination configuration fields:


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

`Name`

</td>
<td valign="top">

Destination name.

</td>
</tr>
<tr>
<td valign="top">

`Type`

</td>
<td valign="top">

Destination type. Use TCP.

</td>
</tr>
<tr>
<td valign="top">

`Address`

</td>
<td valign="top">

<destination\_host\>:<destination\_port\> of the protected on-premise application.

</td>
</tr>
<tr>
<td valign="top">

`ProxyType`

</td>
<td valign="top">

OnPremise

</td>
</tr>
</table>



<a name="loio41cd3b916fcf49e28661d205a85b88cb__section_bfk_hzd_25b"/>

## SOCKS5

The connectivity proxy provides a SOCKS5 proxy that you can use to access on-premise systems via TCP-based protocols. SOCKS5 is the industry standard for proxying TCP-based traffic. For more information, see [RFC 1928](https://www.ietf.org/rfc/rfc1928.txt).

The transparent proxy performs the SOCKS5 handshake with the [Connectivity Proxy](connectivity-proxy-for-kubernetes-e661713.md) to enable the out-of-the-box consumption of that \(otherwise complex\) functionality for the application developer.

For more information on how to directly set up the usage of the TCP protocol for cloud applications, see [Using the TCP Protocol for Cloud Applications](using-the-tcp-protocol-for-cloud-applications-cd15837.md).

