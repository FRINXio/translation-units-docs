# Border Gateway Protocol (BGP)

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance/default/protocols/protocol/frinx-openconfig-policy-types:BGP/{{bgp_process_name}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/bgp/src/main/yang)

```javascript
{
    "protocol": [
        {
            "name": "{{bgp_process_name}}",
            "identifier": "frinx-openconfig-policy-types:BGP",
            "config": {
                "name": "{{bgp_process_name}}",
                "identifier": "frinx-openconfig-policy-types:BGP"
            },
                        
            "local-aggregates": {
                "aggregate": [
                    {
                        "config": {
                            "prefix": "{{network_prefix}}",
                            "frinx-cisco-bgp-extension:apply-policy": "{{network_prefix_rpl}}"
                        }
                    }
                ]
            },
            
            "bgp": {
                "global": {
                   "afi-safis": {
                       "afi-safi": [
                           {
                               "afi-safi-name": "{{bgp_afi_safi_name}}",
                               "config": {
                                   "afi-safi-name": "{{bgp_afi_safi_name}}"
                               }
                           }
                       ]
                   },
                   "config": {
                       "as": {{bgp_as}}
                   }
                },
                "neighbors|peer-groups": {
                    "neighbor|peer-group": [
                        {
                            "neighbor-address": "{{neighbor_ip}}", //only for neighbor
                            "peer-group-name": "{{peer-group-name}}", //only for peer-group
                            "config": {
                                "neighbor-address": "{{neighbor_ip}}", //only for neighbor
                                "peer-group-name": "{{peer-group-name}}", //only for peer-group
                                "peer-group": "{{bgp_group}}", //only for neighbor
                                "peer-as": {{bgp_peer_as}},
                                "auth-password": "{{bgp_nbr_password}}",
                                "description": "{{bgp_nbr_description}}",
                                "send-community": "{{bgp_nbr_sendcommunity}}",
                                "remove-private-as": ""{{bgp_nbr_removepas}},
                                "enabled": {{neighbor_enabled}}
                            }
                            "transport": {
                                "config": {
                                    "local-address": "{{bgp_nbr_updatesource}}",
                                    "passive-mode": "{{bgp_nbr_passivemode}}"
                                }
                            }
                            "route-reflector": {
                                "config": {
                                    "route-reflector-client": "{{bgp_nbr_rrclient}}"
                                }
                            }
                            "ebgp-multihop": {
                                "config": {
                                    "enabled": "{{bgp_nbr_multihop}}",
                                    "multihop-ttl": "{{bgp_nbr_multihop_ttl}}"
                                }
                            }
                            "afi-safis": {
                                "afi-safi": [
                                    "config": {
                                        "frinx-cisco-bgp-extension:soft-reconfiguration": {
                                            "always": true|false
                                        },
                                        "afi-safi-name": "{{bgp_nbr_afi_safi_name}}"
                                    }
                                    "apply-policy": {
                                        "config": {
                                            "import-policy": "{{bgp_rpol_import}}",
                                            "export-policy": "{{bgp_rpol_export}}"
                                        }
                                    }
                                     "ipv4|ipv6|vpnv4-unicast|l2vpn-evpn": {
                                        "config": {
                                            "send-default-route" "{{bgp_nbr_defaultoriginate}}"
                                        }
                                        "prefix-limit": {
                                            "config": {
                                                "max-prefixes": "{{bgp_nbr_maxprefixes}}",
                                                "shutdown-threshold-pct": "{{bgp_nbr_maxprefixes_pct}}"
                                            }
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
```


## OS Configuration Commands

### Cisco IOS XR 5.3.4

#### CLI

---
<pre>
router bgp {{bgp_as}} instance {{bgp_process_name}}
 
 address-family {{bgp_afi_safi_name}}
  network {{network_prefix}} route-policy {{network_prefix_rpl}}

 neighbor {{neighbor_ip}}
  remote-as {{bgp_peer_as}}
  use neighbor-group {{bgp_group}}
  password clear {{bgp_nbr_password}}
  description {{bgp_nbr_description}}
  update-source {{bgp_nbr_updatesource}}
  ebgp-multihop {{bgp_nbr_multihop_ttl}}
  no shutdown | shutdown

  address-family {{bgp_nbr_afi_safi_name}}
   route-policy {{bgp_rpol_import}}|{{bgp_rpol_export}} in|out
   maximum-prefix {{bgp_nbr_maxprefixes}} {{bgp_nbr_maxprefixes_pct}}
   send-community-ebgp {{bgp_nbr_sendcommunity}}
   remove-private-AS
   next-hop-self
   default-originte
   soft-reconfiguration inbound always
</pre>
---

*ipv4 unicast* is a conversion of {{bgp_afi_safi_name}} set *IPV4_UNICAST*  
*ipv6 unicast* is a conversion of {{bgp_afi_safi_name}} set *IPV6_UNICAST*  
*remove-private-AS* is a conversion of {{bgp_nbr_removepas}}  
*default-originte* is a conversion of {{bgp_nbr_defaultoriginate}}  
*next-hop-self* is a conversion of {{bgp_rpol_export}} if value is "nexthopself"  
*no shutdown* is a conversion of {{neighbor_enabled}} set *true*  
*shutdown* is a conversion of {{neighbor_enabled}} set *false*  
*ipv4 unicast* is a conversion of {{bgp_nbr_afi_safi_name}} set *IPV4_UNICAST*  
*ipv6 unicast* is a conversion of {{bgp_nbr_afi_safi_name}} set *IPV6_UNICAST*  
*vpnv4 unicast* is a conversion of {{bgp_nbr_afi_safi_name}} set *L3VPN_IPV4_UNICAST*  

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/bgp)

### Cisco IOS XR 7.0.1

#### CLI

---
<pre>
router bgp {{bgp_as}} instance {{bgp_process_name}}
 
 address-family {{bgp_afi_safi_name}}

 neighbor {{neighbor_ip}}
  remote-as {{bgp_peer_as}}
  password clear {{bgp_nbr_password}}
  description {{bgp_nbr_description}}
  update-source {{bgp_nbr_updatesource}}
  address-family {{bgp_nbr_afi_safi_name}}
</pre>
---

*l2vpn evpn* is a conversion of {{bgp_afi_safi_name}} set *L2VPN_EVPN*  
*remove-private-AS* is a conversion of {{bgp_nbr_removepas}}  
*default-originte* is a conversion of {{bgp_nbr_defaultoriginate}}  
*next-hop-self* is a conversion of {{bgp_rpol_export}} if value is "nexthopself"  
*no shutdown* is a conversion of {{neighbor_enabled}} set *true*  
*shutdown* is a conversion of {{neighbor_enabled}} set *false*  
*l2vpn evpn* is a conversion of {{bgp_nbr_afi_safi_name}} set *L2VPN_EVPN*  

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/unitopo-units/tree/master/xr/xr-7-bgp-unit

### Cisco IOS XE 03.13.01.S

---
<pre>
router bgp {{bgp_as}}
 neighbor {{peer-group-name}} peer-group
 neighbor {{neighbor_ip}} peer-group {{bgp_group}}
 neighbor {{neighbor_ip}}|{{peer-group-name}} remote-as {{bgp_peer_as}}
 neighbor {{neighbor_ip}}|{{peer-group-name}} transport connection-mode passive
 neighbor {{neighbor_ip}}|{{peer-group-name}} password {{bgp_nbr_password}}
 neighbor {{neighbor_ip}}|{{peer-group-name}} update-source {{bgp_nbr_updatesource}}
 neighbor {{neighbor_ip}}|{{peer-group-name}} description {{bgp_nbr_description}}
 address-family {{bgp_nbr_afi_safi_name}}
  neighbor {{neighbor_ip}}|{{peer-group-name}} send-community {{bgp_nbr_sendcommunity}}
  neighbor {{neighbor_ip}}|{{peer-group-name}} route-reflector-client
  neighbor {{neighbor_ip}}|{{peer-group-name}} route-map {{bgp_rpol_import}}|{{bgp_rpol_export}} in|out
  neighbor {{neighbor_ip}} activate
</pre>
---

*transport connection-mode passive* is a conversion of {{bgp_nbr_passivemode}} set *true*  
*route-reflector-client* is a conversion of {{bgp_nbr_rrclient}} set *true*  

### Junos 17.3R1.10

#### CLI

---
<pre>
set routing-options autonomous-system {{bgp_as}}
activate protocols bgp group {{bgp_group}} neighbor {{neighbor_ip}} peer-as {{bgp_peer_as}}
</pre>
---

*activate* is a conversion of {{neighbor_enabled}} set *true*  
*deactivate* is a conversion of {{neighbor_enabled}} set *false*  

##### Unit

Link to github : [junos-unit](https://github.com/FRINXio/unitopo-units/tree/master/junos/junos-17/junos-17-bgp-unit)
