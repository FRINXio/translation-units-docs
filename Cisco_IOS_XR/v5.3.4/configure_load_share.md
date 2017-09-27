# configure load-share on tunnel

## Create REST call

```
PUT
http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-network-instance:network-instances/network-instance/<ni-name>/openconfig-mpls:mpls/lsps/constrained-path/tunnels/tunnel/<tunnel-id>
```
## Delete REST call

```
DELETE
http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-network-instance:network-instances/network-instance/<ni-name>/openconfig-mpls:mpls/lsps/constrained-path/tunnels/tunnel/<tunnel-id>
```

## REST call body (required for create only)

```
{
    "tunnel": {
	 "config": {
		 "name": <tunnel-id>
	 }
	 "bandwidth": {
	     "config": {
		  "set-bandwidth": <bandwidth>
	     }
	 }
    }
}
```


---

<pre>
interface tunnel-te &lt;tunnel-id&gt;
 load-share &lt;bandwidth&gt;
</pre>

---

## show REST call

```
GET
http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-network-instance:network-instances/network-instance/<ni-name>/openconfig-mpls:mpls/lsps/constrained-path/tunnels/tunnel/<tunnel-id>
```
