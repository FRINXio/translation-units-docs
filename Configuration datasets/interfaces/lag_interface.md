# Link Aggregation Group (bundle) interface

## URL

```
frinx-openconfig-interfaces:interfaces/interface/{{lag_ifc_name}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/interfaces/src/main/yang)

```javascript
{
    "interface": [
        {
            "name": "{{lag_ifc_name}}",
            "config": {
                "type": "iana-if-type:ieee8023adLag",
                "enabled": {{lag_enabled}},
                "mtu": {{lag_mtu}},
                "description": "{{lag_description}}",
                "name": "{{lag_ifc_name}}"
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
                                        },
                                        "vrrp": {
                                            "vrrp-group": [
                                                "virtual-router-id": "{{lag_ip_virtual_id}}",
                                                "config": {
                                                    "virtual-router-id": "{{lag_ip_virtual_id}}",
                                                    "virtual-address": "{{lag_ip_virtual_address}}"
                                                }
                                            ]
                                        }
                                    }
                                ]
                            }
                        },
                        "frinx-openconfig-if-ip:ipv6": {
                            "config": {
                                "enabled": {{lag_ip6_enabled}}
                            },
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
                            },
                            "router-advertisement": {
                                "suppress": {{ip6_nd_suppress_ra}}
                            }
                        }
                    },
                    {
                        "index": {{sub_ifc_index}},
                        "config": {
                            "index": {{sub_ifc_index}},
                            "description": "{{lag_sub_description}}",
                            "frinx-juniper-if-extension:rpm-type": "{{rpm_type}}"
                            "enabled": {{lag_sub_enabled}}
                        },
                        "frinx-openconfig-if-ip:ipv4": {
                            "addresses": {
                                "address": [
                                    {
                                        "ip": "{{lag_sub_ip}}",
                                        "config": {
                                            "ip": "{{lag_sub_ip}}",
                                            "prefix-length": "{{lag_sub_prefix_length}}"
                                        },
                                        "vrrp": {
                                            "vrrp-group": [
                                                "virtual-router-id": "{{lag_sub_ip_virtual_id}}",
                                                "config": {
                                                    "virtual-router-id": "{{lag_sub_ip_virtual_id}}",
                                                    "virtual-address": "{{lag_sub_ip_virtual_address}}"
                                                }
                                            ]
                                        }
                                    }
                                ]
                            }
                        },
                        "frinx-openconfig-vlan:vlan": {
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
                        },
                        "frinx-oam:cfm": {
                            "config": {
                                "enabled": {{lag_sub_cfm_enabled}}
                            },
                            "domains": {
                                "domain": [
                                    {
                                        "domain-name": "{{lag_sub_cfm_domain_name}}",
                                        "config": {
                                            "domain-name": "{{lag_sub_cfm_domain_name}}"
                                        },
                                        "mep": {
                                            "config": {
                                                "ma-name": "{{lag_sub_cfm_ma_name}}",
                                                "mep-id": {{lag_sub_cfm_mep_id}}
                                            }
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
                    "max-suppress": {{lag_damp_max_supress}}
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
                "frinx-bfd:bfd-ipv6": {
                    "config": {
                        "destination-address": "{{lag_bfd_destination_address_ipv6}}",
                        "multiplier": {{lag_bfd_multiplier_ipv6}},
                        "min-interval": {{lag_bfd_min_interval_ipv6}}
                    }
                },
                "frinx-openconfig-vlan:switched-vlan" : {
                    "config" : {
                        "interface-mode": "TRUNK",
                        "trunk-vlans": [
                             {{tagged_vlan_ifc_id}}
                         ],
                         "native-vlan": {{untagged_vlan_ifc_id}}
                    }
                }
            }
        }
    ]
}
```

## OS Configuration Commands

### Cisco IOS Classic (15.2(4)S5) / XE (15.3(3)S2)

<pre>
interface {{lag_ifc_name}}
 ip address {{lag_ip}} {{lag_subnet}}
</pre>

{{lag_sub_subnet}} is conversion of {{lag_sub_prefix_length}}  

##### Unit

Link to github : [ios-unit](https://github.com/FRINXio/cli-units/tree/master/ios/interface)

### Cisco IOS XR 5.3.4

#### CLI

<pre>
interface Bundle-Ether{{lag_ifc_id}} 
 description {{lag_description}} 
 mtu {{lag_mtu}}
 ipv4 address {{lag_ip}} {{lag_prefix_length}}
 ipv6 address {{lag_ip6}} {{lag_prefix6_length}}
 ipv6 nd suppress-ra
 dampening {{lag_damp_half_life}}  {{lag_damp_reuse}} {{lag_damp_suppress}} {{lag_damp_max_supress}} | no dampening
 load-interval {{lag_load_interval}}
 bundle minimum-active links {{lag_min_links}}
 bfd mode ietf
 bfd address-family ipv4 fast-detect
 bfd address-family ipv4 destination {{lag_bfd_destination_address}}
 bfd address-family ipv4 minimum-interval {{lag_bfd_min_interval}}
 bfd address-family ipv4 multiplier {{lag_bfd_multiplier}}
 shutdown | no shutdown
</pre>

{{lag_ifc_id}} is parsed from {{lag_ifc_name}}  
example {{lag_ifc_name}} is Bundle-Ether100 -&gt; {{lag_ifc_id}} is 100  

*no shutdown* is a conversion of {{lag_enabled}} set *true*  
*shutdown* is a conversion of {{lag_enabled}} set *false*  
*no dampening* is a conversion of {{lag_damp_enabled}} set *false*  
*ipv6 nd suppress-ra* is a conversion of {{ip6_nd_suppress_ra}} set *true*  

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/interface)

### Cisco IOS XR 6.2.3

#### CLI

<pre>
interface Bundle-Ether{{lag_ifc_id}} 
 description {{lag_description}} 
 mtu {{lag_mtu}}
 ipv4 address {{lag_ip}} {{lag_prefix_length}}
 ipv6 address {{lag_ip6}} {{lag_prefix6_length}}
 ipv6 enable | no ipv6 enable
 dampening {{lag_damp_half_life}}  {{lag_damp_reuse}} {{lag_damp_suppress}} {{lag_damp_max_supress}} | no dampening
 load-interval {{lag_load_interval}}
 bundle minimum-active links {{lag_min_links}}
 bfd mode ietf
 bfd address-family ipv4 fast-detect
 bfd address-family ipv4 destination {{lag_bfd_destination_address}}
 bfd address-family ipv4 minimum-interval {{lag_bfd_min_interval}}
 bfd address-family ipv4 multiplier {{lag_bfd_multiplier}}
 bfd address-family ipv6 fast-detect
 bfd address-family ipv6 destination {{lag_bfd_destination_address_ipv6}}
 bfd address-family ipv6 minimum-interval {{lag_bfd_min_interval_ipv6}}
 bfd address-family ipv6 multiplier {{lag_bfd_multiplier_ipv6}}
 shutdown | no shutdown
</pre>

{{lag_ifc_id}} is parsed from {{lag_ifc_name}}  
example {{lag_ifc_name}} is Bundle-Ether100 -&gt; {{lag_ifc_id}} is 100  

*no shutdown* is a conversion of {{lag_enabled}} set *true*  
*shutdown* is a conversion of {{lag_enabled}} set *false*  
*no dampening* is a conversion of {{lag_damp_enabled}} set *false*  
*ipv6 enable* is a conversion of {{lag_ip6_enabled}} set *true*  
*no ipv6 enable* is a conversion of {{lag_ip6_enabled}} set *false*  

<pre>
interface Bundle-Ether{{lag_ifc_id}}.{{sub_ifc_index}}
 description {{lag_sub_description}}
 ipv4 address {{lag_sub_ip}} {{lag_sub_subnet}}
 encapsulation dot1q {{vlan_id}}
</pre>

{{lag_sub_subnet}} is conversion of {{lag_sub_prefix_length}}  

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/interface)

### Cisco IOS XR 6.6.1

#### CLI

<pre>
interface Bundle-Ether{{lag_ifc_id}} 
 description {{lag_description}} 
 ipv4 address {{lag_sub_ip}} {{lag_sub_subnet}}
 mtu {{lag_mtu}}
 dampening {{lag_damp_half_life}} {{lag_damp_reuse}} {{lag_damp_suppress}} {{lag_damp_max_supress}} | no dampening
 load-interval {{lag_load_interval}}
 mac-address {{lag_mac_address}}
 lacp system mac {{lag_lacp_mac_address}}
 shutdown | no shutdown
</pre>

{{lag_ifc_id}} is parsed from {{lag_ifc_name}}  
example {{lag_ifc_name}} is Bundle-Ether100 -&gt; {{lag_ifc_id}} is 100  
{{lag_mac_address}} is parsed from {{aggregate_mac_address}}  
example {{aggregate_mac_address}} is aa:bb:cc:dd:ee:ff -&gt; aabb.ccdd.eeff  
{{lag_lacp_mac_address}} is parsed from {{aggregate_lacp_mac_address}}  
example {{aggregate_lacp_mac_address}} is aa:bb:cc:dd:ee:ff -&gt; aabb.ccdd.eeff  

{{lag_subnet}} is conversion of {{lag_prefix_length}}  
*no shutdown* is a conversion of {{lag_enabled}} set *true*  
*shutdown* is a conversion of {{lag_enabled}} set *false*  
*no dampening* is a conversion of {{lag_damp_enabled}} set *false*  

---
<pre>
interface Bundle-Ether{{lag_ifc_id}}.{{sub_ifc_index}}
 description {{lag_sub_description}}
 ipv4 address {{lag_sub_ip}} {{lag_sub_subnet}}
 encapsulation dot1q {{vlan_id}}
 load-interval {{lag_sub_load_interval}}
 carrier-delay up {{lag_sub_hold_time_up}}
</pre>

{{lag_ifc_id}} is parsed from {{lag_ifc_name}}  
example {{lag_ifc_name}} is Bundle-Ether100 -&gt; {{lag_ifc_id}} is 100  

{{lag_sub_subnet}} is conversion of {{lag_sub_prefix_length}}  

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/unitopo-units/tree/master/xr/xr-6.6/xr-6.6-interface-unit)

### Cisco IOS XR 6.6.2

#### CLI

<pre>
interface Bundle-Ether{{lag_ifc_id}}.{{sub_ifc_index}}
 description {{lag_sub_description}}
 ipv4 address {{lag_sub_ip}} {{lag_sub_subnet}}
 ipv6 address {{lag_ip6}} {{lag_prefix6_length}}
 encapsulation dot1q {{vlan_id}}
 ethernet cfm
  mep domain {{lag_sub_cfm_domain_name}} service {{lag_sub_cfm_ma_name}} mep-id {{lag_sub_cfm_mep_id}}
</pre>

{{lag_ifc_id}} is parsed from {{lag_ifc_name}}  
example {{lag_ifc_name}} is Bundle-Ether100 -&gt; {{lag_ifc_id}} is 100  

{{lag_sub_subnet}} is conversion of {{lag_sub_prefix_length}}  
*ethernet cfm* is a conversion of {{lag_sub_cfm_enabled}} set to true  
*no ethernet cfm* is a conversion of {{lag_sub_cfm_enabled}} set to false  

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/interface)

### Junos 17.3R1.10

#### CLI

<pre>
set interfaces ae{{lag_ifc_id}} description {{lag_description}}
set interfaces ae{{lag_ifc_id}} mtu {{lag_mtu}}
set interfaces ae{{lag_ifc_id}} unit 0 family inet address {{lag_ip}}/{{lag_prefix_length}}
set interfaces ae{{lag_ifc_id}} aggregated-ether-options minimum-links {{lag_min_links}}
set interfaces ae{{lag_ifc_id}} aggregated-ether-options bfd-liveness-detection neighbor {{lag_bfd_destination_address}}
set interfaces ae{{lag_ifc_id}} aggregated-ether-options bfd-liveness-detection local-address {{lag_bfd_local_address}}
set interfaces ae{{lag_ifc_id}} aggregated-ether-options bfd-liveness-detection minimum-interval {{lag_bfd_min_interval}}
set interfaces ae{{lag_ifc_id}} aggregated-ether-options bfd-liveness-detection multiplier {{lag_bfd_multiplier}}
set interfaces ae{{lag_ifc_id}} aggregated-ether-options link-speed {{lag_link_speed}}
delete interface ae{{lag_ifc_id}} disable | set interface ae{{lag_ifc_id}} disable
</pre>

{{lag_ifc_id}} is parsed from {{lag_ifc_name}}  
example {{lag_ifc_name}} is ae100 -&gt; {{lag_ifc_id}} is 100  

*delete interface ae{{lag_ifc_id}} disable* is a conversion of {{lag_enabled}} set *true*  
*set interface ae{{lag_ifc_id}} disable* is conversion of {{lag_enabled}} set *false*  

**Device does not support damping on LAG interface.**

##### Unit

Link to github : [junos-unit](https://github.com/FRINXio/unitopo-units/tree/master/junos/junos-17/junos-17-interface-unit)

### Junos 18.2R1-S2.1

#### CLI

<pre>
delete interface ae{{lag_ifc_id}} disable | set interface ae{{lag_ifc_id}} disable
set interfaces ae{{lag_ifc_id}} unit 0 family inet address {{lag_ip}}/{{lag_prefix_length}}
set interfaces ae{{lag_ifc_id}} unit 0 family inet address {{lag_ip}}/{{lag_prefix_length}} vrrp-group {{lag_ip_virtual_id}} virtual-address {{lag_ip_virtual_address}}
</pre> 

{{lag_ifc_id}} is parsed from {{lag_ifc_name}}  
example {{lag_ifc_name}} is ae100 -&gt; {{lag_ifc_id}} is 100  

*delete interface ae{{lag_ifc_id}} disable* is a conversion of {{lag_enabled}} set *true*  
*set interface ae{{lag_ifc_id}} disable* is conversion of {{lag_enabled}} set *false*  

---
<pre>
delete interface ae{{lag_ifc_id}} unit {{sub_ifc_index}} disable | set interface ae{{lag_ifc_id}} unit {{sub_ifc_index}} disable
set interfaces ae{{lag_ifc_id}} unit {{sub_ifc_index}} description {{lag_sub_description}}
set interfaces ae{{lag_ifc_id}} unit {{sub_ifc_index}} vlan-id {{vlan_id}}
set interfaces ae{{lag_ifc_id}} unit {{sub_ifc_index}} vlan-tags inner 0x8100:{{inner_vlan_tag}}
set interfaces ae{{lag_ifc_id}} unit {{sub_ifc_index}} vlan-tags outer 0x8100:{{outer_vlan_tag}}
set interfaces ae{{lag_ifc_id}} unit {{sub_ifc_index}} rpm {{rpm_type}}
set interfaces ae{{lag_ifc_id}} unit {{sub_ifc_index}} family inet address {{lag_sub_ip}}/{{lag_sub_prefix_length}}
set interfaces ae{{lag_ifc_id}} unit {{sub_ifc_index}} family inet address {{lag_sub_ip}}/{{lag_sub_prefix_length}} vrrp-group {{lag_sub_ip_virtual_id}} virtual-address {{lag_sub_ip_virtual_address}}
</pre>


{{lag_ifc_id}} is parsed from {{lag_ifc_name}}  
example {{lag_ifc_name}} is ae100 -&gt; {{lag_ifc_id}} is 100  

*inner_vlan_tag* , *outer_vlan_tag* is a conversion of {{vlan_id}} set {{outer_vlan_tag}}.{{inner_vlan_tag}}  
*delete interface ae{{lag_ifc_id}} unit {{sub_ifc_index}} disable* is a conversion of {{lag_sub_enabled}} set *true*  
*set interface ae{{lag_ifc_id}} unit {{sub_ifc_index}} disable* is conversion of {{lag_sub_enabled}} set *false*  
rpm_ifc_index , rpm_subintf_index is a conversion of {{rpm_ifc_id}} set {{rpm_ifc_index}}.{{rpm_subintf_index}}  

##### Unit

Link to github : [junos-unit](https://github.com/FRINXio/unitopo-units/tree/master/junos/junos-18/junos-18-interface-unit)

### Huawei NE5000E (V800R009C10SPC310)

#### CLI

<pre>
interface {{lag_ifc_name}}
 ipv4 address {{lag_ip}} {{lag_subnet}}
</pre>

{{lag_subnet}} is conversion of {{lag_prefix_length}}  

##### Unit

Link to github : [huawei-unit](https://github.com/FRINXio/cli-units/tree/master/huawei/interface)

### Dasan NOS SFU.RR.5.6p5

#### CLI

<pre>
bridge
 lacp aggregator {{lag_ifc_id}}
 vlan add br{{tagged_vlan_ifc_id}} t/{{lag_ifc_id}} tagged
 vlan add br{{untagged_vlan_ifc_id}} t/{{lag_ifc_id}} untagged
</pre>

{{lag_ifc_id}} is parsed from {{lag_ifc_name}}  
example {{lag_ifc_name}} is Bundle-Ether100 -&gt; {{lag_ifc_id}} is 100 and prefix is Bundle-Ether  
Dasan supports two kinds of prefixes (Prefix is settled by lag type)  
* If the prefix of {{lag_ifc_name}} is 'Trunk', lag type is port trunking
* If the prefix of {{lag_ifc_name}} is 'Bundle-Ether', lag type is lacp

*vlan add br{{tagged_vlan_ifc_id}} t/{{lag_ifc_id}} tagged* is only supported by port trunking  
*vlan add br{{untagged_vlan_ifc_id}} t/{{lag_ifc_id}} untagged* is only supported by port trunking  

##### Unit

Link to github : [dasan-unit](https://github.com/FRINXio/cli-units/tree/master/dasan/interface)
