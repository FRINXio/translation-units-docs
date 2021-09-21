# Border Gateway Protocol (BGP)

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance=default/protocols/protocol=frinx-openconfig-policy-types%3ABGP,{{bgp_process_name}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/bgp/src/main/yang)

```javascript
{
    "protocol": [
        {
            "identifier": "frinx-openconfig-policy-types:BGP",
            "name": "{{bgp_process_name}}",
            "config": {
                "identifier": "frinx-openconfig-policy-types:BGP",
                "name": "{{bgp_process_name}}"
            },
                        
            "local-aggregates": {
                "aggregate": [
                    {
                        "config": {
                            "prefix": "{{network_prefix}}",
                            "frinx-bgp-extension:apply-policy": [
                                "{{network_prefix_rpl}}"
                            ]
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
                                   "afi-safi-name": "{{bgp_afi_safi_name}}",
                                   "frinx-bgp-extension:auto-summary": "{{auto_summary}}",
                                   "frinx-bgp-extension:redistribute-connected": {
                                       "enabled": "{{redistribute_connected_enabled}}",
                                       "route-map": "{{redistribute_connected_route_map}}"
                                   },
                                   "frinx-bgp-extension:redistribute-static": {
                                       "enabled": "{{redistribute_static_enabled}}",
                                       "route-map": "{{redistribute_static_route_map}}"
                                   },
                                   "frinx-bgp-extension:synchronization": "{{synchronization}}",
                                   "frinx-bgp-extension:default-information-originate": "{{default_information_originate}}",
                                   "frinx-bgp-extension:table-map": "{{table-map}}"
                               }
                           }
                       ]
                   },
                   "config": {
                       "frinx-bgp-extension:log-neighbor-changes": "{{log_neighbor_changes}}",
                       "as": "{{bgp_as}}",
                       "router-id": "{{router_id}}",
                       "frinx-bgp-extension:import-route": [
                           "{{import_route}}"
                       ]
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
                                "peer-as": "{{bgp_peer_as}}",
                                "auth-password": "{{bgp_nbr_password}}",
                                "description": "{{bgp_nbr_description}}",
                                "send-community": "{{bgp_nbr_sendcommunity}}",
                                "remove-private-as": "{{bgp_nbr_removepas}}",
                                "enabled": "{{neighbor_enabled}}",
                                "frinx-bgp-extension:neighbor-version": "{{bgp_version}}",
                                "frinx-bgp-extension:fall-over-mode": "{{fall_over_mode}}",
                                "frinx-bgp-extension:as-override": "{{as_override}}",
                                "frinx-bgp-extension:timer-configuration": {
                                    "timer-mode": "{{timer_mode}}",
                                    "time-before": "{{time_before}}",
                                    "time-after": "{{time_after}}"
                                },
                                "frinx-bgp-extension:transport": "{{bgp_transport}}",
                                "local-as": "{{local_as}}",
                                "frinx-bgp-extension:local-as-group": {
                                    "no-prepend": "{{local_as_no_prepend}}",
                                    "replace-as": "{{local_as_replace_as}}"
                                }
                            },
                            "transport": {
                                "config": {
                                    "local-address": "{{bgp_nbr_updatesource}}",
                                    "passive-mode": "{{bgp_nbr_passivemode}}"
                                }
                            },
                            "route-reflector": {
                                "config": {
                                    "route-reflector-client": "{{bgp_nbr_rrclient}}"
                                }
                            },
                            "ebgp-multihop": {
                                "config": {
                                    "enabled": "{{bgp_nbr_multihop}}",
                                    "multihop-ttl": "{{bgp_nbr_multihop_ttl}}"
                                }
                            },
                            "afi-safis": {
                                "afi-safi": [
                                    {
                                        "afi-safi-name": "{{bgp_nbr_afi_safi_name}}",
                                        "config": {
                                            "frinx-bgp-extension:soft-reconfiguration": {
                                                "always": true|false
                                            },
                                            "afi-safi-name": "{{bgp_nbr_afi_safi_name}}"
                                        },
                                        "apply-policy": {
                                            "config": {
                                                "import-policy": "{{bgp_rpol_import}}",
                                                "export-policy": "{{bgp_rpol_export}}"
                                            }
                                        },
                                        "ipv4|ipv6|vpnv4-unicast|l2vpn-evpn": {
                                            "config": {
                                                "send-default-route": "{{bgp_nbr_defaultoriginate}}",
                                                "frinx-bgp-extension:send-default-route-route-policy": "{{bgp_nbr_defaultoriginate_rpol}}"
                                            },
                                            "prefix-limit": {
                                                "config": {
                                                    "max-prefixes": "{{bgp_nbr_maxprefixes}}",
                                                    "shutdown-threshold-pct": "{{bgp_nbr_maxprefixes_pct}}"
                                                }
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

### Cisco IOS XR 6.6.1 (via NetConf)

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

Link to github : [xr-unit](https://github.com/FRINXio/unitopo-units/tree/master/xr/xr-6.6/xr-6.6-bgp-unit)

### Cisco IOS XR 6.6.1 (no NetConf)

#### CLI

---
<pre>
router bgp {{bgp_as}}
 
 neighbor-group {{peer-group-name}}
  address-family {{bgp_nbr_afi_safi_name}}
   route-policy {{bgp_rpol_import}}|{{bgp_rpol_export}} in|out
</pre>
---

*vpnv4 unicast* is a conversion of {{bgp_nbr_afi_safi_name}} set *L3VPN_IPV4_UNICAST*

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/bgp)

### Cisco IOS XR 6.6.2

#### CLI

---
<pre>
router bgp {{bgp_as}} instance {{bgp_process_name}}
 
 address-family {{bgp_afi_safi_name}}
  network {{network_prefix}}

 neighbor {{neighbor_ip}}
  remote-as {{bgp_peer_as}}
  password clear {{bgp_nbr_password}}
  description {{bgp_nbr_description}}

  address-family {{bgp_nbr_afi_safi_name}}
   route-policy {{bgp_rpol_import}}|{{bgp_rpol_export}} in|out
   maximum-prefix {{bgp_nbr_maxprefixes}} {{bgp_nbr_maxprefixes_pct}}
   send-community-ebgp {{bgp_nbr_sendcommunity}}
   remove-private-AS
   default-originte route-policy {{bgp_nbr_defaultoriginate_rpol}}
   soft-reconfiguration inbound always
</pre>
---

*ipv4 unicast* is a conversion of {{bgp_afi_safi_name}} set *IPV4_UNICAST*  
*ipv6 unicast* is a conversion of {{bgp_afi_safi_name}} set *IPV6_UNICAST*  
*remove-private-AS* is a conversion of {{bgp_nbr_removepas}}  
*default-originte* is a conversion of {{bgp_nbr_defaultoriginate}}  
*ipv4 unicast* is a conversion of {{bgp_nbr_afi_safi_name}} set *IPV4_UNICAST*  
*ipv6 unicast* is a conversion of {{bgp_nbr_afi_safi_name}} set *IPV6_UNICAST*

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/bgp)

### Cisco IOS XE 03.13.01.S

---
<pre>
router bgp {{bgp_as}}
 bgp log-neighbor-changes|no bgp log-neighbor-changes
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
  neighbor {{neighbor_ip}} version {{bgp_version}}
  neighbor {{neighbor_ip}} as-override
  neighbor {{neighbor_ip}} fall-over bfd
  neighbor {{neighbor_ip}} activate
  neighbor {{neighbor_ip}} remove-private-as
  neighbor {{neighbor_ip}} local-as {{local_as}} {{local_as_no_prepend}} {{local_as_replace_as}}
  auto-summary|no auto-summary
  redistribute connected route-map {{redistribute_connected_route_map}}|no redistribute connected
  redistribute static route-map {{redistribute_static_route_map}}|no redistribute static
  default-information originate|no default-information originate
  synchronization|no synchronization
  table-map {{table-map}} filter
</pre>
---

*bgp log-neighbor-changes* is a conversion of {{log_neighbor_changes}} set *true*  
*no bgp log-neighbor-changes* is a conversion of {{log_neighbor_changes}} set *false*
*default-information originate* is a conversion of {{default_information_originate}} set *true*  
*no default-information originate* is a conversion of {{default_information_originate}} set *false*
*neighbor {{neighbor_ip}} as-override* is a conversion of {{as_override}} set *true*
*neighbor {{neighbor_ip}} fall-over bfd* is a conversion of {{fall_over_mode}} set *true*
*transport connection-mode passive* is a conversion of {{bgp_nbr_passivemode}} set *true*  
*route-reflector-client* is a conversion of {{bgp_nbr_rrclient}} set *true*  
*remove-private-as* is a conversion of {{bgp_nbr_removepas}} set "frinx-openconfig-bgp-types:PRIVATE_AS_REMOVE_ALL"
*no-prepend* is a conversion of {{local_as_no_prepend}} set *true*  
*replace-as* is a conversion of {{local_as_replace_as}} set *true*  
*neighbor {{neighbor_ip}} version 4* is a conversion of {{bgp_version}} set "frinx-bgp-extension:VERSION_4"
*auto-summary* is a conversion of {{auto_summary}} set *true*  
*no auto-summary* is a conversion of {{auto_summary}} set *false*
*redistribute connected route-map {{redistribute_connected_route_map}}* is a conversion of {{redistribute_connected_enabled}} set *true*  
*no redistribute connected* is a conversion of {{redistribute_connected_enabled}} set *false*
*redistribute static route-map {{redistribute_static_route_map}}* is a conversion of {{redistribute_static_enabled}} set *true*  
*no redistribute static* is a conversion of {{redistribute_static_enabled}} set *false*
*synchronization* is a conversion of {{synchronization}} set *true*  
*no synchronization* is a conversion of {{synchronization}} set *false*

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
  

### Huawei NE5000E (V800R009C10SPC310)

#### CLI  

---
<pre> 
bgp {{bgp_as}}                                 
 router-id {{router_id}}                   
 peer {{neighbor_ip}} as-number {{bgp_peer_as}}            
 peer {{neighbor_ip}} description {{bgp_nbr_description}}      
 peer {{neighbor_ip}} password cipher {{bgp_nbr_password}}
 peer {{neighbor_ip}} path-mtu {{bgp_transport}}
 peer {{neighbor_ip}} timer {{timer_mode}} {{time_before}} hold {{time_after}}
                                       
 ipv4-family unicast                       
  import-route {{import_route}}
  peer {{neighbor_ip}} enable                   
  peer {{neighbor_ip}} route-policy {{bgp_rpol_import}} import
  peer {{neighbor_ip}} route-policy {{bgp_rpol_export}} export
</pre>
---

*auto-discovery* is conversion of {{bgp_transport}} set "frinx-bgp-extension:transport"  
*keepalive* is conversion of {{timer_mode}} set "timer_mode"  
*0-21845* is conversion of {{time_before}} set "time_before"  
*3-65535* is conversion of {{timer_after}} set "timer_after"  
*direct, static* is conversions of {{import_route}} set "import_route"

##### Unit

Link to github : [huawei-unit](https://github.com/FRINXio/cli-units/tree/master/huawei/bgp)
