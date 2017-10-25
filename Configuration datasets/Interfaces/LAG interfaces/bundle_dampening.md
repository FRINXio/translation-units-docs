# interface dampening configuration

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
                    "interfaces-damp:damp": {
                        "enabled": true,
                        "half-life": <half-life>,
                        "reuse": <reuse>,
                        "suppress": <suppres>,
                        "max-supress": <max-supress>
                    }
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
 dampening
 dampening &lt;half-life&gt; &lt;reuse&gt; &lt;supress&gt; &lt;max-supress&gt;
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [xr-unit]()

### Junos 15.1F5

#### CLI

---
<pre>
set interfaces &lt;intf-id&gt; damping enable
set interfaces &lt;intf-id&gt; damping half-life &lt;half-life&gt;
set interfaces &lt;intf-id&gt; damping max-suppress &lt;max-supress&gt;
set interfaces &lt;intf-id&gt; damping reuse &lt;reuse&gt;
set interfaces &lt;intf-id&gt; damping suppress &lt;supress&gt;
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit]()
