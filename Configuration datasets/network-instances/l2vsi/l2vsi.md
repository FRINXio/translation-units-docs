# L2VSI (L2 virtual switch instance)

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance/{{vsi_ni_name}}
```

## OPENCONFIG YANG

```javascript
{
    "network-instance": [
        {
            "name": "{{vsi_ni_name}}",
            "config": {
                "name": "{{vsi_ni_name}}",
                "description": "{{vsi_ni_description}}",
                "type": "L2VSI",
                "enabled": true,
                "frinx-saos-vs-extension:encap-cos-policy": {{vsi_ni_encap_cos_policy}},
                "frinx-saos-vs-extension:encap-fixed-dot1dpri": {{vsi_ni_encap_fixed_dot1dpri}},  
                "frinx-saos-vs-extension:tagged-pvst-l2pt": true  
            },
            "connection-points": {
                "connection-point": [
                    {
                        "connection-point-id": "{{vsi_cp_name}}",
                        "config": {
                            "connection-point-id": "{{vsi_cp_name}}"
                        } 
                    }
                ]
            },
            "interfaces": {
                "interface": [
                    {
                        "id": "{{vsi_ni_if_name}}",
                        "config": {
                            "id": "{{vsi_ni_if_name}}",
                            "interface": "{{vsi_ni_if_name}}",
                            "frinx-saos-ni-if-extension:type": "iana-if-type:ieee8023adLag/iana-if-type:l2vlan"
                        } 
                    }
                ]
            },
            "frinx-saos-virtual-ring-extension:rings": {
                "ring": [
                    {
                        "name": "{{ring_name}}",
                        "config": {
                            "name": "{{ring_name}}"
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
virtual-switch ethernet create vs {{vsi_ni_name}} vc {{vsi_cp_name}}
virtual-switch ethernet set vs {{vsi_ni_name}} description {{vsi_ni_description}}
virtual-switch ethernet set vs {{vsi_ni_name}} encap-cos-policy {{vsi_ni_encap_cos_policy}}
virtual-switch ethernet set vs {{vsi_ni_name}} encap-fixed-dot1dpri {{vsi_ni_encap_fixed_dot1dpri}}
virtual-switch ethernet add vs {{vsi_ni_name}} port {{vsi_ni_if_name}}
port set port {{vsi_ni_if_name}} untagged-ctrl-vs {{vsi_ni_name}}
port set port {{vsi_ni_if_name}} untagged-data-vs {{vsi_ni_name}}
l2-cft tagged-pvst-l2pt enable vs {{vsi_ni_name}}
</pre>

{{vsi_ni_encap_cos_policy}} can have values <dot1dpri-inherit | fixed | ip-prec-inherit | phbg-inherit | port-inherit | vs-inherit>  
*l2-cft tagged-pvst-l2pt enable vs {{vsi_ni_name}}* is a conversion of "tagged-pvst-l2pt" field set to true  
*l2-cft tagged-pvst-l2pt disable vs {{vsi_ni_name}}* is a conversion of "tagged-pvst-l2pt" field set to false

### Ciena SAOS 8

#### CLI

<pre>
virtual-switch create vs {{vsi_ni_name}}
virtual-switch set vs {{vsi_ni_name}} description {{vsi_ni_description}} 
ring-protection virtual-ring add ring {{ring_name}} vs {{vsi_ni_name}} 
ring-protection virtual-ring remove ring {{ring_name}} vs {{vsi_ni_name}}
</pre>

<pre>
virtual-switch interface attach cpu-subinterface {{vsi_ni_if_name}} vs {{vsi_ni_name}}
virtual-switch interface attach sub-port {{vsi_ni_if_name}} vs {{vs_ni_name}}
</pre>

cpu-subinterface command is sent, if the type of the interface added is *iana-if-type:l2vlan*  


sub-port command is sent, if the type of the interface added is *iana-if-type:ieee8023adLag*   

*{{vsi_ni_if_name}}* in this case needs to have form <parent_ifc_name.subifc_name> . This can be derived from : https://github.com/FRINXio/translation-units-docs/blob/master/Configuration%20datasets/interfaces/lag_interface.md



