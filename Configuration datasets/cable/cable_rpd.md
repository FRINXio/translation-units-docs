# cable RPD

## URL

```
frinx-openconfig-cable:cable/rpds/rpd={{rpd_id}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/cable/src/main/yang)

```javascript
{
    "rpd": [
        {
            "id": "{{rpd_id}}",
            "core-interface": {
                "config": {
                    "network-delay": "{{interface_network_delay}}",
                    "name": "{{core_interface_name}}",
                    "principal": {{principal_enabled}}
                },
                "if-rpd-us": {
                    "upstream-ports": [
                        {
                            "id": "{{interface_rpd_upstream_id}}",
                            "config": {
                                "cable-controller": "{{upstream_cable_controller}}",
                                "profile": "{{upstream_controller_profile}}"
                            }
                        }
                    ]
                },
                "if-rpd-ds": {
                    "downstream-ports": [
                        {
                            "id": "{{interface_rpd_downstream_id}}",
                            "config": {
                                "cable-controller": "{{downstream_cable_controller}}",
                                "profile": "{{downstream_controller_profile}}"
                            }
                        }
                    ]
                }
            },
            "rpd-us": {
                "upstream-commands": [
                    {
                        "id": "{{rpd_upstream_id}}",
                        "config": {
                            "description": "{{rpd_upstream_descrpition}}"
                        }
                    }
                ]
            },
            "rpd-ds": {
                "downstream-commands": [
                    {
                        "id": "{{rpd_downstream_id}}",
                        "config": {
                            "base-power": "{{downstream_base_power}}"
                        }
                    }
                ]
            },
            "config": {
                "identifier": "{{rpd_mac_address}}",
                "rpd-55d1-us-event-profile": "{{rpd_55d1_us_event_profile}}",
                "r-dti": "{{profile_id}}",
                "rpd-event-profile": "{{rpd_event_profile}}",
            }
        }
    ]
}
```

## OS Configuration Commands

### IOS XE 16

#### CLI

<pre>
cable rpd {{rpd_id}}
 identifier {{rpd_mac_address}}
 rpd-us {{rpd_upstream_id}} description {{rpd_upstream_descrpition}}
 rpd-ds {{rpd_downstream_id}} base-power {{downstream_base_power}}
 core-interface {{core_interface_name}}
  {{principal_enabled}}
  rpd-ds {{interface_rpd_downstream_id}} {{downstream_cable_controller}} profile {{downstream_controller_profile}}
  rpd-us {{interface_rpd_upstream_id}} {{upstream_cable_controller}} profile {{upstream_controller_profile}}
  network-delay {{interface_network_delay}}
 r-dti {{profile_id}}
 rpd-event profile {{rpd_event_profile}}
 rpd-55d1-us-event profile {{rpd_55d1_us_event_profile}}
</pre>

{{downstream_cable_controller}} and {{upstream_cable_controller}} are in commands input with whitespace dividing name and number (Downstream-Cable 1/0/16)

*no principal* is a conversion of {{principal_enabled}} set *false*  
*principal* is a conversion of {{principal_enabled}} set *true*  

##### Unit

Link to github : [ios-xe-unit](https://github.com/FRINXio/cli-units/tree/master/cable/rpd)