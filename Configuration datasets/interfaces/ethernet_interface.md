# Ethernet interface

## URL

```
frinx-openconfig-interfaces:interfaces/interface={{eth_ifc_name}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/interfaces/src/main/yang)

```javascript
{
    "interface": [
        {
            "name": "{{eth_ifc_name}}",
            "config": {
                "type": "iana-if-type:ethernetCsmacd/iana-if-type:other",
                "name": "{{eth_ifc_name}}",
                "mtu": {{eth_mtu}},
                "description": "{{eth_description}}",
                "enabled": {{eth_enabled}},
                "tpid": "{{eth_tpid}}",
                "frinx-saos-if-extension:physical-type": "{{eth_phy_type}}",
                "frinx-saos-if-extension:acceptable-frame-type": "{{eth_aft}}",
                "frinx-saos-if-extension:vs-ingress-filter": "{{eth_vif}}",
                "frinx-saos-if-extension:vlan-ethertype-policy": "{{eth_vep}}",
                "frinx-saos-if-extension:ingress-to-egress-qmap": "{{eth_iteq}}",
                "frinx-saos-if-extension:forward-unlearned": "{{fwd_un}}",
                "frinx-saos-if-extension:max-dynamic-macs": "{{max_macs}}"
                "frinx-cisco-if-extension:l2-protocols": [
                    "{{l2-protocols}}"
                ],
                "frinx-cisco-if-extension:lldp-transmit": {{lldp-transmit}},
                "frinx-cisco-if-extension:lldp-receive": {{lldp-receive}},
                "frinx-cisco-if-extension:cdp-enable": {{cdp-enable}},
                "frinx-cisco-if-extension:switchport-port_security-enable": {{port_security-enable}},
                "frinx-cisco-if-extension:switchport-port_security-maximum": {{port_security-maximum}},
                "frinx-cisco-if-extension:switchport-port_security-violation": "{{port_security-violation}}",
                "frinx-cisco-if-extension:switchport-port_security-aging-type": "{{port_security-aging-type}}",
                "frinx-cisco-if-extension:switchport-port_security-aging-time": {{port_security-aging-time}},
                "frinx-cisco-if-extension:switchport-port_security-aging-static": {{port_security-aging-static}}
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
                        },
                        "frinx-openconfig-if-ip:ipv4": {
                            "config": {
                                "mtu": {{eth_ipv4_mtu}}
                            },
                            "addresses": {
                                "address": [
                                    {
                                        "ip": "{{eth_ip}}",
                                        "config": {
                                            "ip": "{{eth_ip}}",
                                            "prefix-length": {{eth_prefix_length}}
                                        }
                                    }
                                ]
                            }
                        },
                        "frinx-openconfig-if-ip:ipv6": {
                            "addresses": {
                                "address": [
                                    {
                                        "ip": "{{eth_ip6}}",
                                        "config": {
                                            "ip": "{{eth_ip6}}",
                                            "prefix-length": {{eth_prefix6_length}}
                                        }
                                    }
                                ]
                            },
                            "router-advertisement": {
                                "config": {
                                    "suppress": {{ip6_nd_suppress_ra}}
                                }
                            }
                        }
                    },
                    {
                        "index": {{sub_ifc_index}},
                        "config": {
                            "index": {{sub_ifc_index}},
                            "description": "{{eth_sub_description}}",
                            "frinx-juniper-if-extension:rpm-type": "{{rpm_type}}",
                            "enabled": {{subif_enabled}}
                        },
                        "frinx-openconfig-vlan:vlan": {
                            "config": {
                                "vlan-id": {{vlan_id}},
                                "name": {{name}}
                            }
                        },
                        "frinx-openconfig-if-ip:ipv4": {
                            "config": {
                                "mtu": {{eth_sub_ipv4_mtu}}
                            },
                            "addresses": {
                                "address": [
                                    {
                                        "ip": "{{eth_sub_ip}}",
                                        "config": {
                                            "ip": "{{eth_sub_ip}}",
                                            "prefix-length": {{eth_sub_prefix_length}}
                                        }
                                    }
                                ]
                            }
                        },
                        "frinx-cisco-if-extension:statistics": {
                            "config": {
                                "load-interval": {{eth_sub_load_interval}}
                            }
                        }
                    }
                ]
            },
            "frinx-damping:damping": {
                "config": {
                    "enabled": {{eth_damping_enabled}},
                    "half-life": {{eth_half_life}},
                    "reuse": {{eth_reuse}},
                    "suppress": {{eth_suppress}},
                    "max-suppress": {{eth_max_suppress}}
                }
            },
            "frinx-openconfig-if-ethernet:ethernet": {
                "config": {
                    "frinx-openconfig-if-aggregate:aggregate-id": "{{lag_ifc_name}}",
                    "frinx-lacp-lag-member:lacp-mode": "{{lacp_mode}}",
                    "frinx-lacp-lag-member:interval": "{{lacp_interval}}",
                    "frinx-if-aggregate-extension:admin-key": {{lacp_admin_key}}
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
            },
            "frinx-oam:cfm": {
                "mip": {
                    "level": [
                        {
                            "level": {{level}},
                            "vlan": [
                                "{{level-vlan}}"
                            ]
                        }
                    ]
                }
            },
            "frinx-cisco-if-extension:statistics": {
                "config": {
                    "load-interval": {{eth_load_interval}}
                }
            },
            "frinx-saos-if-extension:cft-profile": {
                "config": {
                    "name": "{{cft_profile_name}}",
                    "enabled": {{cft_enabled}}
                }
            }
        }
    ]
}
```

## OS Configuration Commands

### Cisco IOS Classic (15.2(4)S5) / XE (15.3(3)S2)

<pre>
interface {{eth_ifc_name}}
 description {{eth_description}}
 mtu {{eth_mtu}}
 ip address {{eth_ip}} {{eth_subnet}}
 channel-group {{lag_ifc_id}} mode {{lacp_mode}}
 media-type {{eth_phy_type}} 
 shutdown | no shutdown
 switchport port-security | no switchport port-security
 switchport port-security maximum {{port_security-maximum}}
 switchport port-security violation {{port_security-violation}}
 switchport port-security aging time {{port_security-aging-time}}
 switchport port-security aging type {{port_security-aging-type}}
 switchport port-security aging static | no switchport port-security aging static
 ethernet cfm mip level {{level}} vlan {{level-vlan}}
 l2protocol-tunnel {{l2-protocols}}
 lldp transmit | no lldp transmit
 lldp receive | no lldp receive
 cdp enable | no cdp enable
</pre>

{{eth_subnet}} is a conversion of {{eth_prefix_length}}  
*no shutdown* is a conversion of {{eth_enabled}} set *true*  
*shutdown* is a conversion of {{eth_enabled}} set *false*
*switchport port-security* is a conversion of {{port_security-enable}} set *true*
*no switchport port-security* is a conversion of {{port_security-enable}} set *false*
{{port_security-violation}} can be "protect", "restrict" or "shutdown"
{{port_security-aging-type}} can be "absolute" or "inactivity"
*switchport port-security aging static* is a conversion of {{port_security-aging-static}} set *true*
*no switchport port-security aging static* is a conversion of {{port_security-aging-static}} set *false*
*lldp transmit* is a conversion of {{lldp-transmit}} set *true*
*no lldp transmit* is a conversion of {{lldp-transmit}} set *false*
*lldp receive* is a conversion of {{lldp-receive}} set *true*
*no lldp receive* is a conversion of {{lldp-receive}} set *false*
*cdp enable* is a conversion of {{cdp-enable}} set *true*
*no cdp enable* is a conversion of {{cdp-enable}} set *false*
{{lag_ifc_id}} is parsed from {{lag_ifc_name}}
example {{lag_ifc_name}} is Port-channel3 -> {{lag_ifc_id}} is 3
mode on is a conversion of {{lacp_mode}} set to frinx-openconfig-lacp:ON
{{eth_phy_type}} can be "default" or "rj45" or "sfp"

---
<pre>
interface {{eth_ifc_name}}.{{sub_ifc_index}}
 ip address {{eth_sub_ip}} {{eth_sub_subnet}}
</pre>

{{eth_sub_subnet}} is conversion of {{eth_sub_prefix_length}}  

##### Unit

Link to github : [ios-unit](https://github.com/FRINXio/cli-units/tree/master/ios/interface)

### Cisco IOS XR 5.3.4

#### CLI

<pre>
interface {{eth_ifc_name}}
 description {{eth_description}}
 mtu {{eth_mtu}}
 ipv4 address {{eth_ip}} {{eth_subnet}}
 ipv6 address {{eth_ip6}}/{{eth_prefix6_length}}
 ipv6 nd suppress-ra
 dampening {{eth_half_life}} {{eth_reuse}} {{eth_supppress}} {{eth_max_suppress}} | no dampening
 carrier-delay up {{eth_hold_time_up}} down {{eth_hold_time_down}} 
 load-interval {{eth_load_interval}}
 bundle id {{lag_ifc_id}} mode {{lacp_mode}}
 lacp period short | no lacp period short
 shutdown | no shutdown
</pre>

{{lag_ifc_id}} is parsed from {{lag_ifc_name}}  
example {{lag_ifc_name}} is Bundle-Ether100 -&gt; {{lag_ifc_id}} is 100  

*no shutdown* is a conversion of {{eth_enabled}} set *true*  
*shutdown* is a conversion of {{eth_enabled}} set *false*  
{{eth_subnet}} is a conversion of {{eth_prefix_length}}  
*no dampening* is a conversion of {{eth_damping_enabled}} set *false*  
*lacp period short* is a conversion of {{lacp_interval}} set to *frinx-openconfig-lacp:FAST*  
*no lacp period short* is a conversion of {{lacp_interval}} set to *frinx-openconfig-lacp:SLOW*  
if {{lacp_mode}} is not specified then command *bundle id {{lag_ifc_id}} mode on* is used  
*mode active* is a conversion of {{lacp_mode}} set to *frinx-openconfig-lacp:ACTIVE*  
*mode passive* is a conversion of {{lacp_mode}} set to *frinx-openconfig-lacp:PASSIVE*  
*ipv6 nd suppress-ra* is a conversion of {{ip6_nd_suppress_ra}} set *true*  

---
<pre>
interface {{eth_ifc_name}}.{{sub_ifc_index}}
 ipv4 address {{eth_sub_ip}} {{eth_sub_subnet}}
</pre>

{{eth_sub_subnet}} is conversion of {{eth_sub_prefix_length}}  

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/interface)

### Cisco IOS XR 6.2.3

#### CLI

<pre>
interface {{eth_ifc_name}}
 description {{eth_description}}
 dampening {{eth_half_life}} {{eth_reuse}} {{eth_suppress}} {{eth_max_suppress}} | no dampening
 load-interval {{eth_load_interval}}
 bundle id {{lag_ifc_id}} mode {{lacp_mode}}
 carrier-delay up {{eth_hold_time_up}} down {{eth_hold_time_down}}
 lacp period short | no lacp period short
 shutdown | no shutdown
</pre>

{{lag_ifc_id}} is parsed from {{lag_ifc_name}}  
example {{lag_ifc_name}} is Bundle-Ether100 -&gt; {{lag_ifc_id}} is 100  

*no shutdown* is a conversion of {{eth_enabled}} set *true*  
*shutdown* is a conversion of {{eth_enabled}} set *false*  
*no dampening* is a conversion of {{eth_damping_enabled}} set *false*  
*lacp period short* is a conversion of {{lacp_interval}} set to *frinx-openconfig-lacp:FAST*  
*no lacp period short* is a conversion of {{lacp_interval}} set to *frinx-openconfig-lacp:SLOW*  
if {{lacp_mode}} is not specified then command *bundle id {{lag_ifc_id}} mode on* is used  
*mode active* is a conversion of {{lacp_mode}} set to *frinx-openconfig-lacp:ACTIVE*  
*mode passive* is a conversion of {{lacp_mode}} set to *frinx-openconfig-lacp:PASSIVE*  

---
<pre>
interface {{eth_ifc_name}}.{{sub_ifc_index}}
 ipv4 mtu {{eth_sub_ipv4_mtu}}
 load-interval {{eth_sub_load_interval}}
</pre>

---
<pre>
interface {{eth_ifc_name}}.{{sub_ifc_index}}
 description {{eth_sub_description}}
 ipv4 address {{eth_sub_ip}} {{eth_sub_subnet}}
 encapsulation dot1q {{vlan_id}}
</pre>

{{eth_sub_subnet}} is conversion of {{eth_sub_prefix_length}}  

### Cisco IOS XR 6.6.1

#### CLI

<pre>
interface {{eth_ifc_name}}
 description {{eth_description}}
 ipv4 address {{eth_ip}} {{eth_subnet}}
 ipv4 mtu {{eth_ipv4_mtu}}
 dampening {{eth_half_life}} {{eth_reuse}} {{eth_suppress}} {{eth_max_suppress}} | no dampening
 load-interval {{eth_load_interval}}
 bundle id {{lag_ifc_id}} mode {{lacp_mode}}
 lacp period short | no lacp period short
 shutdown | no shutdown
</pre>

{{lag_ifc_id}} is parsed from {{lag_ifc_name}}  
example {{lag_ifc_name}} is Bundle-Ether100 -&gt; {{lag_ifc_id}} is 100  

*no shutdown* is a conversion of {{eth_enabled}} set *true*  
*shutdown* is a conversion of {{eth_enabled}} set *false*  
{{eth_subnet}} is a conversion of {{eth_prefix_length}}  
*no dampening* is a conversion of {{eth_damping_enabled}} set *false*  
*lacp period short* is a conversion of {{lacp_interval}} set to *frinx-openconfig-lacp:FAST*  
*no lacp period short* is a conversion of {{lacp_interval}} set to *frinx-openconfig-lacp:SLOW*  
if {{lacp_mode}} is not specified then command *bundle id {{lag_ifc_id}} mode on* is used  
*mode active* is a conversion of {{lacp_mode}} set to *frinx-openconfig-lacp:ACTIVE*  
*mode passive* is a conversion of {{lacp_mode}} set to *frinx-openconfig-lacp:PASSIVE*  

---
<pre>
interface {{eth_ifc_name}}.{{sub_ifc_index}}
 description {{eth_sub_description}}
 ipv4 address {{eth_sub_ip}} {{eth_sub_subnet}}
 ipv4 mtu {{eth_sub_ipv4_mtu}}
 load-interval {{eth_sub_load_interval}}
 encapsulation dot1q {{vlan_id}}
</pre>

{{eth_sub_subnet}} is conversion of {{eth_sub_prefix_length}}  

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/unitopo-units/tree/master/xr/xr-6.6/xr-6.6-interface-unit)

### Junos 14.1X53-D40.8

#### CLI

<pre>
set interfaces {{eth_ifc_name}} vlan-tagging
delete interfaces {{eth_ifc_name}} disable | set interfaces {{eth_ifc_name}} disable
set interfaces {{eth_ifc_name}} unit 0 family inet address {{eth_ip}}/{{eth_prefix_length}}
</pre>

*vlan-tagging* is a conversion of {{eth_tpid}} set *TPID_0X8100*  
*delete interfaces {{eth_ifc_name}} disable* is a conversion of {{eth_enabled}} set *true*  
*set interfaces {{eth_ifc_name}} disable* is conversion of {{eth_enabled}} set *false*  

<pre>
set interfaces {{eth_ifc_name}} unit {{sub_ifc_index}} vlan-id {{vlan_id}}
set interfaces {{eth_ifc_name}} unit {{sub_ifc_index}} description {{eth_sub_description}}
set interfaces {{eth_ifc_name}} unit {{sub_ifc_index}} family inet address {{eth_sub_ip}}/{{eth_sub_prefix_length}}
set interfaces {{eth_ifc_name}} unit {{sub_ifc_index}} disable
delete interfaces {{eth_ifc_name}} unit {{sub_ifc_index}} disable
</pre>

*set interfaces {{eth_intf_id}} unit {{sub_interface_index}} disable* is conversion of {{subif_enabled}} set *false*  
*delete interfaces {{eth_intf_id}} unit {{sub_interface_index}} disable* is a conversion of {{subif_enabled}} set *true*  

##### Unit

Link to github : [junos-unit](https://github.com/FRINXio/cli-units/tree/master/junos/interface)

### Junos 17.3R1.10

#### CLI

<pre>
set interfaces {{eth_ifc_name}} description {{eth_description}}
set interfaces {{eth_ifc_name}} mtu {{eth_mtu}}
set interfaces {{eth_ifc_name}} unit 0 family inet address {{eth_ip}}/{{eth_prefix_length}}
set interfaces {{eth_ifc_name}} damping enable
set interfaces {{eth_ifc_name}} damping half-life {{eth_half_life}}
set interfaces {{eth_ifc_name}} damping max-suppress {{eth_max_suppress}}
set interfaces {{eth_ifc_name}} damping reuse {{eth_reuse}}
set interfaces {{eth_ifc_name}} damping suppress {{eth_supress}}
set interfaces {{eth_ifc_name}} hold-time up {{eth_hold_time_up}} down {{eth_hold_time_down}}
set interfaces {{eth_ifc_name}} gigether-options 802.3ad {{lag_ifc_id}}
set interfaces {{eth_ifc_name}} aggregated-ether-options lacp {{lacp_mode}}
set interfaces {{eth_ifc_name}} aggregated-ether-options lacp periodic {{lacp_interval}}
delete interfaces {{eth_ifc_name}} disable | set interfaces {{eth_ifc_name}} disable
</pre>

{{lag_ifc_id}} is parsed from {{lag_ifc_name}}  
example {{lag_ifc_name}} is ae100 -&gt; {{lag_ifc_id}} is 100  

*delete interfaces {{eth_ifc_name}} disable* is a conversion of {{eth_enabled}} set *true*  
*set interfaces {{eth_ifc_name}} disable* is conversion of {{eth_enabled}} set *false* 

##### Unit

Link to github : [junos-unit](https://github.com/FRINXio/unitopo-units/tree/master/junos/junos-17/junos-17-interface-unit)

### Junos 18.2R1-S2.1

#### CLI

<pre>
set interfaces {{eth_intf_id}} unit 0 family inet address {{eth_ip}}/{{eth_prefix}}
delete interfaces {{eth_ifc_name}} disable | set interfaces {{eth_ifc_name}} disable
</pre>

*delete interfaces {{eth_ifc_name}} disable* is a conversion of {{eth_enabled}} set *true*  
*set interfaces {{eth_ifc_name}} disable* is conversion of {{eth_enabled}} set *false*  
In the case of *set interfaces ms-x/x/x*, set *iana-if-type:other* instead of *iana-if-type:ethernetCsmacd*

---
<pre>
set interfaces {{eth_ifc_name}} unit {{sub_ifc_index}} description {{eth_sub_description}}
set interfaces {{eth_ifc_name}} unit {{sub_ifc_index}} family inet address {{eth_sub_ip}}/{{eth_sub_prefix_length}}
delete interfaces {{eth_ifc_name}} unit {{sub_ifc_index}} disable | set interfaces {{eth_ifc_name}} unit {{sub_ifc_index}} disable
set interfaces {{rpm_ifc_index}} unit {{rpm_subintf_index}} rpm {{rpm_type}}
</pre>

*delete interfaces {{eth_ifc_name}} unit {{sub_ifc_index}} disable* is a conversion of {{subif_enabled}} set *true*  
*set interfaces {{eth_ifc_name}} unit {{sub_ifc_index}} disable* is conversion of {{subif_enabled}} set *false*  

##### Unit

Link to github : [junos-unit](https://github.com/FRINXio/unitopo-units/tree/master/junos/junos-18/junos-18-interface-unit)


### Brocade (V5.6.0fT163)

#### CLI

<pre>
tag-type {{eth_tpid}} {{eth_ifc_name}}

interface {{eth_ifc_name}}
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
interface {{eth_ifc_name}}
 ipv4 address {{eth_ip}} {{eth_subnet}}
</pre>

{{eth_subnet}} is conversion of {{eth_prefix_length}}

##### Unit

Link to github : [huawei-unit](https://github.com/FRINXio/cli-units/tree/master/huawei/interface)

### Dasan NOS SFU.RR.5.6p5

#### CLI

<pre>
bridge
 vlan add br{{tagged_vlan_ifc_id}} {{phy_port_id}} tagged
 vlan add br{{untagged_vlan_ifc_id}} {{phy_port_id}} untagged
 lacp port {{phy_port_id}} aggregator {{lag_ifc_id}}
 lacp port admin-key {{phy_port_id}} {{lacp_admin_key}}
 lacp port timeout {{phy_port_id}} short | no lacp port timeout {{phy_port_id}}
 jumbo-frame {{phy_port_id}} {{eth_mtu}}
 port enable {{phy_port_id}} | port disable {{phy_port_id}}
</pre>

{{phy_port_id}} is parsed from {{eth_ifc_name}}  
example {{eth_ifc_name}} is Ethernet1/1 -&gt; {{phy_port_id}} is 1/1  

{{lag_ifc_id}} is parsed from {{lag_ifc_name}}  
example {{lag_ifc_name}} is Bundle-Ether100 -&gt; {{lag_ifc_id}} is 100  

*port enable {{phy_port_id}}* is a conversion of {{eth_enabled}} set *true*  
*port disable {{phy_port_id}}* is a conversion of {{eth_enabled}} set *false*  
*lacp port timeout {{phy_port_id}} short* is a conversion of {{lacp_interval}} set to *frinx-openconfig-lacp:FAST*  
*no lacp port timeout {{phy_port_id}} short* is a conversion of {{lacp_interval}} set to *frinx-openconfig-lacp:SLOW*  

##### Unit

Link to github : [dasan-unit](https://github.com/FRINXio/cli-units/tree/master/dasan/interface)


### Ciena SAOS 6.14

#### CLI

<pre>
port
      set port {{eth_ifc_name}} description {{eth_description}}
      enable port {{eth_ifc_name}} | port disable port {{eth_ifc_name}}
      set port {{eth_ifc_name}} mode {{eth_phy_type}}
      set port {{eth_ifc_name}} max-frame-size {{eth_mtu}}
      set port {{eth_ifc_name}} vs-ingress-filter {{eth_vif}}
      set port {{eth_ifc_name}} acceptable-frame-type {{eth_aft}}
      set port {{eth_ifc_name}} ingress-to-egress-qmap {{eth_iteq}}

flow access-control set port {{eth_ifc_name}} forward-unlearned {{fwd_un}}
flow access-control set port {{eth_ifc_name}} max-dynamic-macs {{max_macs}}
</pre>

*port enable port {{eth_ifc_name}}* is a conversion of {{eth_enabled}} set *true*  
*port disable port {{eth_ifc_name}}* is a conversion of {{eth_enabled}} set *false*   
{{eth_phy_type}} can be "default" or "rj45" or "sfp"  
*vs-ingress-filter on* is a conversion of {{eth_vif}} set *true*  
*vs-ingress-filter off* is a conversion of {{eth_vif}} set *false*  
{{eth_aft}} can be "all", "tagged-only", "untagged-only"  
{{eth_iteq}} can be "Default-RCOS" or "NNI-NNI"  
*forward-unlearned on* is a conversion of {{fwd_un}} set *true*  
*forward-unlearned off* is a conversion of {{fwd_un}} set *false*   

<pre>
vlan add vlan {{vlan_ids}} port {{eth_ifc_name}}
</pre>
    
{{vlan_ids}} from usual range (max 4094)  

<pre>
virtual-circuit ethernet set port {{eth_ifc_name}} vlan-ethertype-policy {{eth_vep}}
</pre>

{{eth_vep}} can be "all" or "vlan-tpid"  
 
<pre>
l2-cft set port {{eth_ifc_name}} profile {{cft_profile_name}}
l2-cft enable port {{eth_ifc_name}}
l2-cft disable port {{eth_ifc_name}}
</pre>

l2-cft enable port {{eth_ifc_name}} is a conversion of {{cft_enabled}} set to true  
l2-cft disable port {{eth_ifc_name}} is a conversion of {{cft_enabled}} set to false

##### Unit

Link to github : [saos-unit]()
