# Access Control List

## URL

```
frinx-openconfig-acl:acl/interfaces/interface/{{iacl_intf_id}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/acl/src/main/yang)

```javascript
{
    "interface": [
        {
            "id": "{{iacl_intf-id}}",
            "ingress-acl-sets": {
                "ingress-acl-set": [
                    {
                        "set-name": "{{iacl_in_acl_name}}",
                        "type": "ACL_IPV4|ACL_IPV6",
                        "config": {
                            "set-name": "{{iacl_in_acl_name}}",
                            "type": "ACL_IPV4|ACL_IPV6"
                        }
                    }
                ]
            },
            "egress-acl-sets": {
                "egress-acl-set": [
                    {
                        "set-name": "{{iacl_out_acl_name}}",
                        "type": "ACL_IPV4|ACL_IPV6",
                        "config": {
                            "set-name": "{{iacl_out_acl_name}}",
                            "type": "ACL_IPV4|ACL_IPV6"
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
interface {{iacl_intf_id}}
  ipv4|ipv6 access-group {{iacl_in_acl_name}} ingress
  ipv4|ipv6 access-group {{iacl_out_acl_name}} egress
</pre>

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/acl)

### Junos 14.1X53-D40.8

#### CLI

<pre>
set interfaces {{iacl_intf_id}} unit 0 family inet filter input {{iacl_in_acl_name}}
</pre>

##### Unit

Link to github : [junos-unit](https://github.com/FRINXio/unitopo-units/tree/master/junos/junos-14-acl-unit)

### Junos 17.3R1.10

#### CLI

<pre>
set interfaces {{iacl_intf_id}} unit 0 family inet filter input {{iacl_in_acl_name}}
set interfaces {{iacl_intf_id}} unit 0 family inet filter output {{iacl_out_acl_name}}
</pre>

##### Unit

Link to github : [junos-unit](https://github.com/FRINXio/unitopo-units/tree/master/junos/junos-17-acl-unit)
