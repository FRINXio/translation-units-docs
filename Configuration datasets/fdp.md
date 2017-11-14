# Configure FDP interfaces

## URL

```
fdp:fdp
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/fdp/src/main/yang)

```javascript
{
    "fdp": {
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


### Brocade (V5.6.0fT163)

#### CLI

If fdp/interfaces/interface/<intf-id>/config/enabled is true
---
<pre>
interface &lt;intf-id&gt;
 fdp enable
</pre>
---

If fdp/interfaces/interface/<intf-id>/config/enabled is false
---
<pre>
interface &lt;intf-id&gt;
 no fdp enable
</pre>
---

##### Unit