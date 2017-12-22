# Multiprotocol Label Switching - Tunnel

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance/default/mpls/lsps/constrained-path/tunnels/tunnel/{{mpls_tunnel_id}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/mpls/src/main/yang)

[extensions to MPLS YANG model](https://github.com/FRINXio/openconfig/tree/master/network-instance/src/main/yang)

```javascript
{
    "tunnel": [
        {
            "name": "{{mpls_tunnel_id}}",
            "config": {
                "name": "{{mpls_tunnel_id}}",
                "shortcut-eligible": {{mpls_shortcut_eligible}},
                "metric-type": "frinx-openconfig-mpls-types:LSP_METRIC_ABSOLUTE",
                "metric": {{mpls_metric}}
            },
            "frinx-cisco-mpls-te-extension:cisco-mpls-te-extension": {
                "config": {
                    "load-share": {{mpls_load_share}}
                }
            }
        }
    ]
}
```

## OS Configuration Commands

### Cisco IOS XR 5.3.4

#### CLI

<pre>
interface tunnel-te {{mpls_tunnel_id}}
 load-share {{mpls_load_share}}
 autoroute announce | no autoroute announce
 metric absolute {{mpls_metric}}
</pre>

*autoroute announce* is a conversion of {{mpls_shorcut_eligible}} set *true*  
*no autoroute announce* is a conversion of {{mpls_shortcut_eligible}} set *false*  
*load-share* is not supported on virtual platform CISCO IOS-XR

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/mpls)

### Junos 15.1F-6.9

#### CLI

<pre>
set protocols mpls label-switched-path {{mpls_tunnel_id}}
set protocols mpls label-switched-path {{mpls_tunnel_id}} metric {{mpls_metric}}
</pre>

*set protocols mpls label-switched-path {{mpls_tunnel_id}}* is a conversion of {{mpls_shortcut_eligible}} set *true*  

##### Unit

NOT IMPLEMENTED

Link to github : [junos-unit]()
