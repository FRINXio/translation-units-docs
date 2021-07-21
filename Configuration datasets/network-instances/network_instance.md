# Configure network instance (VRF)

## URL

```
ios-essential:vrfs/vrf={{l3_vpn_bgp_vrf}}
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


# Configure default network instance

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance=default
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/network-instance/src/main/yang)

```javascript
{
    "frinx-openconfig-network-instance:network-instance": [
        {
            "name": "default",
            "vlans": "{{vlans}}",
            "frinx-cisco-ipvsix-extension:cisco-ipv6-config": {
                "unicast-routing-enabled": "{{unicast-routing}}",
                "cef-enabled": "{{cef}}"
            },
            "policy-forwarding": "{{policy-forwarding}}",
            "protocols": "{{protocols}}",
            "config": {
                "name": "default",
                "type": "frinx-openconfig-network-instance-types:DEFAULT_INSTANCE"
            },
            "interfaces": {
                "interface": [
                    {
                        "id": "{{interface-name}}"
                    }
                ]
            }
        }
    ]
}
```

*vlans* definition - [vlans](https://github.com/FRINXio/translation-units-docs/blob/master/Configuration%20datasets/network-instances/vlans/vlan.md)  
*policy-forwarding* definition - [policy-forwarding](https://github.com/FRINXio/translation-units-docs/blob/master/Configuration%20datasets/network-instances/policy-forwarding/pf_interfaces.md)  
*protocols* definition - [protocols](https://github.com/FRINXio/translation-units-docs/tree/master/Configuration%20datasets/network-instances/protocols)  
*interface-name* is a conversion of each interface name for this network-instance  
*cisco-ipv6-config* is a conversion of global ipv6 configuration for device and consist of:  
    *unicast-routing* and *cef* whose values can only be true or false 


## OS Commands

### Cisco IOS Classic (15.2(4)S5)

#### CLI

---
<pre>
ipv6 unicast-routing
ipv6 cef
</pre>
---
