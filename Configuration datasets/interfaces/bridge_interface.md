# BRIDGE interface

## URL

```
frinx-openconfig-interfaces:interfaces/interface={{bridge_ifc_name}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/interfaces/src/main/yang)

```javascript
{
    "frinx-openconfig-interfaces:interface": [
        {
            "name": "{{bridge_ifc_name}}",
            "config": {
                "type": "iana-if-type:bridge",
                "enabled": {{bridge_enabled}},
                "frinx-cisco-if-extension:vrf-forwarding": "{{vrf_forwarding}}",
                "frinx-cisco-if-extension:snmp-trap-link-status": {{snmp_trap_link_status}},
                "name": "{{bridge_ifc_name}}"
            },
            "subinterfaces": {
                "subinterface": [
                    {
                        "index": 0,
                        "frinx-openconfig-if-ip:ipv4": {
                            "addresses": {
                                "address": [
                                    {
                                        "ip": "{{vlan_ip}}",
                                        "config": {
                                            "prefix-length": {{vlan_prefix_length}},
                                            "ip": "{{vlan_ip}}"
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

### IOS 12

#### CLI

<pre>
interface BDI{{bridge_ifc_id}}
 shutdown | no shutdown
 vrf forwarding {{vrf_forwarding}}
 ip address {{bridge_ip}}/{{bridge_prefix_length}}
 snmp trap link-status | no snmp trap link-status
</pre>

{{bridge_ifc_id}} is parsed from {{bridge_ifc_name}}  
example {{bridge_ifc_name}} is BDI10 -&gt; {{bridge_ifc_id}} is 10  

*no shutdown* is a conversion of {{vlan_enabled}} set *true*  
*shutdown* is a conversion of {{vlan_enabled}} set *false* 
*no snmp trap link-status* is a conversion of {{snmp_trap_link_status}} set *false*  
*snmp trap link-status* is a conversion of {{snmp_trap_link_status}} set *true*   

##### Unit

Link to github : [ios-unit](https://github.com/FRINXio/cli-units/tree/master/ios/interface)
