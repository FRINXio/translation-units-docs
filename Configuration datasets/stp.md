# Configure STP interfaces

## URL

```
stp:stp
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/cdp/src/main/yang)

```javascript
{
    "stp": {
        "interfaces": {
            "interface": [
                {
                    "name": "<intf-id>",
                }
            ]
        }
    }
}
```


## OS Commands

### Brocade (V5.6.0fT163)

#### CLI

If /stp/interfaces/interface/<intf-id> exists 
---
<pre>
interface &lt;intf-id&gt;
 spanning-tree
</pre>
---

If /interfaces/interface/<intf-id> exists and /stp/interfaces/interface/<intf-id> does not exist
---
<pre>
interface &lt;intf-id&gt;
 no spanning-tree
</pre>
---

##### Unit