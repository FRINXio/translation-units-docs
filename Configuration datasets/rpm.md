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
        {
            "interface": [
                {
                    "interface-id": "{{rpm_intf_id}}",
                    "config": {
                        "interface-id": "{{rpm_intf_id}}",
                        "rpm-type": "{{rpm_type}}"
                    }
                }
            ]
        }
    },
    "probe": [
        {
            "probe-name": "{{probe_name}}",
            "config": {
                "probe-name": "{{probe_name}}"
            },
            "test": [
                "test-name": "{{probe_test_name}}",
                "config": {
                    "test-name": "{{probe_test_name}}",
                    "address-type": IPV4,
                    "target-address": "{{probe_test_target_address}}",
                    "source-address": "{{probe_test_source_address}}",
                    "interface-id": "{{probe_test_intf_id}}"
            ]
        }
    ],
    "static-route": {
        "endpoints": {
            "endpoint": [
                "endpoint-id": "{{rpm_endpoint_id}}",
                "config": {
                    "endpoint-id": "{{rpm_endpoint_id}}"
                },
                "test": [
                    "test-name": "{{rpm_endpoint_test_name}}",
                    "config": {
                        "test-name": "{{rpm_endpoint_test_name}}",
                        "next-hop": "{{rpm_endpoint_next_hop}}",
                        "instance-name": {{rpm_endpoint_instance_name}},
                        "interface-id": "{{rpm_endpoint_intf_id}}"
                    },
                    "routes": {
                        "route": [
                            "prefix": "{{rpm_endpoint_route_prefix}}",
                            "config": {
                                "prefix": "{{rpm_endpoint_route_prefix}}"
                            }
                        ]
                    }
                ]
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
set services rpm probe {{probe_name}} test {{probe_test_name}} target address {{probe_test_target_address}}
set services rpm probe {{probe_name}} test {{probe_test_name}} source-address {{probe_test_source_address}}
set services rpm probe {{probe_name}} test {{probe_test_name}} destination-interface {{probe_test_intf_id}}
set rpmstaticroute:rpmstaticroute endpoint {{rpm_endpoint_id}} test {{rpm_endpoint_test_name}} route {{rpm_endpoint_route_prefix}}
set rpmstaticroute:rpmstaticroute endpoint {{rpm_endpoint_id}} test {{rpm_endpoint_test_name}} next-hop {{rpm_endpoint_next_hop}}
set rpmstaticroute:rpmstaticroute endpoint {{rpm_endpoint_id}} test {{rpm_endpoint_test_name}} routing-instance {{rpm_endpoint_instance_name}}
set rpmstaticroute:rpmstaticroute endpoint {{rpm_endpoint_id}} test {{rpm_endpoint_test_name}} interface {{rpm_endpoint_intf_id}}
</pre>

rpm_intf_index , rpm_subintf_index is a conversion of {{rpm_intf_id}} set {{rpm_intf_index}}.{{rpm_subintf_index}}
*client-delegate-probes* is a conversion of {{rpm_type}} set to CLIENT_DELEGATE_PROBES


##### Unit

Link to github : [junos-unit](https://github.com/FRINXio/unitopo-units/tree/master/junos/junos-18/junos-18-rpm-unit)