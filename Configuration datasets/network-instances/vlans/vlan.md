# VLAN

## URL
```
frinx-openconfig-network-instance:network-instances/network-instance/default/vlans/vlan/{{vlan_id}}
```

## OPENCONFIG YANG
[YANG models](https://github.com/FRINXio/openconfig/tree/master/network-instance/src/main/yang)

```javascript
{
  "vlan" : {
    "vlan-id" : {{vlan_id}},
    "config" : {
        "vlan-id" : {{vlan_id}},
        "name" : {{vlan_name}},
        "frinx-dasan-vlan-extension:eline" : {{eline_enabled}},
        "frinx-ciena-vlan-extension:egress-tpid": "{{vlan_tpid}}"
    }
  }
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

## Ciena 3916/3930
####
<pre>vlan create vlan {{vlan_id}} name {{vlan_name}}
vlan set vlan {{vlan_id}} egress-tpid {{vlan_tpid_e}}</pre>

{{vlan_tpid}} should be pure numberic, converted from oc-vlan-types:TPID_TYPES from openconfig
