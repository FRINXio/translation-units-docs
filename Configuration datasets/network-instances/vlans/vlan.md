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
        "frinx-dasan-vlan-extension:eline" : false
    }
  }
}
```

## OS Configuration Commands
### Dasan NOS SFU.RR.5.6p5
#### CLI
if eline is enable
<pre>
bridge
 vlan create {{vlan_id}} eline
!
</pre>

if eline is disable
<pre>
bridge
 vlan create {{vlan_id}}
!
</pre>

result of `show running-config bridge`
<pre>
bridge
 vlan create 10,20-29,30 eline
 vlan create 101,201-209,300
!
</pre>
