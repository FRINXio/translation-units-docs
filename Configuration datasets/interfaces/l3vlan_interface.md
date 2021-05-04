# L3 VLAN interface

## URL

```
frinx-openconfig-interfaces:interfaces/interface={{vlan_ifc_name}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/interfaces/src/main/yang)

```javascript
{
    "interface": [
        {
            "name": "{{vlan_ifc_name}}",
            "config": {
                "type": "iana-if-type:l3ipvlan",
                "enabled": {{vlan_enabled}},
                "name": "{{vlan_ifc_name}}",
                "mtu": {{vlan_mtu}}
            },
            "frinx-l3ipvlan:l3ipvlan":  {
                "config": {
                    "ip-redirects": {{ip_redirect}}
                }
            },
            "subinterfaces": {
                "subinterface": [
                    {
                        "index": 0,
                        "config": {
                            "index": 0
                        },
                        "frinx-openconfig-if-ip:ipv4": {
                            "addresses": {
                                "address": [
                                    {
                                        "ip": "{{vlan_ip}}",
                                        "config": {
                                            "ip": "{{vlan_ip}}",
                                            "prefix-length": {{vlan_prefix_length}}
                                        }
                                    }
                                ]
                            }
                        }
                    }
                ]
            }
        }
    ]
}
```

## OS Configuration Commands

### Dasan NOS SFU.RR.5.6p5

#### CLI

<pre>
interface br{{vlan_ifc_id}}
 shutdown | no shutdown
 ip redirects | no ip redirects
 mtu {{vlan_mtu}}
 ip address {{vlan_ip}}/{{vlan_prefix_length}}
</pre>

{{vlan_ifc_id}} is parsed from {{vlan_ifc_name}}  
example {{vlan_ifc_name}} is Vlan10 -&gt; {{vlan_ifc_id}} is 10  

*no shutdown* is a conversion of {{vlan_enabled}} set *true*  
*shutdown* is a conversion of {{vlan_enabled}} set *false*  
*no ip redirects* is a conversion of {{ip_redirect}} set *false*  
*ip redirects* is a conversion of {{ip_redirect}} set *true*  


##### Unit

Link to github : [dasan-unit](https://github.com/FRINXio/cli-units/tree/master/dasan/interface)
