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
            "config": {
                "name": "{{vsi_ni_name}}"
                "type": "L2VSICP" //new NI type
                "enabled": true
            }
            "connection-points": {
                "connection-point": [
                    {
                        "config": {
                            "connection-point-id": "{{vsicp_ni_name}}"
                        } 
                    }
                ]
            }
            "vlans": {
                "vlan": [
                    {
                        "config": {
                            "vlan-id": "{{vsicp_ni_vlan_id}}"
                            "statistics":  "{{vsicp_ni_vlan_statistics}}" //new augument (can be true of false)
                        } 
                    }
                ]
            }

        }
    ]
}
```

## OS Configuration Commands

### Ciena 3916/3930

#### CLI

<pre>
virtual-circuit ethernet create vc {{vsicp_ni_name}} vlan {{vsicp_ni_vlan_id}} statistics on 
</pre>

*statistics on* is a conversion of vsicp_ni_vlan_statistics = true

##### Unit

NOT IMPLEMENTED
