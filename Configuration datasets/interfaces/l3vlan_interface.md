# L3 VLAN interface

## URL

```
frinx-openconfig-interfaces:interfaces/interface/Vlan{{vlan_intf_id}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/interfaces/src/main/yang)

```javascript
{
    "interface": [
        {
            "name": "Vlan{{vlan_intf_id}}",
            "config": {
                "type": "iana-if-type:l3ipvlan",
                "enabled": {{vlan_enabled}},
                "name": "Vlan{{vlan_intf_id}}",
                "mtu": {{vlan_mtu}},
                "tpid": "{{vlan_tpid}}"
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
                            "index": 0,
                            "description": "{{vlan_description}}"
                        },
                        "vlan": {
                            "config": {
                                "vlan-id": {{vlan_id}}
                            }
                        },
                        "frinx-openconfig-if-ip:ipv4": {
                            "addresses": {
                                "address": [
                                    {
                                        "ip": "{{vlan_ip}}",
                                        "config": {
                                            "ip": "{{vlan_ip}}",
                                            "prefix-length": {{vlan_prefix}}
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

### Junos 14.1X53-D40.8

#### CLI

<pre>
set interfaces {{vlan_intf_id}} vlan-tagging
set interfaces {{vlan_intf_id}} unit 0 description {{vlan_description}}
set interfaces {{vlan_intf_id}} unit 0 vlan-id {{vlan_id}}
set interfaces {{vlan_intf_id}} unit 0 family inet address {{vlan_ip}}/{{vlan_prefix}}
</pre>

*vlan-tagging* is a conversion of {{vlan_tpid}} set *TPID_0X8100*  

### Dasan NOS SFU.RR.5.6p5

#### CLI

<pre>
interface br{{vlan_intf_id}}
 shutdown | no shutdown
 ip redirects | no ip redirects
 mtu {{vlan_mtu}}
 ip address {{vlan_ip}}/{{vlan_prefix}}
</pre>

*no shutdown* is a conversion of {{vlan_enabled}} set *true*  
*shutdown* is a conversion of {{vlan_enabled}} set *false*  
*no ip redirects* is a conversion of {{ip_redirect}} set *false*  
*ip redirects* is a conversion of {{ip_redirect}} set *true*  