# configure load-share on tunnel

## Create REST call

```
PUT
http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-mpls:mpls/

```
## Delete REST call

```
DELETE
http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-mpls:mpls/
```

## REST call body (required for create only)

```
{
    "mpls": [ 
        {
            "lsps": {
                "constrained-path": {
                    "tunnels": [
                        {
                             "config": {
                                     "name": <tunnel-id>
                             }
                             "bandwidth": {
                                 "config": {
                                      "set-bandwidth": <bandwidth>
                                 }
                             }
                        }
                    ]
                }
            }
        }
    ]
}
```


---

<pre>
interface tunnel-te &lt;tunnel-id&gt;
 load-share &lt;load-share&gt;
</pre>




