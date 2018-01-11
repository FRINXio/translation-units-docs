# Border Gateway Protocol (BGP)

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance/default/protocols/protocol/frinx-openconfig-policy-types:BGP/{{bgp_process_name}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/bgp/src/main/yang)

```javascript
{
    "protocol": [
        {
            "name": "{{bgp_process_name}}",
            "identifier": "frinx-openconfig-policy-types:BGP",
            "config": {
                "name": "{{bgp_process_name}}",
                "identifier": "frinx-openconfig-policy-types:BGP"
            },
            "bgp": {
                "global": {
                    "config": {
                        "as": {{bgp_as}}
                    }
                },
                "neighbors": {
                    "neighbor": [
                        {
                            "neighbor-address": "{{neighbor_ip}}",
                            "config": {
                                "neighbor-address": "{{neighbor_ip}}",
                                "peer-group": "{{bgp_group}}",
                                "peer-as": {{bgp_peer_as}},
                                "enabled": {{neighbor_enabled}}
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
router bgp {{bgp_as}} instance {{bgp_process_name}}
 neighbor {{neighbor_ip}}
   remote-as {{bgp_peer_as}}
   use neighbor-group {{bgp_group}}
   no shutdown | shutdown
</pre>
---

*no shutdown* is a conversion of {{neighbor_enabled}} set *true*    
*shutdown* is a conversion of {{neighbor_enabled}} set *false*  

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/bgp)

### Junos 17.3R1.10

#### CLI

---
<pre>
activate protocols bgp group &lt;group&gt; neighbor &lt;neighbor_address&gt;
</pre>
---

*activate* is a conversion of {{neighbor_enabled}} set *true*    
*deactivate* is a conversion of {{neighbor_enabled}} set *false*  

##### Unit

NOT IMPLEMENTED

Link to github : [junos-unit]()
