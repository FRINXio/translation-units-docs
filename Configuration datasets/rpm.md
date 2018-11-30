# Real-time performance monitoring (RPM)

## URL

```
frinx-rpm:rpm
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/rpm/src/main/yang)

```javascript
"rpm": {
    "interfaces": {
        "interface": [
            {
                "interface-id": "{{rpm_intf_id}}",
                "config": {
                    "interface-id": "{{rpm_intf_id}}",
                    "rpm-type": "{{rpm_type}}"
                }
            }
        ]
    },
    "probes": {
        "probe": [
            {
                "probe-name": "{{probe_name}}",
                "config": {
                    "probe-name": "{{probe_name}}",
                    "delegate-probes": true/false
                },
                "tests": {
                    "test": [
                        {
                            "test-name": "{{probe_test_name}}",
                            "config": {
                                "test-name": "{{probe_test_name}}",
                                "target-type": address,
                                "target-address": "{{probe_test_target_address}}",
                                "source-address": "{{probe_test_source_address}}",
                                "destination-interface-id": "{{probe_test_dest_intf_id}}"
                            }
                        }
                    ]
                }
            }
        ]
    },
    "static-route": {
        "endpoints": {
            "endpoint": [
                {
                    "endpoint-id": "{{rpm_endpoint_id}}",
                    "config": {
                        "endpoint-id": "{{rpm_endpoint_id}}"
                    }
                },
                "tests": {
                    "test": [
                        {
                            "test-name": "{{rpm_endpoint_test_name}}",
                            "config": {
                                "test-name": "{{rpm_endpoint_test_name}}",
                                "next-hop": "{{rpm_endpoint_next_hop}}",
                                "routing-instance-name": "{{rpm_endpoint_routing_instance_name}}",
                                "interface-id": "{{rpm_endpoint_intf_id}}",
                                "static-route-name": [
                                    "{{rpm_endpoint_static_route_name}}"
                                ]
                            }
                        }
                    ]
                }
            ]
        }
    }
}
```

## OS Configuration Commands

### Junos 18.2R2

#### CLI

<pre>
set interfaces {{rpm_intf_index}} unit {{rpm_subintf_index}} rpm {{rpm_type}}
set services rpm probe {{probe_name}} delegate-probes
set services rpm probe {{probe_name}} test {{probe_test_name}} target address {{probe_test_target_address}}
set services rpm probe {{probe_name}} test {{probe_test_name}} source-address {{probe_test_source_address}}
set services rpm probe {{probe_name}} test {{probe_test_name}} destination-interface {{probe_test_dest_intf_id}}
</pre>

rpm_intf_index , rpm_subintf_index is a conversion of {{rpm_intf_id}} set {{rpm_intf_index}}.{{rpm_subintf_index}}  
*set interfaces {{rpm_intf_index}} unit {{rpm_subintf_index}} rpm client-delegate-probes* is a conversion of &lt;rpm-type&gt; set *client-delegate-probes*  
*set services rpm probe {{probe_name}} delegate-probes* is a conversion of &lt;delegate-probes&gt; set *true*  
*set services rpm probe {{probe_name}} test {{probe_test_name}} target address* is a conversion of &lt;target-type&gt; set *address*  


<pre>
set rpmstaticroute:rpmstaticroute endpoint {{rpm_endpoint_id}} test {{rpm_endpoint_test_name}} route {{rpm_endpoint_static_route_name}}
set rpmstaticroute:rpmstaticroute endpoint {{rpm_endpoint_id}} test {{rpm_endpoint_test_name}} next-hop {{rpm_endpoint_next_hop}}
set rpmstaticroute:rpmstaticroute endpoint {{rpm_endpoint_id}} test {{rpm_endpoint_test_name}} routing-instance {{rpm_endpoint_routing_instance_name}}
set rpmstaticroute:rpmstaticroute endpoint {{rpm_endpoint_id}} test {{rpm_endpoint_test_name}} interface {{rpm_endpoint_intf_id}}
</pre>


##### Unit

Link to github : [junos-unit](https://github.com/FRINXio/unitopo-units/tree/master/junos/junos-18/junos-18-rpm-unit)
