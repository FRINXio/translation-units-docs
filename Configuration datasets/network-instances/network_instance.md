# Configure network instance (VRF)

## URL

```
ios-essential:vrfs/vrf/{{l3_vpn_bgp_vrf}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/network-instance/src/main/yang)

```javascript
{
    "vrf": {
        "id": {{l3_vpn_bgp_vrf}}
	"description": {{l3_vpn_bgp_vrf_desc}}
    }
}
```

## OS Commands

### Cisco IOS Classic (15.2(4)S5) / XE (15.3(3)S2)

#### CLI

---
<pre>
ip {{l3_vpn_bgp_vrf}}
description {{l3_vpn_bgp_vrf_desc}}
</pre>
---

##### Unit

Link to github : [ios-unit](https://github.com/FRINXio/cli-units/tree/master/ios/essential)
