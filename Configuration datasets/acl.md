# Access Control List

## URL

```
openconfig-acl:acl/interfaces/interface/<intf-id>
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/acl/src/main/yang)

```javascript
{
    "interface": [
        {
            "id": <intf-id>
            "config": {
                "id": <intf-id>
            }
            "interface-ref": {
                "config": {
                    "interface": <intf-id>
                }
            }
            "ingress-acl-sets": {
                "ingress-acl-set": [
                    {
                        "set-name": <in_acl_name>
                        "type": "ACL_IPV4"
                        "config": {
                            "set-name": <in_acl_name>
                            "type": "ACL_IPV4"
                        }
                    }
                ]
            }
            "egress-acl-sets": {
                "egress-acl-set": [
                    {
                        "set-name": <out_acl_name>
                        "type": "ACL_IPV4"
                        "config": {
                            "set-name": <out_acl_name>
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

<pre>
interface &lt;intf-id&gt;
  ipv4 access-group &lt;in_acl_name&gt; &lt;ingress&gt;
  ipv4 access-group &lt;out_acl_name&gt; &lt;egress&gt;
</pre>

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [xr-unit]()

### Junos 15.1F-6.9

#### CLI

<pre>
set interfaces &lt;intf-id&gt; unit 0 family inet filter &lt;input&gt; &lt;in_acl_name&gt;
set interfaces &lt;intf-id&gt; unit 0 family inet filter &lt;output&gt; &lt;out_acl_name&gt;
</pre>

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit]()
