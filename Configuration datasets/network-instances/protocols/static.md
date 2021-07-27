# Static Route

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance=default/protocols/protocol=frinx-openconfig-policy-types%3ASTATIC,default
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/local-routing/src/main/yang)

```javascript
{
    "protocol":[
        { 
            "identifier": "frinx-openconfig-policy-types:STATIC",
            "name": "default",
            "config": {
                "identifier": "frinx-openconfig-policy-types:STATIC",
                "name": "default"
            },
            "static-routes": {
                "static": [
                    {
                        "prefix": "{{static_route_prefix}}",
                        "config": {
                            "prefix": "{{static_route_prefix}}",
                            "frinx-local-routing-extension:afi-safi-type": "{{afi_safi_type}}"
                        },
                        "next-hops": {
                            "next-hop": [
                                {
                                    "index": "{{next_hop_index}}",
                                    "config": {
                                        "index": "{{next_hop_index}}",
                                        "next-hop": "{{next_hop_ip}}",
                                        "frinx-local-routing-extension:set-tag": "{{nh_tag_id}}"
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

### IOS 12

#### CLI

<pre>
router static
 address-family {{afi_safi_name}}
   {{prefix_ip}}/{{prefix_length}} {{next_hop_ifc_name}}.{{next_hop_subifc_idx}} {{next_hop_ip}} tag {{nh_tag_id}}
</pre>

*ipv4 unicast*  is a conversion of {{afi_safi_type}} set *IPV4_UNICAST*  
*ipv6 unicast*  is a conversion of {{afi_safi_type}} set *IPV6_UNICAST*  
{{prefix_ip}} is parsed from {{static_route_prefix}}  
{{prefix_length}} is parsed from {{static_route_prefix}} 

##### Unit

Link to github : [ios-unit](https://github.com/FRINXio/cli-units/tree/master/ios/interface)

### Cisco IOS XR 6.6.2

#### CLI

---
<pre>
router static
 address-family {{afi_safi_name}}
   {{prefix_ip}}/{{prefix_length}} {{next_hop_ifc_name}}.{{next_hop_subifc_idx}} {{next_hop_ip}} tag {{nh_tag_id}}
</pre>
---

*ipv4 unicast*  is a conversion of {{afi_safi_type}} set *IPV4_UNICAST*  
*ipv6 unicast*  is a conversion of {{afi_safi_type}} set *IPV6_UNICAST*  
{{prefix_ip}} is parsed from {{static_route_prefix}}  
{{prefix_length}} is parsed from {{static_route_prefix}}  

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/lr)
