# interface dampening configuration

## URL

```
openconfig-interfaces/interfaces/interface/<intf-id>
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
                }
            }
        }
    ]
}

//TODO: dampening configuration not available in openconfig

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

Link to github : [xr-unit][]

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

Link to github : [junos-unit][]
