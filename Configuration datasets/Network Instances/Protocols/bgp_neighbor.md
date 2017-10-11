# BGP neighbor configuration

## URL

```
openconfig-network-instance:network-instances/network-instance/<ni-name>/protocols/protocol/openconfig-policy-types:BGP/<process-name>
```

## OPENCONFIG YANG

```json
{
    "protocol": [
        {
            "name": <proces-name>,
            "identifier": "openconfig-policy-types:BGP",
            "config": {
                "name": <proces-name>,
                "identifier": "openconfig-policy-types:BGP"
            },
            "bgp": {
                "global": {
                    "config": {
                        "as": <as>,
                    }
                }
                "neighbors": {
                    "neighbor": [
                        {
                            "config": {
                                "neighbor-address": <neighbor_address>
                                "enabled": true
                            }
                        }
                    ]
                }
            }
        }
    ]
}
```


## OS Configuration Commands

#### Cisco IOS XR 5.4.3

---
<pre>
router bgp &lt;as&gt; instance &lt;process-name&gt;
 neighbor &lt;neighbor_address&gt;
   no shutdown
</pre>
---

#### Junos

---
<pre>
activate protocols bgp group iBGP neighbor &lt;neighbor_address&gt;
</pre>
---
