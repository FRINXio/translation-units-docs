# VLAN

## URL
```
frinx-openconfig-network-instance:network-instances/network-instance/default/vlans/vlan/{{vlan_id}}
```

## OPENCONFIG YANG
[YANG models](https://github.com/FRINXio/openconfig/tree/master/network-instance/src/main/yang)

```javascript
{
    "vlan": [
        {
            "vlan-id": {{vlan_id}},
            "config": {
                "vlan-id": {{vlan_id}},
                "frinx-dasan-vlan-extension:eline": {{eline_enabled}},
                "frinx-saos-vlan-extension:egress-tpid": "{{vlan_tpid}}"
            },
            "frinx-saos-virtual-ring-extension:rings": {
                "ring": [
                    {
                        "name": "{{ring-name}}",
                        "config": {
                            "name": "{{ring-name}}"
                        }
                    }
                ]
            }
        }
    ]
}
```

## OS Configuration Commands
### Dasan NOS SFU.RR.5.6p5
#### CLI
if {{eline_enabled}} is true
<pre>
bridge
 vlan create {{vlan_id}} eline
!
</pre>

if {{eline_enabled}} is false
<pre>
bridge
 vlan create {{vlan_id}}
!
</pre>

## Ciena SAOS 614
#### CLI
<pre>vlan create vlan {{vlan_id}}
vlan set vlan {{vlan_id}} name {{vlan_name}}
vlan set vlan {{vlan_id}} egress-tpid {{vlan_tpid_e}}
ring-protection virtual-ring add ring {{ring-name}} vid {{vlan-id}}</pre>

{{vlan_tpid}} should be pure numeric, converted from oc-vlan-types:TPID_TYPES from openconfig
