# Interface policy configuration

## URL

```
openconfig-network-instance:network-instances/network-instance/<ni-name>/openconfig-policy-forwarding:policy-forwarding/interfaces/interface/<intf-id>
```

## OPENCONFIG YANG

```javascript
{
    "interface": [
        {
            "config": {
                "interface-id": <intf-id>
                "apply-forwarding-policy": <policy-name>
            }
        }
    ]
}

// TODO add augment to 'input/output' - for XR, because we don't model policy
```

## OS Configuration Commands

### Cisco IOS XR 5.3.4

#### CLI

---
<pre>
interface &lt;intf-id&gt;
 service-policy input &lt;policy-name&gt;
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [xr-unit][]

### Junos 15.1F5

#### CLI

---
<pre>
set class-of-service interfaces &lt;intf-id&gt; scheduler-map &lt;policy-name&gt;
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit][]
