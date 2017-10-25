# Common interface configuration

## URL

```
openconfig-interfaces:interfaces/interface/<intf-id>
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/interfaces/src/main/yang)

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
                "cisco-if-extension:statistics": {
                    "load-interval": <load-interval>
                }
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

// TODO: add logging
```

## OS Configuration Commands

### Cisco IOS Classic (15.2(4)S5) / XE (15.3(3)S2)

---
<pre>
configure terminal
interface &lt;intf-id&gt;
description &lt;descr&gt;
mtu &lt;mtu&gt;
shutdown
exit
exit
</pre>
---

##### Unit

Unit version range: 3.1.1.rc1-frinx

Link to github : [ios-unit](https://github.com/FRINXio/cli-units/tree/master/ios/interface)

### Cisco IOS XR 5.3.4

#### CLI

---
<pre>
interface &lt;intf-id&gt;
 description &lt;desc&gt;
 mtu &lt;mtu&gt;
 carrier-delay up &lt;up&gt; down &lt;down&gt;
 load-interval &lt;load-interval&gt;
 logging &lt;events&gt; &lt;link-status&gt;
 no shutdown
</pre>
---

##### Unit

Unit version range: 3.1.1.rc1-frinx

Link to github : [xr-unit](https://github.com/FRINXio/unitopo-units/tree/master/xr-6-interface-unit)

### Junos 15.1F5

#### CLI

---
<pre>
set interfaces &lt;intf-id&gt;
set interfaces &lt;intf-id&gt; description &lt;desc&gt;
set interfaces &lt;intf-id&gt; mtu &lt;mtu&gt;
set interfaces &lt;intf-id&gt; hold-time up &lt;up&gt; down &lt;down&gt;
set event-options policy log-on-snmp-trap-link-up events snmp_trap_link_up
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit]()
