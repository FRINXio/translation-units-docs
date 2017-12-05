# Access Control List

## URL

```
frinx-openconfig-acl:acl/interfaces/interface/<intf-id>
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
                        "set-name": <in-acl-name>
                        "type": "ACL_IPV4"
                        "config": {
                            "set-name": <in-acl-name>
                            "type": "ACL_IPV4"
                        }
                    }
                ]
            }
            "egress-acl-sets": {
                "egress-acl-set": [
                    {
                        "set-name": <out-acl-name>
                        "type": "ACL_IPV4"
                        "config": {
                            "set-name": <out-acl-name>
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
  ipv4 access-group &lt;in-acl-name&gt; ingress
  ipv4 access-group &lt;out-acl-name&gt; egress
</pre>

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [xr-unit]()

### Junos 15.1F-6.9

#### CLI

<pre>
set interfaces &lt;intf-id&gt; unit 0 family inet filter input &lt;in-acl-name&gt;
set interfaces &lt;intf-id&gt; unit 0 family inet filter output &lt;out-acl-name&gt;
</pre>

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit]()
