# Probes

## URL

```
frinx-openconfig-probes:probes
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/probes/src/main/yang)

```javascript
"frinx-openconfig-probes": {
    "probes": {
        {
            "probe": [
                {
                    "name": "{{probe_name}}",
                    "config": {
                        "name": "{{probe_name}}",
                        "juniper-oc-probes:delegate-probes": true/false
                    },
                    "tests": {
                            {
                                "test": [
                                    "name": "{{probe_test_name}}",
                                    "config": {
                                        "name": "{{probe_test_name}}",
                                        "source": "{{probe_test_source_address}}",
                                        "juniper-oc-probes:destination-interface": "{{probe_test_dest_intf_id}}"
                                    },
                                    "target": {
                                        "config": {
                                            "address": "{{probe_test_target_address}}"
                                        }
                                    }
                                ]
                            }
                        }
                    }
                }
            }
        }
    }
}
```

## OS Configuration Commands

### Junos 18.2R2

#### CLI

<pre>
set services rpm probe {{probe_name}} delegate-probes
set services rpm probe {{probe_name}} test {{probe_test_name}} target address {{probe_test_target_address}}
set services rpm probe {{probe_name}} test {{probe_test_name}} source-address {{probe_test_source_address}}
set services rpm probe {{probe_name}} test {{probe_test_name}} destination-interface {{probe_test_dest_intf_id}}
</pre>

*set services rpm probe {{probe_name}} delegate-probes* is a conversion of &lt;delegate-probes&gt; set *true*  
*set services rpm probe {{probe_name}} test {{probe_test_name}} target address* is a conversion of &lt;target-type&gt; set *address*  


##### Unit

Link to github : [junos-unit](https://github.com/FRINXio/unitopo-units/tree/master/junos/junos-18/junos-18-rpm-unit)

