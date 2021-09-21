# L3VPN configuration (BGP as CE-PE protocol)

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance={{l3_vpn_bgp_vrf}}
```

## OPENCONFIG YANG

```javascript
{
    "network-instance": [
        {
            "config": {
                "name": "{{l3_vpn_bgp_vrf}}",
                "type": "L3VRF", //matches vpws-instance-type in ietf
                "route-distinguisher": "{{l3_vpn_bgp_rd}}",
                "frinx-huawei-network-instance-extension:prefix-limit-from": "{{prefix-limit-from}}",
                "frinx-huawei-network-instance-extension:prefix-limit-to": "{{prefix-limit-to}}",
                "enabled-address-families": "{{l3_vpn_bgp_enabled_address_families}}",
                "enabled": true
            },
            
            "interfaces": {
                "interface": [
                    {
                        "config": {
                            "id": "{{l3_vpn_bgp_interface_id}}"
                        }
                    }
                ]
            },
            
            "protocols": {
                "protocol": [
                    {
                        "config": {
                            "identifier": "BGP",
                            "enabled": true
                        },
                        
                        "local-aggregates": {
                            "aggregate": [
                                {
                                    "config": {
                                        "prefix": "{{l3_vpn_bgp_network_prefix}}",
                                        "frinx-bgp-extension:apply-policy": [
                                            "{{network_prefix_rpl}}"
                                        ],
                                        "frinx-bgp-extension:summary-only": true,
                                    }
                                }
                            ]
                        },
                        
                        "bgp": {
                            "global": {
                                "as": "{{l3_vpn_bgp_as_number}}",
                                "router-id": "{{l3_vpn_bgp_router_id}}",
                                "afi-safis": {
                                    "afi-safi": [
                                        "config": {
                                            "afi-safi-name": "ipv4",
                                            "enabled": true
                                        }
                                    ]
                                }
                            },
                            "neighbors": {
                                "neighbor": [
                                    {
                                        "config": {
                                            "neighbor-address": "{{l3_vpn_bgp_neighbor_address}}",
                                            "enabled": true,
                                            "peer-as": "{{l3_vpn_bgp_remote_as}}"
                                        },
                                        "afi-safis": {
                                            "afi-safi": [
                                                "config": {
                                                    "afi-safi-name": "ipv4",
                                                    "enabled": true
                                                },
                                                "apply-policy": {
                                                    "config": {
                                                        "import-policy": "{{l3_vpn_bgp_vrf}}-route-target-import",
                                                        "export-policy": "{{l3_vpn_bgp_vrf}}-route-target-export"
                                                    }
                                                }
                                            ]
                                        }
                                    }
                                ]
                            }
                        }
                    }
                ]
            }
        }
    ]
}
```

```
frinx-openconfig-routing-policy:routing-policy/defined-sets{{l3_vpn_bgp_vrf}}
```

```
{
    "bgp-defined-sets" {
        ext-community-sets {
            ext-community-set [
                {            
                    "config": {
                        "ext-community-set-name": "{{l3_vpn_bgp_vrf}}-route-target-export-set"
                        "ext-community-set-member": [
                            {{l3_vpn_bgp_rt_exp_1}},
                            {{l3_vpn_bgp_rt_exp_2}},
                            {{l3_vpn_bgp_rt_exp_3}}
                        ]
                       }
                }
                {            
                    "config": {
                        "ext-community-set-name": "{{l3_vpn_bgp_vrf}}-route-target-import-set"
                        "ext-community-set-member": [
                            {{l3_vpn_bgp_rt_imp_1}},
                            {{l3_vpn_bgp_rt_imp_2}},
                            {{l3_vpn_bgp_rt_imp_3}}
                        ]
                    }
                }
            ]
        }
    }
}
```
*CONSTRAINTS*  
Network-instance with name {{l3_vpn_bgp_vrf}} must exist before defined-sets or both must be created in the same transaction.  
Delete must be executed in reverse order or in the same transaction.  
Policy {{l3_vpn_bgp_vrf}}-route-target-import and {{l3_vpn_bgp_vrf}}-route-target-export must exist on device before are used in network-instance.

## OS Configuration Commands

### CISCO IOS XR (5.1.3) (6.1.2)

#### CLI

<pre>
vrf {{l3_vpn_bgp_vrf}}
 address-family ipv4 unicast
  import route-target 
   {{l3_vpn_bgp_rt_imp_1}}
   {{l3_vpn_bgp_rt_imp_2}}
   {{l3_vpn_bgp_rt_imp_3}}
  export route-target 
   {{l3_vpn_bgp_rt_exp_1}}
   {{l3_vpn_bgp_rt_exp_2}}
   {{l3_vpn_bgp_rt_exp_3}}

interface {{l3_vpn_bgp_interface_id}}
 vrf {{l3_vpn_bgp_vrf}}
 
router bgp {{l3_vpn_bgp_as_number}}
 vrf {{l3_vpn_bgp_vrf}}
  rd {{l3_vpn_bgp_rd}}
  
  address-family ipv4 unicast
   network {{l3_vpn_bgp_network_prefix}}
   
  neighbor {{l3_vpn_bgp_neighbor_address}}
   remote-as {{l3_vpn_bgp_remote_as}}
   address-family ipv4 unicast
    route-policy {{l3_vpn_bgp_vrf}}-route-target-import in
    route-policy {{l3_vpn_bgp_vrf}}-route-target-export out
</pre>

### CISCO IOS XR (6.6.1)

#### CLI

<pre>
router bgp {{l3_vpn_bgp_as_number}}
 vrf {{l3_vpn_bgp_vrf}}
  address-family ipv4 unicast
   aggregate-address {{l3_vpn_bgp_network_prefix}} summary-only route-policy {{network_prefix_rpl}}
</pre>

*summary-only* is a conversion of "frinx-bgp-extension:summary-only" set *true*

### Cisco IOS (VIOS 15.6(2)T)

#### CLI

<pre>
ip vrf {{l3_vpn_bgp_vrf}}
 rd {{l3_vpn_bgp_rd}}
 route-target export {{l3_vpn_bgp_rt_exp_1}}
 route-target export {{l3_vpn_bgp_rt_exp_2}}
 route-target export {{l3_vpn_bgp_rt_exp_3}}
 route-target import {{l3_vpn_bgp_rt_imp_1}}
 route-target import {{l3_vpn_bgp_rt_imp_2}}
 route-target import {{l3_vpn_bgp_rt_imp_3}}

interface {{l3_vpn_bgp_interface_id}}
 ip vrf forwarding {{l3_vpn_bgp_vrf}}

router bgp {{l3_vpn_bgp_as_number}}
 address-family ipv4 vrf {{l3_vpn_bgp_vrf}}
  network {{l3_vpn_bgp_network_prefix}}
  neighbor {{l3_vpn_bgp_neighbor_address}} remote-as {{l3_vpn_bgp_remote_as}}
  neighbor {{l3_vpn_bgp_neighbor_address}} activate
</pre>

### Junos 18.2R1-S2.1

#### CLI

<pre>
set routing-instances {{l3_vpn_bgp_vrf}} routing-options aggregate route {{l3_vpn_bgp_network_prefix}} policy {{network_prefix_rpl}}
</pre>

### Huawei NE5000E (V800R009C10SPC310)

#### CLI

---
<pre>
ip vpn-instance {{l3_vpn_bgp_vrf}}
 ipv4-family
  route-distinguisher {{l3_vpn_bgp_rd}}
  prefix limit {{prefix-limit-from}} {{prefix-limit-to}} 
  vpn-target {{l3_vpn_bgp_rt_exp_1}} export-extcommunity
  vpn-target {{l3_vpn_bgp_rt_imp_1}} import-extcommunity
  
interface {{l3_vpn_bgp_interface_id}}
 undo shutdown
 ip binding vpn-instance {{l3_vpn_bgp_vrf}}

bgp {{l3_vpn_bgp_as_number}}
 ipv4-family vpn-instance {{l3_vpn_bgp_vrf}}
  network {{l3_vpn_bgp_network_prefix}}
  peer {{l3_vpn_bgp_neighbor_address}} as-number {{l3_vpn_bgp_remote_as}}
  peer {{l3_vpn_bgp_neighbor_address}} route-policy {{l3_vpn_bgp_vrf}}-route-target-import import
  peer {{l3_vpn_bgp_neighbor_address}} route-policy {{l3_vpn_bgp_vrf}}-route-target-export export
</pre>
---

*1 to 100000* is conversion of {{prefix-limit-from}} set "frinx-huawei-network-instance-extension:prefix-limit-from"  
*1 to 100* is conversion of {{prefix-limit-to}} set "frinx-huawei-network-instance-extension:prefix-limit-to"

##### Unit

Link to github : [huawei-unit](https://github.com/FRINXio/cli-units/tree/master/huawei/network-instance/src/main/java/io/frinx/cli/unit/huawei/network/instance/handler/vrf)
