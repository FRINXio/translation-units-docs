# Open Shortest Path First (OSPF)

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance/default/protocols/protocol/frinx-openconfig-policy-types:OSPF/{{ospf}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/ospf/src/main/yang)

```javascript
{
    "protocol": [
        {
            "name": {{ospf}},
            "identifier": "frinx-openconfig-policy-types:OSPF",
            "config": {
                "name": {{ospf}},
                "identifier": "frinx-openconfig-policy-types:OSPF"
            },
            "ospfv2": {
                "global": {
                    "timers": {
                        "max-metric": {   // non cisco devices
                            "config": {
                                "set": true,
                                "timeout": {{ospf_timeout}},
                                "include": [ 
                                    "frinx-openconfig-ospf-types":"MAX_METRIC_INCLUDE_STUB", 
                                    "frinx-openconfig-ospf-types":"MAX_METRIC_INCLUDE_TYPE2_EXTERNAL"
                                ]
                            }
                        },
                        "frinx-cisco-ospf-extension:max-metric-timers" {
                            "max-metric-timer": [
                                {
                                    "trigger": {{ospf_trigger}},
                                    "config": {
                                        "trigger": {{ospf_trigger}}, // frinx-openconfig-ospf-types:MAX_METRIC_ON_SYSTEM_BOOT or MAX_METRIC_ON_SWITCHOVER
                                        "timeout": {{ospf_trigger_timeout}},
                                        "include": [ 
                                            "frinx-openconfig-ospf-types":"MAX_METRIC_INCLUDE_STUB", 
                                            "frinx-openconfig-ospf-types":"MAX_METRIC_INCLUDE_TYPE2_EXTERNAL",
                                            "frinx-cisco-ospf-extension":"MAX_METRIC_SUMMARY_LSA"
                                        ]
                                    }
                                }
                            ]
                        }
                    }
                },
                "areas": {
                    "area": [
                        {
                            "identifier":{{ospf_area_id}},
                            "config": {
                                "identifier": {{ospf_area_id}}
                            },
                            "interfaces": {
                                "interface": [
                                    {
                                        "id": "{{ospf_interface}}",
                                        "config": {
                                            "id": "{{ospf_interface}}",
                                            "network-type": "{{ospf_network_type}}",
                                            "frinx-ospf-extension:enabled": {{ospf_interface_enabled}},
                                            "metric": {{ospf_cost}},
                                            "passive": {{ospf_passive}},
                                            "priority": {{ospf_priority}}
                                        },
                                        "mpls": {
                                            "igp-ldp-sync": {
                                                "config": {
                                                    "enabled": {{igp_ldp_sync_enabled}}
                                                }
                                            }
                                        },
                                        "timers": {
                                            "config": {
                                                "retransmission-interval": {{ospf_retrans_interval}}
                                            }
                                        },
                                        "frinx-bfd-extension:enable-bfd": {
                                            "config": {
                                                "enabled": {{bfd_interface_enabled}}
                                            }
                                        },
                                        "frinx-bfd-extension:bfd": {
                                            "config": {
                                                "multiplier": {{bfd_interface_multiplier}},
                                                "min-interval": {{bfd_interface_min_interval}},
                                                "min-receive-interval": {{bfd_interface_min_recieve_interval}}
                                            }
                                        }
                                        "frinx-ospf-extension:authentication": {
                                            "config": {
                                                "type": "auth-type:md5",
                                                "passwords": {
                                                    "password": [
                                                        {
                                                            "auth-id": {{ospf_auth_id}},
                                                            "config": {
                                                                "auth-id": {{ospf_auth_id}},
                                                                "auth-password": {{ospf_auth_password}}
                                                            }
                                                        }
                                                    ]
                                                }
                                            }
                                        }
                                    }
                                ]
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

*include-stub* is a conversion of *MAX_METRIC_INCLUDE_STUB* in the include list of the max-metric-timer  
*external-lsa* is a conversion of *MAX_METRIC_INCLUDE_TYPE2_EXTERNAL* in the include list of the max-metric-timer  
*summary-lsa* is a conversion of *MAX_METRIC_SUMMARY_LSA* in the include list of the max-metric-timer  

### Cisco IOS XR 5.3.4

#### CLI

<pre>
router ospf {{ospf}}
 max-metric router-lsa on-startup {{ospf_timeout}} include-stub summary-lsa external-lsa
 max-metric router-lsa {{ospf_trigger}} {{ospf_trigger_timeout}} include-stub summary-lsa external-lsa
 area {{ospf_area_id}}
  interface {{ospf_interface}}
   cost {{ospf_cost}}
   passive {{ospf_passive}}
   bfd fast-detect <disable>
   mpls ldp sync
   mpls ldp sync disabled
</pre>
*bfd fast-detect* is a conversion of {{bfd_interface_enabled}} set *true*  
*bfd fast-detect disable* is a conversion of {{bfd_interface_enabled}} set *false*  
*mpls ldp sync* is a conversion of {{igp_ldp_sync_enabled}} set *true*  
*mpls ldp sync disabled* is a conversion of {{igp_ldp_sync_enabled}} set *false*  
*passive enable* is a conversion of {{ospf_passive}} set *true*  
*passive disabled* is a conversion of {{ospf_passive}} set *false*

*{{ospf_trigger}}* value MAX_METRIC_ON_SYSTEM_BOOT is to be converted to *on-startup*  
*{{ospf_trigger}}* value MAX_METRIC_ON_SWITCHOVER is to be converted to *on-switchover*  

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/ospf)

### Cisco IOS XR 6.6.2

#### CLI

<pre>
router ospf {{ospf}}
 area {{ospf_area_id}}
  interface {{ospf_interface}}
</pre>

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/ospf)

### Junos 14.1X53-D40.8

#### CLI

<pre>
set protocols ospf area {{ospf_area_id}} interface {{ospf_interface}} interface-type {{ospf_network_type}}
set protocols ospf area {{ospf_area_id}} interface {{ospf_interface}} metric {{ospf_cost}}
set protocols ospf area {{ospf_area_id}} interface {{ospf_interface}} priority {{ospf_priority}}
delete protocols ospf area {{ospf_area_id}} interface {{ospf_interface}} disable 
| set protocols ospf area {{ospf_area_id}} interface {{ospf_interface}} disable
set protocols ospf area {{ospf_area_id}} interface {{ospf_interface}} authentication md5 {{ospf_auth_id}} key {{ospf_auth_password}}
| delete protocols ospf area {{ospf_area_id}} interface {{ospf_interface}} authentication
set protocols ospf area {{ospf_area_id}} interface {{ospf_interface}} bfd-liveness-detection minimum-interval {{bfd_interface_min_interval}}
set protocols ospf area {{ospf_area_id}} interface {{ospf_interface}} bfd-liveness-detection minimum-receive-interval {{bfd_interface_min_recieve_interval}}
set protocols ospf area {{ospf_area_id}} interface {{ospf_interface}} bfd-liveness-detection multiplier {{bfd_interface_multiplier}}
set protocols ospf area {{ospf_area_id}} interface {{ospf_interface}} retransmit-interval {{ospf_retrans_interval}}
</pre>

*delete protocols ospf area {{ospf_area_id}} interface {{ospf_interface}} disable* is a conversion of {{ospf_interface_enabled}} set *true*  
*set protocols ospf area {{ospf_area_id}} interface {{ospf_interface}} disable* is a conversion of {{ospf_interface_enabled}} set *false*  

##### Unit

Link to github : [junos-unit](https://github.com/FRINXio/cli-units/tree/master/junos/ospf)

### Junos 17.3R1.10

#### CLI

<pre>
set protocols ospf overload timeout {{ospf_timeout}}
set protocols ospf area {{ospf_area_id}} interface {{ospf_interface}} metric {{ospf_cost}}
</pre>

##### Unit

Link to github : [junos-unit](https://github.com/FRINXio/unitopo-units/tree/master/junos/junos-17/junos-17-ospf-unit)
