# Interface LACP configuration

## URL

```
openconfig-lacp:lacp/interfaces/interface/<intf-id>
```

## OPENCONFIG YANG

```javascript
{
    "interface": [
        {
            "name": <intf-id>
            "config": {
                "name": <intf-id>
                "interval": "FAST"
                "lacp-mode": "ACTIVE"
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
   lacp period short
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [xr-unit][]

### Junos 15.1F5

#### CLI

---
<pre>
set interfaces &lt;intf-id&gt; aggregated-ether-options lacp active
set interfaces &lt;intf-id&gt; aggregated-ether-options lacp periodic fast
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit][]
