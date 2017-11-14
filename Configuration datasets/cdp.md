# Configure CDP interfaces

## URL

```
cdp:cdp
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/cdp/src/main/yang)

```javascript
{
    "cdp": {
        "interfaces": {
            "interface": [
                {
                    "name": "<intf-id>",
                    "config": {
                        "name": "<intf-id>",
                        "enabled": true
                }
            ]
        }
    }
}
```


## OS Commands

### Cisco IOS Classic (15.2(4)S5) / XE (15.3(3)S2)

#### CLI

If cdp/interfaces/interface/<intf-id>/config/enabled is true
---
<pre>
interface &lt;intf-id&gt;
 cdp enable
</pre>
---

If cdp/interfaces/interface/<intf-id>/config/enabled is false
---
<pre>
interface &lt;intf-id&gt;
 no cdp enable
</pre>
---

##### Unit

### Cisco IOS Xr (XRv 5.1.3 and XRv 6.1.2 tested)

#### CLI

If cdp/interfaces/interface/<intf-id>/config/enabled is true
---
<pre>
interface &lt;intf-id&gt;
 cdp
</pre>
---

If cdp/interfaces/interface/<intf-id>/config/enabled is false
---
<pre>
interface &lt;intf-id&gt;
 no cdp
</pre>
---

##### Unit

### Brocade (V5.6.0fT163)

#### CLI

If cdp/interfaces/interface/<intf-id>/config/enabled is true
---
<pre>
interface &lt;intf-id&gt;
 cdp enable
</pre>
---

If cdp/interfaces/interface/<intf-id>/config/enabled is false
---
<pre>
interface &lt;intf-id&gt;
 no cdp enable
</pre>
---

##### Unit