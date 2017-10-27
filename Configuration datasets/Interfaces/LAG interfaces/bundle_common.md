l# configure interface bundle

## URL

```
openconfig-interfaces/interfaces/interface/<intf-id>
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/interfaces/src/main/yang)

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
                    "min-links": <min-links>
                }
            }
        }
    ]
}
```

## OS Configuration Commands

### Cisco IOS XR 5.3.4

#### CLI

---
<pre>
interface &lt;intf-id&gt;
 bundle minimum-active links &lt;min-links&gt;
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [xr-unit]()

### Junos 15.1F5

#### CLI

---
<pre>
set interfaces &lt;intf-id&gt; aggregated-ether-options minimum-links &lt;min-links&gt;
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit]()
