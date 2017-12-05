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
                                "peer-group": "<group>",
                                "peer-as": <peer-as>,
                                "enabled": <true|false>
                            }
                        }
                    ]
                }
                "peer-groups": {
                    "peer-group": [
                        {
                            "peer-group-name": "<group>",
                            "config": {
                                "peer-group-name": "<group>",
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
 neighbor-group &lt;group&gt;
 neighbor &lt;neighbor_address&gt;
   remote-as &lt;peer-as&gt;
   use neighbor-group &lt;group&gt;
   no shutdown
</pre>
---

*no shutdown* is conversion of *"enabled": true*  
*shutdown* is conversion of *"enabled": false*

##### Unit

Unit version range: 3.1.1.rc5

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/bgp)

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
