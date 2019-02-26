# Link Aggregation Group (bundle) interface

## URL

```
frinx-openconfig-interfaces:interfaces/interface/{{lag_intf_name}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/interfaces/src/main/yang)

```javascript
{
    "interface": [
        {
            "name": "{{lag_intf_name}}",
            "config": {
                "type": "iana-if-type:ieee8023adLag",
                "enabled": {{lag_enabled}},
                "mtu": {{lag_mtu}},
                "description": "{{lag_description}}",
                "name": "{{lag_intf_name}}"
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
                        },
                        "frinx-openconfig-if-ip:ipv6": {
                            "addresses": {
                                "address": [
                                    {
                                        "ip": "{{lag_ip6}}",
                                        "config": {
                                            "ip": "{{lag_ip6}}",
                                            "prefix-length": "{{lag_prefix6_length}}"
                                        }
                                    }
                                ]
                            }
                        },
                        "router-advertisement": {
                            "suppress": true
                        }
                    },
                    {
                        "index": {{sub_interface_index}},
                        "config": {
                            "index": {{sub_interface_index}},
                            "enabled": {{lag_sub_enabled}}
                        },
                        "vlan": {
                            "config": {
                                "vlan-id": {{vlan_id}}
                            }
                        },
                        "frinx-cisco-if-extension:statistics": {
                            "config": {
                                "load-interval": {{lag_sub_load_interval}}
                            }
                        },
                        "frinx-cisco-if-extension:hold-time": {
                            "config": {
                                "up": {{lag_sub_hold_time_up}}
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
                    "frinx-juniper-if-aggregate-extension:link-speed": {{lag_link_speed}},
                    "frinx-if-aggregate-extension:mac-address": {{aggregate_mac_address}},
                    "frinx-if-aggregate-extension:system-id-mac": {{aggregate_lacp_mac_address}}
                },
                "frinx-bfd:bfd": {
                    "config": {
                        "local-address": "{{lag_bfd_local_address}}",
                        "destination-address": "{{lag_bfd_destination_address}}",
                        "multiplier": {{lag_bfd_multiplier}},
                        "min-interval": {{lag_bfd_min_interval}}
                    }
                },
                "frinx-openconfig-vlan:switched-vlan" : {
                    "config" : {
                        "interface-mode": "TRUNK",
                        "trunk-vlans": [
                             {{tagged_vlan_intf_id}}
                         ],
                         "native-vlan": {{untagged_vlan_intf_id}}
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
interface Bundle-Ether{{lag_intf_id}} 
 description {{lag_description}} 
 mtu {{lag_mtu}}
 ipv4 address {{lag_ip}} {{lag_prefix_length}}
 ipv6 address {{lag_ip6}} {{lag_prefix6_length}}
 ipv6 nd suppress-ra
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

{{lag_intf_id}} is parsed from {{lag_intf_name}}  
example {{lag_intf_name}} is Bundle-Ether100 -&gt; {{lag_intf_id}} is 100  

*no shutdown* is a conversion of {{lag_enabled}} set *true*  
*shutdown* is a conversion of {{lag_enabled}} set *false*  
*no dampening* is a conversion of {{lag_damp_enabled}} set *false*  
*nd suppress-ra* is a conversion of "suppress": true

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/interface)

### Cisco IOS XR 6.6.1

#### CLI

<pre>
interface Bundle-Ether{{lag_intf_id}} 
 description {{lag_description}} 
 mtu {{lag_mtu}}
 dampening {{lag_damp_half_life}} {{lag_damp_reuse}} {{lag_damp_suppress}} {{lag_damp_max-supress}} | no dampening
 load-interval {{lag_load_interval}}
 mac-address {{lag_mac_address}}
 lacp system mac {{lag_lacp_mac_address}}
 shutdown | no shutdown
</pre>
<pre>
interface Bundle-Ether{{lag_intf_id}}.{{sub_interface_index}}
 load-interval {{lag_sub_load_interval}}
 carrier-delay up {{lag_sub_hold_time_up}}
</pre>

{{lag_intf_id}} is parsed from {{lag_intf_name}}  
example {{lag_intf_name}} is Bundle-Ether100 -&gt; {{lag_intf_id}} is 100  
{{lag_mac_address}} is parsed from {{aggregate_mac_address}}  
example {{aggregate_mac_address}} is aa:bb:cc:dd:ee:ff -&gt; aabb.ccdd.eeff  
{{lag_lacp_mac_address}} is parsed from {{aggregate_lacp_mac_address}}  
example {{aggregate_lacp_mac_address}} is aa:bb:cc:dd:ee:ff -&gt; aabb.ccdd.eeff  
*no shutdown* is a conversion of {{lag_enabled}} set *true*  
*shutdown* is a conversion of {{lag_enabled}} set *false*  
*no dampening* is a conversion of {{lag_damp_enabled}} set *false*  
##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/unitopo-units/tree/master/xr/xr-7-interface-unit)

### Junos 17.3R1.10

#### CLI

<pre>
set interfaces ae{{lag_intf_id}} description {{lag_description}}
set interfaces ae{{lag_intf_id}} mtu {{lag_mtu}}
set interfaces ae{{lag_intf_id}} unit 0 family inet address {{lag_ip}}/{{lag_prefix_length}}
set interfaces ae{{lag_intf_id}} aggregated-ether-options minimum-links {{lag_min_links}}
set interfaces ae{{lag_intf_id}} aggregated-ether-options bfd-liveness-detection neighbor {{lag_bfd_destination_address}}
set interfaces ae{{lag_intf_id}} aggregated-ether-options bfd-liveness-detection local-address {{lag_bfd_local_address}}
set interfaces ae{{lag_intf_id}} aggregated-ether-options bfd-liveness-detection minimum-interval {{lag_bfd_min_interval}}
set interfaces ae{{lag_intf_id}} aggregated-ether-options bfd-liveness-detection multiplier {{lag_bfd_multiplier}}
set interfaces ae{{lag_intf_id}} aggregated-ether-options link-speed {{lag_link_speed}}
delete interface ae{{lag_intf_id}} disable | set interface ae{{lag_intf_id}} disable
</pre>

{{lag_intf_id}} is parsed from {{lag_intf_name}}  
example {{lag_intf_name}} is ae100 -&gt; {{lag_intf_id}} is 100  

*delete interface ae{{lag_intf_id}} disable* is a conversion of {{lag_enabled}} set *true*  
*set interface ae{{lag_intf_id}} disable* is conversion of {{lag_enabled}} set *false*  

**Device does not support damping on LAG interface.**

##### Unit

NOT IMPLEMENTED

Link to github : [junos-unit](https://github.com/FRINXio/unitopo-units/tree/master/junos/junos-17/junos-17-interface-unit)

### Junos 18.2R2

#### CLI

<pre>
set interfaces ae{{lag_intf_id}} unit {{sub_interface_index}} description {{lag_description}}
set interfaces ae{{lag_intf_id}} unit {{sub_interface_index}} vlan-id {{vlan_id}}
set interfaces ae{{lag_intf_id}} unit {{sub_interface_index}} vlan-tags inner 0x8100:{{inner_vlan_tag}}
set interfaces ae{{lag_intf_id}} unit {{sub_interface_index}} vlan-tags outer 0x8100:{{outer_vlan_tag}}
delete interface ae{{lag_intf_id}} disable | set interface ae{{lag_intf_id}} disable
delete interface ae{{lag_intf_id}} unit {{sub_interface_index}} disable | set interface ae{{lag_intf_id}} unit {{sub_interface_index}} disable
</pre> 

{{lag_intf_id}} is parsed from {{lag_intf_name}}  
example {{lag_intf_name}} is ae100 -&gt; {{lag_intf_id}} is 100  

*inner_vlan_tag* , *outer_vlan_tag* is a conversion of {{vlan_id}} set {{outer_vlan_tag}}.{{inner_vlan_tag}}  
*delete interface ae{{lag_intf_id}} disable* is a conversion of {{lag_enabled}} set *true*  
*set interface ae{{lag_intf_id}} disable* is conversion of {{lag_enabled}} set *false*  
*delete interface ae{{lag_intf_id}} unit {{sub_interface_index}} disable* is a conversion of {{lag_sub_enabled}} set *true*  
*set interface ae{{lag_intf_id}} unit {{sub_interface_index}} disable* is conversion of {{lag_sub_enabled}} set *false*  

Link to github : [junos-unit](https://github.com/FRINXio/unitopo-units/tree/master/junos/junos-18/junos-18-interface-unit)

### Dasan NOS SFU.RR.5.6p5

#### CLI

<pre>
bridge
 lacp aggregator {{lag_intf_id}}
 vlan add br{{tagged_vlan_intf_id}} t/{{lag_intf_id}} tagged
 vlan add br{{untagged_vlan_intf_id}} t/{{lag_intf_id}} untagged
</pre>

{{lag_intf_id}} is parsed from {{lag_intf_name}}  
example {{lag_intf_name}} is Bundle-Ether100 -&gt; {{lag_intf_id}} is 100 and prefix is Bundle-Ether  
Dasan supports two kinds of prefixes (Prefix is settled by lag type)  
* If the prefix of {{lag_intf_name}} is 'Trunk', lag type is port trunking
* If the prefix of {{lag_intf_name}} is 'Bundle-Ether', lag type is lacp

*vlan add br{{tagged_vlan_intf_id}} t/{{lag_intf_id}} tagged* is only supported by port trunking
*vlan add br{{untagged_vlan_intf_id}} t/{{lag_intf_id}} untagged* is only supported by port trunking