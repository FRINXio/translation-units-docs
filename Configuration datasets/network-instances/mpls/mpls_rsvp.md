# Multiprotocol Label Switching - Resource Reservation Protocol (MPLS RSVP)

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance/default/mpls/signaling-protocols/rsvp-te/interface-attributes/interface/{{rsvp_intf_id}}
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

#### CLI

<pre>
rsvp
 interface {{rsvp_intf_id}}
  bandwidth {{rsvp_bandwidth}}
</pre>

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/mpls)

### Junos 17.3R1.10

#### CLI

<pre>
set protocols rsvp interface {{rsvp_intf_id}} bandwidth {{rsvp_bandwidth}}
</pre>

##### Unit

NOT IMPLEMENTED

Link to github : [junos-unit]()
