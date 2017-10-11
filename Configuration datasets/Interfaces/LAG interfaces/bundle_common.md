# configure interface bundle

## URL

```
openconfig-interfaces/interfaces/interface/<intf-id>
```

## OPENCONFIG YANG

```json
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
                    "min-links": <min-links>
                }
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
 bundle minimum-active links &lt;min-links&gt;
</pre>
---

#### Junos

---
<pre>
set interfaces &lt;intf-id&gt; aggregated-ether-options minimum-links &lt;min-links&gt;
</pre>
---
