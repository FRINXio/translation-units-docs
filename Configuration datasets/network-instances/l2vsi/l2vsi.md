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
            "config": {
                "name": "{{vsi_ni_name}}",
                "description": "{{vsi_ni_description}}",
                "type": "L2VSI",
                "enabled": true,
                "frinx-saos-vs-extension:encap-cos-policy": {{vsi_ni_encap_cos_policy}},
                "frinx-saos-vs-extension:encap-fixed-dot1dpri": {{vsi_ni_encap_fixed_dot1dpri}},
                "frinx-l2-cft-extension:cft" {
                    "name": {{cft_name}},
                    "config": {
                        "mode": {{cft_mode}},
                        "name": {{cft_name}},
                        "ctrl-protocols": {
                            "ctrl-protocol": [
                                {
                                    "name": {{cft_ctrl_protocol_name}},
                                    "disposition": {{cft_disposition}}
                                }
                            ]
                        }
                    }
                {
            }
            "connection-points": {
                "connection-point": [
                    {
                        "config": {
                            "connection-point-id": "{{vsi_cp_name}}"
                        } 
                    }
                ]
            }
            "interfaces": {
                "interface": [
                    {
                        "config": {
                            "id": "{{vsi_ni_if_name}}",
                            "interface": "{{vsi_ni_if_name}}",
                            "frinx-l2-cft-extension:interface-cft" {
                               "enabled": {{cft_enabled}},
                               "profile": {{cft_name}}
                            }
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
</pre>

{{vsi_ni_encap_cos_policy}} can have values <dot1dpri-inherit | fixed | ip-prec-inherit | phbg-inherit | port-inherit | vs-inherit>  

<pre>
l2-cft set mode {{cft_mode}}
l2-cft create profile {{cft_name}}
l2-cft protocol add profile {{cft_name}} ctrl-protocol {{cft_ctrl_protocol_name}} untagged-disposition {{cft_disposition}}
l2-cft set port {{vsi_ni_if_name}} profile {{cft_name}}
l2-cft enable port {{vsi_ni_if_name}}
</pre>

{{cft_mode}} can be <mef-ce1|mef-ce2>  
{{cft_ctrl_protocol_name}} can be <802.1x | all-bridges-block | 
bridge-block | bridge-rsvd-0B0F | bridge-rsvd-0C0D | garp-block | gmrp | gvrp | lacp | lacpmarker | lldp | oam>  
{{cft_disposition}} can be <discard | forward | egress-l2pttranslate>  
l2-cft enable port {{vsi_ni_if_name}} is a conversion of {{cft_enabled}} set to true  
l2-cft disable port {{vsi_ni_if_name}} is a conversion of {{cft_enabled}} set to false

##### Unit

