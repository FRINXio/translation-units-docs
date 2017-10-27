# Interface policy configuration

## URL

```
openconfig-network-instance:network-instances/network-instance/<ni-name>/openconfig-policy-forwarding:policy-forwarding/interfaces/interface/<intf-id>
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/interfaces/src/main/yang)

```javascript
{
    "interface": [
        {
            "interface-id": <intf-id>
            "config": {
                "interface-id": <intf-id>
                "apply-forwarding-policy": <policy-name>
                "direction": <ingress/egress>
            }
            "interface-ref": {
                "config": {
                    "interface": <intf-id>
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
 service-policy &lt;input/output&gt; &lt;policy-name&gt;
</pre>

*input* is conversion of *"direction": "ingress"*  
*output* is conversion of *"direction": "egress"*

---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [xr-unit]()

### Junos 15.1F5

#### CLI

---
<pre>
set class-of-service interfaces &lt;intf-id&gt; scheduler-map &lt;policy-name&gt;
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit]()
