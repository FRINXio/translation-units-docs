# Ethernet Virtual Private Network (EVPN)

## URL

```
frinx-evpn:evpn
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/evpn/src/main/yang)

```javascript
{
    "group": [
        {
            "config": {
                "id": {{evpn_group_id}}
            },
            "core-interfaces": {
                "interface": [
                    {
                        "name": "{{evpn_core_if_name}}",
                        "config": {
                            "type": "{{evpn_core_if_type}}",
                            "name": "{{evpn_core_if_name}}"
                        }
                    }
                ]
            }
        }
    ],

    "interfaces": {
        "interface": [
            "name": "{{evpn_if_name}}",
            "config": {
                "type": "{{evpn_if_type}}",
                "name": "{{evpn_if_name}}"
            },
            "ethernet-segment": {
                "config": {
                    "identifier": "{{ethernet_segment_id}}",
                    "load-balancing-mode": "{{ethernet_segment_lb_mode}}",
                    "bgp-route-target": "{{bgp_route_target}}"
                }
            },
            "core-isolation-group": {{evpn_isolation_group_id}}
        ]
    }
}
```

## OS Configuration Commands

### Cisco IOS XR 7.0.1

#### CLI

<pre>
evpn
 group {{evpn_group_id}}
  core interface Bundle-Ether {{evpn_core_if_id}}
 interface Bundle-Ether {{evpn_if_id}}
  ethernet-segment
   identifier type 0 {{ethernet_segment_id}}
   load-balancing-mode {{ethernet_segment_lb_mode}}
   bgp route-target {{bgp_route_target}}
  core-isolation-group {{evpn_isolation_group_id}}
</pre>

{{evpn_core_if_id}} is parsed from {{evpn_core_if_name}}  
example {{evpn_core_if_name}} is Bundle-Ether100 -> {{evpn_core_if_id}} is 100  
{{evpn_if_id}} is parsed from {{evpn_if_name}}  
*Bundle-Ether* is a conversion of {{evpn_core_if_type}} set to "iana-if-type:ieee8023adLag"  
*mode port-active* is a conversion of {{ethernet_segment_lb_mode}} set to "frinx-es-lb-mode:PORT-ACTIVE"  
*mode single-active* is a conversion of {{ethernet_segment_lb_mode}} set to "frinx-es-lb-mode:SINGLE-ACTIVE"  

#### Unit

Link to github : [xr-unit](https://github.com/FRINXio/unitopo-units/tree/master/xr/xr-7-evpn)

