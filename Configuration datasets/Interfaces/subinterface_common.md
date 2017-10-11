# Subinterface common configuration

## URL

```
openconfig-interfaces:interfaces/interface/<intf-id>/subinterfaces/subinterface/0
```

## OPENCONFIG YANG

```json
{
    "subinterface": [
        {
            "index": 0
            "config": {
                "index": 0
            }
            "ipv4": {
                "addresses": {
                    "address": {
                        "ip":
                        "config": {
                            "ip": <ip>
                            "prefix-length": <prefix>
                        }
                    }
                }
            }
        }
    ]
}

TODO: in unit implementation convert prefix to subnet for XR
```

## OS Configuration Commands

#### Cisco IOS XR 5.4.3

---
<pre>
interface &lt;intf-id&gt;
 ipv4 address &lt;ip&gt; &lt;subnet&gt;
</pre>
---

#### Junos

---
<pre>
set interfaces &lt;intf-id&gt;
set interfaces &lt;intf-id&gt; unit 0 family inet address &lt;ip&gt/&lt;prefix&gt;;
</pre>
---
