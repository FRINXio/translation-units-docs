# configure LAG bundle member

## Create REST call

```
PUT
http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-interfaces:interfaces/interface/<intf-id>/config
```

## REST call body 

```
{
    "config": {
        "type": "iana-if-type:ieee8023adLag",
        "enabled": true,
        "name": "<intf-id>"
    }
    "aggregation": {
        "config": {
            "lag-type": LACP
        }
    }
    "hold-time": {
        "config": {
            "up": <up-value>
            "down": <down-value>
        }  
    }
}
```

---

<pre>
interface &lt;intf-id&gt;
 bundle-id &lt;bundle-id&gt; mode active
 carrier-delay up &lt;up-value&gt; down &lt;down-value&gt;
 load-interval &lt;interval&gt;
 dampening
</pre>



