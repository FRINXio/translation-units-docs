# L2VSI (L2 virtual switch instance virtual circuit)

Interconnects L2VSI with a vlan-based upstream path

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance/{{vsicp_ni_name}}
```

## OPENCONFIG YANG

```javascript
{
    "network-instance": [
        {
            "name": "{{vsicp_ni_name}}",
            "config": {
                "name": "{{vsicp_ni_name}}"
                "type": "L2VSICP" //new NI type
                "enabled": true
            },
            "vlans": {
                "vlan": [
                    {
                        "vlan-id": "{{vsicp_ni_vlan_id}}",
                        "config": {
                            "vlan-id": "{{vsicp_ni_vlan_id}}",
                            "statistics":  {{vsicp_ni_vlan_statistics}}
                        } 
                    }
                ]
            }
        }
    ]
}
```

## OS Configuration Commands

### Ciena SAOS 6.14

#### CLI

<pre>
virtual-circuit ethernet create vc {{vsicp_ni_name}} vlan {{vsicp_ni_vlan_id}} statistics {{vsicp_ni_vlan_statistics}}
</pre>

*statistics on* is a conversion of {{vsicp_ni_vlan_statistics}} set true  
*statistics off* is a conversion of {{vsicp_ni_vlan_statistics}} set false


##### Unit
