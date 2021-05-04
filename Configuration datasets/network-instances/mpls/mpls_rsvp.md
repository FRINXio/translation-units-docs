# Multiprotocol Label Switching - Resource Reservation Protocol (MPLS RSVP)

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance=default/mpls/signaling-protocols/rsvp-te/interface-attributes/interface={{rsvp_intf_id}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/mpls/src/main/yang)

[extensions to MPLS YANG model](https://github.com/FRINXio/openconfig/tree/master/network-instance/src/main/yang)

```javascript
{
    "interface": [
         {
             "interface-id": "{{rsvp_intf_id}}",
             "config": {
                 "interface-id": "{{rsvp_intf_id}}"
             },
             "subscription": {
                "config": {
                    "frinx-mpls-rsvp-extension:bandwidth": {{rsvp_bandwidth}}
                }
             }
         }
    ]
}
```

## OS Configuration Commands

### Cisco IOS XR 5.3.4
{{rsvp_bandwidth}} 
- setting to _default_ results in 'bandwidth' meaning setting default device bandwidth
- setting to numeric value results in 'bandwith &lt;number&gt;  
- transformation: input bandwith in bps, in XR router as Kbps

#### CLI

<pre>
rsvp
 interface {{rsvp_intf_id}}
  bandwidth {{rsvp_bandwidth}}
</pre>

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/mpls)

### Junos 17.3R1.10
{{rsvp_bandwidth}} 
- transformation: k,m,g from JUNOS router translates to thousand, million, billion

#### CLI

<pre>
set protocols rsvp interface {{rsvp_intf_id}} bandwidth {{rsvp_bandwidth}}
</pre>

##### Unit

Link to github : [junos-unit](https://github.com/FRINXio/unitopo-units/tree/master/junos/junos-17/junos-17-mpls-unit)
