# Intermediate System to Intermediate System (IS-IS)

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance/default/protocols/protocol/frinx-openconfig-policy-types:ISIS/{{isis}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/isis/src/main/yang)

```javascript
{
    "protocol": [
        {
            "name": {{isis}},
            "identifier": "frinx-openconfig-policy-types:ISIS",
            "config": {
                "name": {{isis}},
                "identifier": "frinx-openconfig-policy-types:ISIS"
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
*point-to-point* is a conversion of {{isis_circuit_type}} set *circuit-type:POINT_TO_POINT*  

{{isis_interface_afi_name}} value afi-type:IPV6 is to be converted to *ipv6*  
{{isis_interface_safi_name}} value safi-type:UNICAST is to be converted to *unicast*  
{{isis_interface_level}} value level-type:LEVEL_1 is to be converted to *level-1*  
{{isis_interface_level}} value level-type:LEVEL_2 is to be converted to *level-2*  
{{isis_interface_level}} value level-type:LEVEL_1_2 is to be converted to *level-1-2*  

