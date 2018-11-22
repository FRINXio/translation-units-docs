# Ethernet interface

## URL

```
frinx-openconfig-interfaces:interfaces/interface/{{eth_intf_id}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/interfaces/src/main/yang)

```javascript
{
    "interface": [
        {
            "name": "{{eth_intf_id}}",
            "config": {
                "type": "iana-if-type:ethernetCsmacd",
                "name": "{{eth_intf_id}}",
                "mtu": {{eth_mtu}},
                "description": "{{eth_description}}",
                "enabled": {{eth_enabled}},
                "tpid": "{{eth_tpid}}"
            },
            "hold-time": {
                "config": {
                    "up": {{eth_hold_time_up}},
                    "down": {{eth_hold_time_down}}
                }
            },
            "subinterfaces": {
                "subinterface": [
                    {
                        "index": 0,
                        "config": {
                            "index": 0,
                            "description": "{{subif_description}}"
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
                                        "ip": "{{eth_ip}}",
                                        "config": {
                                            "ip": "{{eth_ip}}",
                                            "prefix-length": {{eth_prefix}}
                                        }
                                    }
                                ]
                            }
                        },
                        "frinx-openconfig-if-ip:ipv6": {
                            "addresses": {
                                "address": [
                                    {
                                        "ip": "{{eth_ip}}",
                                        "config": {
                                            "ip": "{{eth_ip6}}",
                                            "prefix-length": {{eth_prefix6}}
                                        }
                                    }
                                ]
                            },
                            "router-advertisement": {
                                "config": {
                                    "suppress": "{{ip6_nd_suppress_ra}}"
                                }
                            }
                        }
                    },
                    {
                        "index": {{sub_interface_index}},
                        "config": {
                            "index": {{sub_interface_index}},
                            "description": "{{subif_description}}"
                        },
                        "frinx-openconfig-if-ip:ipv4": {
                            "addresses": {
                                "address": [
                                    {
                                        "ip": "{{eth_ip}}",
                                        "config": {
                                            "ip": "{{eth_ip}}",
                                            "prefix-length": {{eth_prefix}}
                                        }
                                    }
                                ]
                            },
                            "vrrp": {
                                "vrrp-group": [
                                    "virtual-router-id": "{{eth_ipv4_virtual_id}}",
                                    "config": {
                                        "virtual-router-id": "{{eth_ipv4_virtual_id}}",
                                        "virtual-address": "{{eth_ipv4_virtual_address}}"
                                    }
                                ]
                            }
                        }
                    }
                ]
            },
            "frinx-damping:damping": {
                "config": {
                    "enabled": {{eth_damping_enabled}},
                    "half-life": {{eth_half-time}},
                    "reuse": {{eth_reuse}},
                    "suppress": {{eth_suppress}},
                    "max-suppress": {{eth_max-suppress}}
                }
            },
            "frinx-openconfig-if-ethernet:ethernet": {
                "config": {
                    "frinx-openconfig-if-aggregate:aggregate-id": "Bundle-Ether{{eth_lag_intf_id}}",
                    "frinx-lacp-lag-member:lacp-mode": "{{lacp_mode}}",
                    "frinx-lacp-lag-member:interval": "{{lacp_interval}}",
                    "frinx-if-aggregate-extension:admin-key": {{admin-key}}
                },
                "frinx-openconfig-vlan:switched-vlan" : {
                    "config" : {
                        "interface-mode": "{{vlan_mode}}",
                        "trunk-vlans": [
                             {{vlan_intf_id}}
                         ],
                         "access-vlan": {{vlan_intf_id}}
                    }
                }
            },
            "frinx-cisco-if-extension:statistics": {
                "config": {
                    "load-interval": {{eth_load_interval}}
                }
            }
        }
    ]
}
```

## OS Configuration Commands

### Cisco IOS Classic (15.2(4)S5) / XE (15.3(3)S2)

<pre>
interface {{eth_intf_id}}
 description {{eth_description}}
 mtu {{eth_mtu}}
 ip address {{eth_ip}} &lt;subnet&gt;
 shutdown | no shutdown
</pre>

&lt;subnet&gt; is a conversion of {{eth_prefix}}  
*no shutdown* is a conversion of {{eth_enabled}} set *true*  
*shutdown* is a conversion of {{eth_enabled}} set *false*  

##### Unit

Link to github : [ios-unit](https://github.com/FRINXio/cli-units/tree/master/ios/interface)

### Cisco IOS XR 5.3.4

#### CLI

<pre>
interface {{eth_intf_id}}
 description {{eth_description}}
 mtu {{eth_mtu}}
 ipv4 address {{eth_ip}} {{eth_prefix}}
 ipv6 address {{eth_ip6}} {{eth_prefix6}}
 ipv6 nd suppress-ra
 dampening {{eth_half-life}} {{reuse}} {{suppress}} {{max-suppress}} | no dampening
 carrier-delay up {{eth_hold_time_up}} down {{eth_hold_time_down}} 
 load-interval {{eth_load-interval}}
 bundle id {{eth_lag_intf_id}} mode {{lacp_mode}}
 lacp period short | no lacp period short
 shutdown | no shutdown
</pre>

*no shutdown* is a conversion of {{eth_enabled}} set *true*  
*shutdown* is a conversion of {{eth_enabled}} set *false*  
*no dampening* is a conversion of {{eth_damping_enabled}} set *false*  
*lacp period short* is a conversion of {{lacp_interval}} set to *frinx-openconfig-lacp:FAST*  
*no lacp period short* is a conversion of {{lacp_interval}} set to *frinx-openconfig-lacp:SLOW*  
if {{lacp_mode}} is not specified then command *bundle id {{eth_lag_intf_id}} mode on* is used  
*mode active* is a conversion of {{lacp_mode}} set to *frinx-openconfig-lacp:ACTIVE*  
*mode passive* is a conversion of {{lacp_interval}} set to *frinx-openconfig-lacp:PASSIVE*  
*ipv6 nd suppress-ra* is a conversion of {{ip6_nd_suppress_ra}} set *true*

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/interface)

### Cisco IOS XR 7.0.1

#### CLI

<pre>
interface {{eth_intf_id}}
 description {{eth_description}}
 ipv4 address {{eth_ip}} {{eth_prefix}}
 dampening {{eth_half-life}} {{reuse}} {{suppress}} {{max-suppress}} | no dampening
 load-interval {{eth_load-interval}}
 bundle id {{eth_lag_intf_id}} mode {{lacp_mode}}
 lacp period short | no lacp period short
 shutdown | no shutdown
</pre>

*no shutdown* is a conversion of {{eth_enabled}} set *true*  
*shutdown* is a conversion of {{eth_enabled}} set *false*  
*no dampening* is a conversion of {{eth_damping_enabled}} set *false*  
*lacp period short* is a conversion of {{lacp_interval}} set to *frinx-openconfig-lacp:FAST*  
*no lacp period short* is a conversion of {{lacp_interval}} set to *frinx-openconfig-lacp:SLOW*  
if {{lacp_mode}} is not specified then command *bundle id {{eth_lag_intf_id}} mode on* is used  
*mode active* is a conversion of {{lacp_mode}} set to *frinx-openconfig-lacp:ACTIVE*  
*mode passive* is a conversion of {{lacp_interval}} set to *frinx-openconfig-lacp:PASSIVE*  

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/unitopo-units/tree/master/xr/xr-7-interface-unit)

### Junos 14.1X53-D40.8

#### CLI

<pre>
set interfaces {{eth_intf_id}} vlan-tagging
set interfaces {{eth_intf_id}} unit 0 description {{subif_description}}
set interfaces {{eth_intf_id}} unit 0 vlan-id {{vlan_id}}
set interfaces {{eth_intf_id}} unit 0 family inet address {{eth_ip}}/{{eth_prefix}}
</pre>

*vlan-tagging* is a conversion of {{eth_tpid}} set *TPID_0X8100*

### Junos 17.3R1.10

#### CLI

<pre>
set interfaces {{eth_intf_id}} description {{eth_description}}
set interfaces {{eth_intf_id}} mtu {{eth_mtu}}
set interfaces {{eth_intf_id}} unit 0 family inet address {{eth_ip}}/{{eth_prefix}}
set interfaces {{eth_intf_id}} damping enable
set interfaces {{eth_intf_id}} damping half-life {{eth_half-life}}
set interfaces {{eth_intf_id}} damping max-suppress {{eth_max-supress}}
set interfaces {{eth_intf_id}} damping reuse {{eth_reuse}}
set interfaces {{eth_intf_id}} damping suppress {{eth_supress}}
set interfaces {{eth_intf_id}} hold-time up {{eth_hold_time_up}} down {{eth_hold_time_down}}
set interfaces {{eth_intf_id}} gigether-options 802.3ad {{eth_lag_intf_id}}
set interfaces ae{{eth_lag_intf_id}} aggregated-ether-options lacp {{lacp_mode}}
set interfaces ae{{eth_lag_intf_id}} aggregated-ether-options lacp periodic {{lacp_interval}}
delete interface {{eth_intf_id}} disable | set interface {{eth_intf_id}} disable
</pre>

*delete interface {{lag_intf_id}} disable* is a conversion of {{lag_enabled}} set *true*  
*set interface {{lag_intf_id}} disable* is conversion of {{lag_enabled}} set *false* 

##### Unit

Link to github : [junos-unit](https://github.com/FRINXio/unitopo-units/tree/master/junos/junos-17/junos-17-interface-unit)

### Junos 18.2R2

#### CLI

<pre>
set interfaces {{eth_intf_id}} unit {{sub_interface_index}} description {{subif_description}}
set interfaces {{eth_intf_id}} unit {{sub_interface_index}} family inet address {{eth_ip}}/{{eth_prefix}}
set interfaces {{eth_intf_id}} unit {{sub_interface_index}} family inet address {{eth_ip}}/{{eth_prefix}} vrrp-group {{eth_ipv4_virtual_id}} virtual-address {{eth_ipv4_virtual_address}}
</pre>

##### Unit

Link to github : [junos-unit](https://github.com/FRINXio/unitopo-units/tree/master/junos/junos-18/junos-18-interface-unit)


### Brocade (V5.6.0fT163)

#### CLI

<pre>
tag-type {{eth_tpid}} {{eth_intf_id}}

interface {{eth_intf_id}}
  port-name {{eth_description}}
  enable | disable
</pre>

*enable* is a conversion of {{eth_enabled}} set *true*  
*disable* is a conversion of {{eth_enabled}} set *false*  

##### Unit

Link to github : [brocade-unit](https://github.com/FRINXio/cli-units/tree/master/brocade/interface)

### Huawei NE5000E (V800R009C10SPC310)

#### CLI

<pre>
interface {{eth_intf_id}}
 ipv4 address {{eth_ip}} {{subnet}}
</pre>

{{subnet}} is conversion of {{eth_prefix}}


### Dasan NOS SFU.RR.5.6p5

#### CLI

<pre>
bridge
 vlan add br{{vlan_intf_id}} {{phy_port_id}} [un]tagged
 lacp port {{phy_port_id}} aggregator {{eth_lag_intf_id}}
 lacp port admin-key {{phy_port_id}} {{admin-key}}
 jumbo-frame {{phy_port_id}} {{eth_mtu}}
 port enable {{phy_port_id}} | port disable {{phy_port_id}}
</pre>

{{phy_port_id}} is parsed from {{eth_intf_id}}  
example {{eth_intf_id}} is Ethernet1/1 -&gt; {{phy_port_id}} is 1/1  

*tagged* is a conversion of {{vlan_mode}} set *TRUNK*  
*untagged* is a conversion of {{vlan_mode}} set *ACCESS*  
*port enable {{phy_port_id}}* is a conversion of {{eth_enabled}} set *true*  
*port disable {{phy_port_id}}* is a conversion of {{eth_enabled}} set *false*  
