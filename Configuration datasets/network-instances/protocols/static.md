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
            "name": "default",
            "identifier": "frinx-openconfig-policy-types:STATIC",
            "config": {
                "name": "default",
                "identifier": "frinx-openconfig-policy-types:STATIC"
            },
            "afi-safis": {
                "afi-safi": [
                    "afi-safi-name": "{{static_afi_safi_name}}",
                    "config": {
                        "afi-safi-name": "{{static_afi_safi_name}}"
                    },
                    "routes": {
                        "route": [
                            {
                                "source-ip": "{{source_ip}}",
                                "config": {
                                    "source-ip": "{{source_ip}}",
                                    "prefix-length": {{prefix_length}}
                                },
                                "next-hops": {
                                    "next-hop": [
                                        {
                                            "ip": "{{next_hop_ip}}",
                                            "interface-name": "{{interface_name}}",
                                            "config": {
                                                "ip": "{{next_hop_ip}}",
                                                "interface-name": "{{interface_name}}",
                                                "tag": "{{tag_name}}"
                                            }
                                        }
                                    ]
                                }
                            }
                        ]
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
 address-family {{static_afi_safi_name}}
   {{source_ip}}/{{prefix_length}} {{interface_name}} {{next_hop_ip}} tag {{tag_name}}
</pre>
---

*ipv4 unicast*  is a conversion of {{static_afi_safi_name}} set *IPV4_UNICAST*  
*ipv6 unicast*  is a conversion of {{static_afi_safi_name}} set *IPV6_UNICAST*  
{{interface_name}} or {{next_hop_ip}} could be omitted by set to *null*

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/static)
