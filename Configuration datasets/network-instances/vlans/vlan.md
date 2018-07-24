# VLAN

## URL
```
frinx-openconfig-network-instance:network-instance/network-instance/default/vlans/vlan/{{vlan_id}}
```

## OPENCONFIG YANG
[YANG models](https://github.com/FRINXio/openconfig/tree/master/network-instance/src/main/yang)

```javascript
{
  "vlan" : {
    "vlan-id" : {{vlan_id}},
    "config" : {
        "vlan-id" : {{vlan_id}},
        "frinx-dasan-vlan-extension:eline" : {{eline_enabled}}
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
