# Show BGP process type/ID

## REST call

```
http://localhost:8181/restconf/operational/network-topology:network-topology/topology/unified/node/<node-id>/yang-ext:mount/openconfig-network-instance:network-instances/network-instance/<ni-name>/protocols/protocol/openconfig-policy-types:BGP/<process-name>
```

## REST response body

```
{
    "protocol": [
        {
            "name": <proces-name>,
            "identifier": "openconfig-policy-types:BlGP",
            "config": {
                "name": <proces-name>,
                "identifier": "openconfig-policy-types:BGP"
            },
            "bgp": {
                "global": {
                    "config": {
                        "as": <as>,
                        "router-id": <router-id>
                    }
                }
            },
            "state": {
                "name": <proces-name>,
                "identifier": "openconfig-policy-types:BGP"
            }
        }
    ]
}
```


---

<pre>
RP/0/0/CPU0:XR1#show run router bgp
Thu Jun  4 17:40:46.790 UTC

router bgp &lt;as&gt; instance &lt;process-name&gt;
 bgp router-id &lt;router-id&gt;
!
</pre>

---
