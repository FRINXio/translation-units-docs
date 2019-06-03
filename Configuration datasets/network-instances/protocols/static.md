# Static Route

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance/default/protocols/protocol/frinx-openconfig-policy-types:STATIC
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/static/src/main/yang)

```javascript
{
    "protocol":[
        { 
            "identifier": "frinx-openconfig-policy-types:STATIC",
            "config": {
                "identifier": "frinx-openconfig-policy-types:STATIC"
            },
            "static-routes": {
                "static": [
                    {
                        "prefix": "{{static_route_prefix}}",
                        "config": {
                            "prefix": "{{static_route_prefix}}",
                            "afi-safi-type": "{{afi_safi_type}}",
                            "set-tag": "{{tag_id}}"
                        },
                        "next-hops": {
                            "next-hop": [
                                {
                                    "index": "{{next_hop_index}}",
                                    "config": {
                                        "index": "{{next_hop_index}}",
                                        "next-hop": "{{next_hop_ip}}"
                                    },
                                    "interface-ref": {
                                        "config": {
                                            "interface": "{{next_hop_ifc_name}}",
                                            "subinterface": "{{next_hop_subifc_idx}}"
                                        }
                                    }
                                }
                            ]
                        }
                    }
                ]
            }
        }
    ]
}
```


## OS Configuration Commands

### Cisco IOS XR 6.6.2

#### CLI

---
<pre>
router static
 address-family {{afi_safi_name}}
   {{prefix_ip}}/{{prefix_length}} {{next_hop_ifc_name}}.{{next_hop_subifc_idx}} {{next_hop_ip}} tag {{tag_id}}
</pre>
---

*ipv4 unicast*  is a conversion of {{afi_safi_type}} set *IPV4_UNICAST*  
*ipv6 unicast*  is a conversion of {{afi_safi_type}} set *IPV6_UNICAST*  
{{prefix_ip}} is parsed from {{static_route_prefix}}  
{{prefix_length}} is parsed from {{static_route_prefix}}  

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/static)
