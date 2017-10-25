# configure LAG bundle member

## URL

```
openconfig-interfaces:interfaces/interface/<intf-id>
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/interfaces/src/main/yang)

```javascript
{
    "interface": [
        {
            "config": {
                "type": "ift:ethernetCsmacd",
                "enabled": true,
                "name": "<intf-id>"
            }
            "openconfig-if-ethernet:ethernet": {
                "config": {
                    "openconfig-if-aggregate:aggregate-id": <bundle-id>
                    "cisco-if-extension:mode": ACTIVE
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
 bundle-id &lt;bundle-id&gt; mode active
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [xr-unit]()

### Junos 15.1F5

#### CLI

---
<pre>
set interfaces &lt;intf-id&gt; gigether-options 802.3ad &lt;bundle-id&gt;
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit]()
