# configure BGP neighbor

## Create REST call

```
PUT
http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-bgp:bgp

```
## Delete REST call

```
DELETE
http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-bgp:bgp
```

## REST call body (required for create only)

```
{
    "bgp": [
        {
            "neighbors": [
                {
                    "config": {
                        "neighbor-address": "<neighbor_address>"
                    }
                }
            "global": {
                "config": {
                    "as": "<as_number>",
                    ## "router-id": "<router-id>",
                }
            }
        }
    ]
}
```


---

<pre>
router bgp &l;tas&gt;
 neighbor &lt;neighbor_address&gt;
   no shutdown
</pre>




