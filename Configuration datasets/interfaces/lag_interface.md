# Link Aggregation Group (bundle) interface

## URL

```
frinx-openconfig-interfaces:interfaces/interface/{{lag_intf_id}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/interfaces/src/main/yang)

```javascript
{
    "interface": [
        {
            "name": "{{lag_intf_id}}",
            "config": {
                "type": "iana-if-type:ieee8023adLag",
                "enabled": {{lag_enabled}},
                "mtu": {{lag_mtu}},
                "description": "{{lag_description}}",
                "name": "Bundle-Ether{{lag_intf_id}}"
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
                                        "ip": "{{lag_ip}}",
                                        "config": {
                                            "ip": "{{lag_ip}}",
                                            "prefix-length": "{{lag_prefix_length}}"
                                        }
                                    }
                                ]
                            }
                        }
                    }
                ]
            },
            "frinx-damping:damping": {
                "config": {
                    "enabled": {{lag_damp_enabled}},
                    "half-life": {{lag_damp_half_life}},
                    "reuse": {{lag_damp_reuse}},
                    "suppress": {{lag_damp_suppress}},
                    "max-suppress": {{lag_damp_max-supress}}
                }
            },
            "frinx-cisco-if-extension:statistics": {
                "config": {
                    "load-interval": {{lag_load_interval}}
                }
            },
            "frinx-openconfig-if-aggregate:aggregation": {
                "config": {
                    "min-links": {{lag_min_links}},
                    "frinx-juniper-if-aggregate-extension:link-speed": {{lag_link_speed}}
                },
                "frinx-bfd:bfd": {
                    "config": {
			"local-address": "{{lag_bfd_local_address}}"
                        "destination-address": "{{lag_bfd_destination_address}}",
                        "multiplier": {{lag_bfd_multiplier}},
                        "min-interval": {{lag_bfd_min_interval}}
                    }
                }
            }
        }
    ]
}
```

## OS Configuration Commands

### Cisco IOS XR 5.3.4

#### CLI

<pre>
interface {{lag_intf_id}} 
 description {{lag_description}} 
 mtu {{lag_mtu}}
 ipv4 address {{lag_ip}} {{lag_prefix_length}}
 dampening {{lag_damp_half_life}}  {{lag_damp_reuse}} {{lag_damp_suppress}} {{lag_damp_max-supress}} | no dampening
 load-interval {{lag_load_interval}}
 bundle minimum-active links {{lag_min-links}}
 bfd mode ietf
 bfd address-family ipv4 fast-detect
 bfd address-family ipv4 destination {{lag_bfd_destination_address}}
 bfd address-family ipv4 minimum-interval {{lag_bfd_min_interval}}
 bfd address-family ipv4 multiplier {{lag_bfg_multiplier}}
 shutdown | no shutdown
</pre>

*no shutdown* is a conversion of {{eth_enabled}} set *true*  
*shutdown* is a conversion of {{eth_enabled}} set *false*  
*no dampening* is a conversion of {{eth_damping_enabled}} set *false*  

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/interface)

### Junos 15.1F-6.9

#### CLI

<pre>
set interfaces {{lag_intf_id}} description {{lag_description}}
set interfaces {{lag_intf_id}} mtu {{lag_mtu}}
set interfaces {{lag_intf_id}} unit 0 family inet address {{lag_ip}}/{{lag_prefix_length}}
set interfaces {{lag_intf_id}} aggregated-ether-options minimum-links {{lag_min_links}}
set interfaces {{lag_intf_id}} aggregated-ether-options bfd-liveness-detection neighbor {{lag_bfd_destination_address}}
set interfaces {{lag_intf_id}} aggregated-ether-options bfd-liveness-detection local-address {{lag_bfd_local_address}}
set interfaces {{lag_intf_id}} aggregated-ether-options bfd-liveness-detection minimum-interval {{lag_bfd_min_interval}}
set interfaces {{lag_intf_id}} aggregated-ether-options bfd-liveness-detection multiplier {{lag_bfd_multiplier}}
set interfaces {{lag_intf_id}} aggregated-ether-options link-speed {{lag_link_speed}}
delete interface {{lag_intf_id}} disable | set interface {{lag_intf_id}} disable
</pre>

*delete interface {{lag_intf_id}} disable* is a conversion of {{lag_enabled}} set *true*  
*set interface {{lag_intf_id}} disable* is conversion of {{lag_enabled}} set *false*  

**Device does not support damping on LAG interface.**

##### Unit

NOT IMPLEMENTED

Link to github : [junos-unit]()
