# CABLE interface

## URL

```
frinx-openconfig-interfaces:interfaces/interface={{cable_ifc_name}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/interfaces/src/main/yang)

```javascript
{
    "interface": [
        {
            "name": "{{cable_ifc_name}}",
            "config": {
                "type": "iana-if-type:other",
                "name": "{{cable_ifc_name}}"
            },
            "frinx-rphy-if-extension:cable": {
                "upstream": {
                    "upstream-bonding-groups": {
                        "bonding-group": [
                            {
                                "id": "{{bonding_group_id}}",
                                "config": {
                                    "attributes": "{{bonding_group_attributes}}",
                                    "id": "{{bonding_group_id}}",
                                    "upstream": "{{bonding_group_upstream}}"
                                }
                            }
                        ]
                    }
                },
                "config": {
                    "bundle": "{{bundle_id}}"
                }
            },
            "frinx-rphy-if-extension:downstream": {
                "config": {
                    "rf-channels": "{{downstream_rf_channels}}",
                    "name": "{{downstream_name}}"
                }
            },
            "frinx-rphy-if-extension:upstream": {
                "upstream-cables": [
                    {
                        "id": "{{upstream_cable_id}}",
                        "config": {
                            "id": "{{upstream_cable_id}}",
                            "us-channel": "{{upstream_channle}}",
                            "name": "{{upstream_name}}"
                        }
                    }
                ]
            }
        }
    ]
}
```

## OS Configuration Commands

### IOS XE 16

#### CLI

<pre>
!
interface {{cable_ifc_name}}
 downstream {{downstream_name}} rf-channel {{downstream_rf_channels}}
 downstream {{downstream_name}} rf-channel {{downstream_rf_channels}}
 downstream {{downstream_name}} rf-channel {{downstream_rf_channels}}
 downstream {{downstream_name}} rf-channel {{downstream_rf_channels}}
 upstream {{upstream_cable_id}} {{upstream_name}} us-channel {{upstream_channle}}
 cable upstream bonding-group {{bonding_group_id}}
  upstream {{bonding_group_upstream}}
  attributes {{bonding_group_attributes}}
 cable bundle {{bundle_id}}
end
!
</pre>

{{downstream_rf_channels}} are read from all lines and input into one attribute "rf-channels"
{{upstream_name}} and {{downstream_name}} are in commands input with whitespace dividing name and number (Downstream-Cable 1/0/16)

##### Unit

Link to github : [ios-xe-unit](https://github.com/FRINXio/cli-units/tree/master/ios/interface)