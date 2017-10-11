# configure LAG bundle member

## URL

```
http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-interfaces:interfaces/interface/<intf-id>
```

## OPENCONFIG YANG

```json
{
    "interface": [
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
    ]
}

TODO: add dampening and load-interval, also specify mode active

```

## OS Configuration Commands

#### Cisco IOS XR 5.4.3
---
<pre>
interface &lt;intf-id&gt;
 bundle-id &lt;bundle-id&gt; mode active
 carrier-delay up &lt;up-value&gt; down &lt;down-value&gt;
 load-interval &lt;interval&gt;
 dampening
</pre>
---

#### Junos

---
<pre>
TODO
</pre>
---




