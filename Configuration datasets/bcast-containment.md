# Broadcast-Containment (Broadcast-containment filters)

## URL

```
frinx-openconfig-broadcast-containment:filters/filter/{{bc_name}}
```

## OPENCONFIG YANG

```javascript
{
    "frinx-openconfig-broadcast-containment:filters": {
        "enabled": {{bc_enable}},
        "filter": [
            {
                "name": "{{bc_name}}",
                "interfaces": {
                    "interface": [
                        {
                            "name": "{{eth_ifc_name}}",
                            "config": {
                                "name": "{{eth_ifc_name}}",
                                "filter": "{{bc_name}}"
                            }
                        }
                    ]
                },
                "config": {
                    "containment-clasification": [
                        "unknown-ucast",
                        "bcast"
                    ],
                    "rate": {{speed}}
                }
            }
        ]
    }
}
```

## OS Configuration Commands

### Ciena SAOS 6.14

#### CLI

<pre>
broadcast-containment create filter {{bc_name}}
broadcast-containment set filter {{bc_name}} kbps {{speed}}
broadcast-containment set filter {{bc_name}} containment-classification bcast,unknown-ucast
broadcast-containment add filter {{bc_name}} port {{eth_ifc_name}}
broadcast-containment {{bc_enable}}
</pre>

{{bc_enable}} Enable broadcast containment to use the broadcast containment feature. By default, is disabled. Values are enable/disable.

##### Unit

