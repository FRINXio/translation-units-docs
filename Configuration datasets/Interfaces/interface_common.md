# Common interface configuration

## URL

```
openconfig-interfaces:interfaces/interface/<intf-id>
```

## OPENCONFIG YANG

```json
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
        }
    ]
}
```

## OS Configuration Commands

#### Cisco IOS XR 5.4.3

---
<pre>
interface &lt;intf-id&gt;
 description &lt;desc&gt;
 mtu &lt;mtu&gt;
 ipv4 address &lt;ip&gt; &lt;subnet&gt;
 no shutdown
</pre>
---

#### Junos

---
<pre>
set interfaces &lt;intf-id&gt;
set interfaces &lt;intf-id&gt; description &lt;desc&gt;
set interfaces &lt;intf-id&gt; mtu &lt;mtu&gt;
set interfaces &lt;intf-id&gt; unit 0 family inet address &lt;prefix&gt;
</pre>
---
