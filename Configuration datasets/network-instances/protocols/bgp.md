# Border Gateway Protocol (BGP)

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance/<ni-name>/protocols/protocol/frinx-openconfig-policy-types:BGP/<process-name>
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/bgp/src/main/yang)

```javascript
{
    "protocol": [
        {
            "name": "<proces-name>",
            "identifier": "frinx-openconfig-policy-types:BGP",
            "config": {
                "name": "<proces-name>",
                "identifier": "frinx-openconfig-policy-types:BGP"
            },
            "bgp": {
                "global": {
                    "config": {
                        "as": <as>
                    }
                },
                "neighbors": {
                    "neighbor": [
                        {
                            "neighbor-address": "<neighbor_address>",
                            "config": {
                                "neighbor-address": "<neighbor_address>",
                                "peer-as": <peer-as>,
                                "enabled": <true|false>
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

### Cisco IOS XR 5.3.4

#### CLI

---
<pre>
router bgp &lt;as&gt; instance &lt;process-name&gt;
 neighbor &lt;neighbor_address&gt;
   remote-as &lt;peer-as&gt;
   no shutdown
</pre>
---

*no shutdown* is conversion of *"enabled": true*
*shutdown* is conversion of *"enabled": false*

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [xr-unit]()

### Junos 15.1F-6.9

#### CLI

---
<pre>
activate protocols bgp group iBGP neighbor &lt;neighbor_address&gt;
</pre>
---

*activate* is conversion of *"enabled": true*
*deactivate* is conversion of *"enabled": false*

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit]()
