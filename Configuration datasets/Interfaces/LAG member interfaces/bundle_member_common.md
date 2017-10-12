# configure LAG bundle member

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
                "type": "iana-if-type:ieee8023adLag",
                "enabled": true,
                "name": "<intf-id>"
            }
            "aggregation": {
                "config": {
                    "lag-type": LACP
                }
            }
        }
    ]
}

//TODO: specify mode active

```

## OS Configuration Commands

### Cisco IOS XR 5.3.4

#### CLI

---
<pre>
interface &lt;intf-id&gt;
 bundle-id &lt;bundle-id&gt; mode active
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [xr-unit][]

### Junos 15.1F5

#### CLI

---
<pre>
TODO
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit][]