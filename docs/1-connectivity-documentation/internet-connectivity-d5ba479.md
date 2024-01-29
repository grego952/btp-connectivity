<!-- loiod5ba479b79654bc8960c6891da304813 -->

# Internet Connectivity

Use the transparent proxy for Kubernetes to set up connections of type `Internet`.

The transparent proxy handles the HTTP\(s\) communication protocol for Internet destinations. As an application developer, you must create an SAP BTP destination of type `HTTP` and proxy type `Internet`, for example:

> ### Sample Code:  
> ```
> {
>     "Name": "example-dest-client-cert",
>     "Type": "HTTP",
>     "ProxyType": "Internet",
>     "URL": "https:/myapp.com",
>     "Authentication": "ClientCertificateAuthentication",
>     "KeyStorePassword": "Abcd1234",
>     "KeyStoreLocation": "cert.jks"
> } 
> ```

To target the destination with the name “example-dest-client-cert” for handling by the transparent proxy, you should create the following Kubernetes resource in a namespace of your choice:

```
apiVersion: destination.connectivity.api.sap/v1
kind: Destination 
metadata: 
  name: example-dest 
spec:   
  destinationRef:
    name: "example-dest-client-cert"
  destinationServiceInstanceName: dest-service-instance-example // can be ommited if config.destinationService.defaultInstanceName is provided
```

The transparent proxy monitors the available destinations in SAP BTP and compares them with the existing `destinations.destination.connectivity.api.sap` Kubernetes resources in the namespace where it is installed. Once a new SAP BTP destination is created for which a `destinations.destination.connectivity.api.sap` resource exists, the transparent proxy changes its configuration.



After the transparent proxy has executed successfully all necessary operations on the given SAP BTP destination, the status of the `destinations.destination.connectivity.api.sap` Kubernetes resource will be updated as shown below, and the DNS record "example-dest" will route to the configured URL in the destination:

```
apiVersion: destination.connectivity.api.sap/v1
kind: Destination 
metadata: 
  name: example-dest 
spec:  
  destinationRef:
    name: "example-dest-client-cert"
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



<a name="loiod5ba479b79654bc8960c6891da304813__section_mmb_nyf_rtb"/>

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

URL of the target endpoint.

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

Internet

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

