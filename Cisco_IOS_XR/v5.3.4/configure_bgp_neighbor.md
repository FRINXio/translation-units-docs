# configure BGP neighbor

## Create REST call

```
PUT
http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-network-instance:network-instances/network-instance/<ni-name>/protocols/protocol/openconfig-bgp:bgp
```
## Delete REST call

```
DELETE
http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-network-instance:network-instances/network-instance/<ni-name>/protocols/protocol/openconfig-bgp:bgp
```

## REST call body (required for create only)

```
{
    "bgp": {
        "global": {
            "config": {
                "as": "<as>",
            }
        }
        "neighbors": {
            "neighbor": [
                {
                    "config": {
                        "neighbor-address": "<neighbor_address>"
                    }
                }
            ]
        }
    }
}

```


---

<pre>
router bgp &lt;as&gt;
 neighbor &lt;neighbor_address&gt;
   no shutdown
</pre>

---

## show REST call

```
GET
http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-network-instance:network-instances/network-instance/<ni-name>/protocols/protocol/openconfig-bgp:bgp
```
