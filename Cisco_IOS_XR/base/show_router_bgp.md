# Show BGP process type/ID

## REST call

```
http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-network-instance:network-instance/network-instance/<ni-name>/protocols/protocol/BGP/<process-name>
```

## REST response body

```
{
    "protocol": {
        "identifier": "BGP"
        "name": <proces-name>
        "config": {
            "identifier": "BGP"
            "name": <proces-name>
        }
        "state": {
            "identifier": "BGP"
            "name": <proces-name>
        }
        "bgp": {
            "global": {
                "config": {
                     "router-id": <router-id>
                     "as": <proces-name>
                }
                "state": {
                     "router-id": <router-id>
                     "as": <proces-name>
                }
            }
        }
    }
}
```


---

<pre>
RP/0/0/CPU0:XR1#show run router bgp
Thu Jun  4 17:40:46.790 UTC

router bgp &lt;process-name&gt;
 router-id &lt;router-id&gt;
!
</pre>

---
