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
                "cisco-extension:statistics" {
                    "load-interval" : <load-interval>
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

```
augment "/oc-if:interfaces/oc-if:interface/oc-if:config" {

    description "Adds CISCO proprietary property of load-interval";

    container statistics {
        description "Per-interface statistics configuration";
        leaf load-interval {
        type uint32 {
            range "0..600";
        }
        default "300";
        description
            "Specify interval for load calculation for an
            interface";
        }
    }
}
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

Unit version range: NOT IMPLEMENTED

Link to github : [xr-unit][]

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

Link to github : [junos-unit][]
