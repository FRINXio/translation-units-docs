# Intermediate System to Intermediate System (IS-IS)

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance=default/protocols/protocol=frinx%2Dopenconfig%2Dpolicy%2Dtypes%3AISIS,{{isis}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/isis/src/main/yang)

```javascript
{
    "protocol": [
        {
            "identifier": "frinx-openconfig-policy-types:ISIS",
            "name": {{isis}}
            "config": {
                "identifier": "frinx-openconfig-policy-types:ISIS",
                "name": {{isis}}
            },
            "isis": {
                "interfaces": {
                    "interface": [
                        {
                            "interface-id": "{{isis_interface}}",
                            "config": {
                                "interface-id": "{{isis_interface}}",
                                "circuit-type": "{{isis_circuit_type}}",
                                "frinx-isis-extension:level-capability": "{{isis_interface_level}}"
                            },
                            "authentication" {
                                "key": {
                                    "config": {
                                        "auth-password": "Encrypted[{{isis_interface_password}}]"
                                    }
                                }
                            },
                            "afi-safi" {
                                "af": [
                                    {
                                        "afi-name": "{{isis_interface_afi_name}}",
                                        "safi-name": "{{isis_interface_safi_name}}",
                                        "config": {
                                            "afi-name": "{{isis_interface_afi_name}}",
                                            "safi-name": "{{isis_interface_safi_name}}",
                                            "frinx-isis-extension:metric": {{isis_interface_metric}}
                                        }
                                    }
                                ]
                            },
                            "timers" {
                                "config": {
                                    "frinx-isis-extension:retransmission-interval": {{isis_retrans_interval}}
                                }
                            }
                        }
                    ]
                },
                "global": {
                    "config": {
                        "frinx-isis-extension:max-link-metric": [
                            {{max_link_metric}}
                        ]
                    },
                    "afi-safi" {
                        "af": [
                            {
                                "afi-name": "{{global_afi_name}}",
                                "safi-name": "{{global_safi_name}}",
                                "config": {
                                    "afi-name": "{{global_afi_name}}",
                                    "safi-name": "{{global_safi_name}}"
                                },
                                "frinx-isis-extension:redistributions": {
                                    "redistribution": [
                                        {
                                            "protocol": isis,
                                            "instance": {{redist_instance}},
                                            "config": {
                                                "protocol": isis,
                                                "instance": {{redist_instance}},
                                                "level": {{redist_level}},
                                                "metric": {{redist_metric}},
                                                "route-policy": {{redist_route_policy}}
                                            }
                                        }
                                    ]
                                }
                            }
                        ]
                    }
                }
            }
        }
    ]
}
```

## OS Configuration Commands
### Cisco IOS XR 6.2.3

#### CLI

<pre>
router isis {{isis}}
 interface {{isis_interface}}
  circuit-type {{isis_interface_level}}
  point-to-point
  hello-password hmac-md5 encrypted {{isis_interface_password}}
  retransmit-interval {{isis_retrans_interval}}
  address-family {{isis_interface_afi_name}} {{isis_interface_safi_name}}
   metric {{isis_interface_metric}}
</pre>
*point-to-point* is a conversion of {{isis_circuit_type}} set *POINT_TO_POINT*  

{{isis_interface_afi_name}} value *frinx-openconfig-isis-types:IPV6* is to be converted to *ipv6*  
{{isis_interface_safi_name}} value *frinx-openconfig-isis-types:UNICAST* is to be converted to *unicast*  
{{isis_interface_level}} value *LEVEL_1* is to be converted to *level-1*  
{{isis_interface_level}} value *LEVEL_2* is to be converted to *level-2*  
{{isis_interface_level}} value *LEVEL_1_2* is to be converted to *level-1-2*  

### Cisco IOS XR 6.6.1(CLI)

#### CLI

<pre>
router isis {{isis}}
 max-link-metric [level 1|2]
 address-family {{global_afi_name}} {{global_safi_name}}
  redistribute isis {{redist_instance}} {{redist_level_option}} metric {{redist_metric}} route-policy {{redist_route_policy}}
</pre>

{{max_link_metric}} value *frinx-isis-extension:NOT_SET* is to be converted to *max-link-metric*  
{{max_link_metric}} value *frinx-isis-extension:LEVEL_1* is to be converted to *max-link-metric level 1*  
{{max_link_metric}} value *frinx-isis-extension:LEVEL_2* is to be converted to *max-link-metric level 2*  

{{global_afi_name}} value *frinx-openconfig-isis-types:IPV6* is to be converted to *ipv6*  
{{global_safi_name}} value *frinx-openconfig-isis-types:UNICAST* is to be converted to *unicast*  

{{redist_level_option}} is converted from {{redist_level}}.
* if {{redist_level}} is *LEVEL_1*, then {{redist_level_option}} is set as *level-1*
* if {{redist_level}} is *LEVEL_2*, then {{redist_level_option}} is set as *level-2*
* if {{redist_level}} is *LEVEL_1_2*, then {{redist_level_option}} is set as *level-1-2*
