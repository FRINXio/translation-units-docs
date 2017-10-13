# Common interface configuration

## URL

```
openconfig-interfaces:interfaces/interface/<intf-id>
```

## OPENCONFIG YANG

```javascript
{
    "interface": [
        {
            "config": {
                "type": "iana-if-type:softwareLoopback"
                "enabled": true
                "mtu": <mtu>
                "description": <desc>
                "name": <intf-id>
            }
            "hold-time": {
                "config": {
                    "up": <up>
                    "down": <down>
                }
            }
        }
    ]
}

// TODO: augment to set load-interval
// TODO: add logging
```

## OS Configuration Commands

### Cisco IOS XR 5.3.4

#### CLI

---
<pre>
interface &lt;intf-id&gt;
 description &lt;desc&gt;
 mtu &lt;mtu&gt;
 ipv4 address &lt;ip&gt; &lt;subnet&gt;
 carrier-delay up &lt;up&gt; down &lt;down&gt;
 load-interval &lt;load-interval&gt;
 logging &lt;events&gt; &lt;link-status&gt;
 no shutdown
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [xr-unit][]

### Junos 15.1F5

#### CLI

---
<pre>
set interfaces &lt;intf-id&gt;
set interfaces &lt;intf-id&gt; description &lt;desc&gt;
set interfaces &lt;intf-id&gt; mtu &lt;mtu&gt;
set interfaces &lt;intf-id&gt; unit 0 family inet address &lt;prefix&gt;
set interfaces &lt;intf-id&gt; hold-time up &lt;up&gt; down &lt;down&gt;
set event-options policy log-on-snmp-trap-link-up events snmp_trap_link_up
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit][]
