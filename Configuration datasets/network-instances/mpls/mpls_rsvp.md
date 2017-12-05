# Multiprotocol Label Switching - Resource Reservation Protocol (MPLS RSVP)

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance/<ni-name>/mpls/signaling-protocols/rsvp-te/interface-attributes/interface/<intf-id>
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/mpls/src/main/yang)

[extensions to MPLS YANG model](https://github.com/FRINXio/openconfig/tree/master/network-instance/src/main/yang)

```javascript
{
    "interface": [
         {
             "interface-id": "<intf-id>",
             "config": {
                 "interface-id": "<intf-id>"
             },
             "subscription": {
                "config": {
                    "frinx-mpls-rsvp-extension:bandwidth": <bandwidth>
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
 interface &lt;intf-id&gt;
  bandwidth &lt;bandwidth&gt;
</pre>

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [xr-unit]()

### Junos 15.1F-6.9

#### CLI

<pre>
set protocols rsvp interface &lt;intf-id&gt; bandwidth &lt;bandwidth&gt;
</pre>

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit]()

