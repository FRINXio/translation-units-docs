# Subinterface common configuration

## URL

```
openconfig-interfaces:interfaces/interface/<intf-id>/subinterfaces/subinterface/0
```

## OPENCONFIG YANG

```javascript
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

### Cisco IOS XR 5.3.4

#### CLI

---
<pre>
interface &lt;intf-id&gt;
 ipv4 address &lt;ip&gt; &lt;subnet&gt;
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
set interfaces &lt;intf-id&gt; unit 0 family inet address &lt;ip&gt/&lt;prefix&gt;;
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit][]
