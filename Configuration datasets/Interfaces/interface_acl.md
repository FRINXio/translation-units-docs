# Interface ACL configuration

## URL

```
openconfig-acl:acl/interfaces/interface/<intf-id>
```

## OPENCONFIG YANG

```javascript
{
    "interface": [
        {
            "ingress-acl-sets": {
                "ingress-acl-set": [
                    {
                        "set-name": <acl_name>
                        "type": "ACL_IPV4"
                        "config": {
                            "set-name": <acl_name>
                            "type": "ACL_IPV4"
                        }
                    }
                ]
            }
            "egress-acl-sets": {
                "egress-acl-set": [
                    {
                        "set-name": <acl_name>
                        "type": "ACL_IPV4"
                        "config": {
                            "set-name": <acl_name>
                            "type": "ACL_IPV4"
                        }
                    }
                ]
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
  ipv4 access-group &lt;acl_name&gt; &lt;ingress/egress&gt;
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [xr-unit][]

### Junos 15.1F5

#### CLI

---
<pre>
set interfaces &lt;intf-id&gt; unit 0 family inet filter &lt;input/output&gt; &lt;acl_name&gt;
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit][]
