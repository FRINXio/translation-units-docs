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
                            "index": 0
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
                    "frinx-openconfig-if-aggregate:aggregate-id": "{{eth_lag_intf-id}}"
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
 dampening {{eth_half-life}} {{reuse}} {{suppress}} {{max-suppress}} | no dampening
 carrier-delay up {{eth_hold_time_up}} down {{eth_hold_time_down}} 
 load-interval {{eth_load-interval}}
 bundle-id &lt;bundle-id&gt; mode on
 shutdown | no shutdown
</pre>

&lt;bundle-id&gt; is a conversion of {{eth_lag_intf-id}}  
*no shutdown* is a conversion of {{eth_enabled}} set *true*  
*shutdown* is a conversion of {{eth_enabled}} set *false*  
*no dampening* is a conversion of {{eth_damping_enabled}} set *false*  

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/interface)

### Junos 15.1F-6.9

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
set interfaces {{eth_intf_id}} gigether-options 802.3ad &lt;bundle-id&gt;
delete interface {{eth_intf_id}} disable | set interface {{eth_intf_id}} disable
</pre>

&lt;bundle-id&gt; is a conversion of {{eth_lag_intf-id}}  
*delete interface {{lag_intf_id}} disable* is a conversion of {{lag_enabled}} set *true*  
*set interface {{lag_intf_id}} disable* is conversion of {{lag_enabled}} set *false* 

##### Unit

NOT IMPLEMENTED

Link to github : [junos-unit]()

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
