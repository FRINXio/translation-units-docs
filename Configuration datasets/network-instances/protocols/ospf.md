# Open Shortest Path First (OSPF)

## URL

```
frinx-openconfig-network-instance:network-instance/network-instance/default/protocols/protocol/frinx-openconfig-policy-types:OSPF/{{ospf}}
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
                        "max-metric": {
                            "config": {
                                "set": true,
                                "timeout": {{ospf_timeout}},
                                "include": [ 
                                    "frinx-openconfig-ospf-types:MAX_METRIC_INCLUDE_STUB", 
                                    "frinx-openconfig-ospf-types:MAX_METRIC_INCLUDE_TYPE2_EXTERNAL",
                                    "frinx-openconfig-ospf-types:MAX_METRIC_INCLUDE",
                                    "frinx-cisco-ospf-extension:MAX_METRIC_SUMMARY_LSA"
                                ]
                            }
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
                                            "metric": {{ospf_cost}}
                                        },
                                        "frinx-bfd-extension:enable-bfd": {
                                            "config": {
                                                "enabled": {{bfd_interface_enabled}}
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

### Cisco IOS XR 5.3.4

#### CLI

<pre>
router ospf {{ospf}}
 max-metric router-lsa on-startup {{ospf_timeout}} include-stub summary-lsa external-lsa
 area {{ospf_area_id}
  interface {{ospf_interface}}
   cost {{ospf_cost}}
   bfd fast-detect <disable>
</pre>
*bfd fast-detect* is a conversion of {{bfd_interface_enabled}} set *true*  
*bfd fast-detect disable* is a conversion of {{bfd_interface_enabled}} set *false*

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/ospf)

### Junos 17.3R1.10

#### CLI

<pre>
set protocols ospf overload timeout {{ospf_timeout}}
set protocols ospf area {{ospf_area_id}} interface {{ospf_interface}} metric {{ospf_cost}}
</pre>

##### Unit

Link to github : [junos-unit](https://github.com/FRINXio/unitopo-units/tree/master/junos/junos-17-ospf-unit)
