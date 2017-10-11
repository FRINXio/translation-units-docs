# RSVP bandwidth configuration

## URL

```
openconfig-network-instance:network-instances/network-instance/<ni-name>/openconfig-mpls:mpls/signaling-protocols/rsvp-te/interface-attributes/interface/<intf-id>
```

## OPENCONFIG YANG

```json
{
    "interface": [
        {
            "config": {
                "interface-id": <intf-id>
            }
            "bandwidth-reservations": {
                 "bandwidth-reservation": [
                     {
                        "reserved-bandwidth": <bandwidth>
                     }
                 ]
            }
        }
    ]
}


TODO: bandwidth is not configurable @see https://github.com/openconfig/public/blob/master/release/models/mpls/openconfig-mpls-rsvp.yang
```

## OS Configuration Commands

#### Cisco IOS XR 5.4.3

---
<pre>
rsvp
 interface &lt;intf-id&gt;
  bandwidth &lt;bandwidth&gt;
</pre>
---

#### Junos

---
<pre>
set protocols rsvp interface &lt;intf-id&gt; bandwidth &lt;bandwidth&gt;
</pre>
---
