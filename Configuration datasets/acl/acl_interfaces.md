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
            "id": "{{iacl_intf_id}}",
            "config": {
               "id":"{{iacl_intf_id}}"
            },
            "ingress-acl-sets": {
                "ingress-acl-set": [
                    {
                        "set-name": "{{iacl_in_acl_name}}",
                        "type": "frinx-openconfig-acl:ACL_IPV4|frinx-openconfig-acl:ACL_IPV6",
                        "config": {
                            "set-name": "{{iacl_in_acl_name}}",
                            "type": "frinx-openconfig-acl:ACL_IPV4|frinx-openconfig-acl:ACL_IPV6"
                        }
                    }
                ]
            },
            "egress-acl-sets": {
                "egress-acl-set": [
                    {
                        "set-name": "{{iacl_out_acl_name}}",
                        "type": "frinx-openconfig-acl:ACL_IPV4|frinx-openconfig-acl:ACL_IPV6",
                        "config": {
                            "set-name": "{{iacl_out_acl_name}}",
                            "type": "frinx-openconfig-acl:ACL_IPV4|frinx-openconfig-acl:ACL_IPV6"
                        }
                    }
                ]
            }
        }
    ]
}
```

## OS Configuration Commands

### Cisco IOS XR 5.3.4, IOS XR 6.6.2

#### CLI

<pre>
interface {{iacl_intf_id}}
  ipv4|ipv6 access-group {{iacl_in_acl_name}} ingress
  ipv4|ipv6 access-group {{iacl_out_acl_name}} egress
</pre>

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/acl)

### Cisco IOS XE 15.4(2)S

#### CLI

<pre>
interface {{iacl_intf_id}}
  ip access-group {{iacl_in_acl_name}} in|out
  ipv6 traffic-filter {{iacl_out_acl_name}} in|out
</pre>

##### Examples

<pre>
interface GigabitEthernet1
 ip access-group inacl1 in
 ipv6 traffic-filter outacl1 out
</pre>

##### Unit

Link to github : [xe-unit](https://github.com/FRINXio/cli-units/tree/master/ios/acl)

### Junos 14.1X53-D40.8

#### CLI

<pre>
set interfaces {{iacl_intf_id}} unit 0 family inet filter input {{iacl_in_acl_name}}
</pre>

##### Unit

Link to github : [junos-unit](https://github.com/FRINXio/cli-units/tree/master/junos/acl)

### Junos 17.3R1.10

#### CLI

<pre>
set interfaces {{iacl_intf_id}} unit 0 family inet filter input {{iacl_in_acl_name}}
set interfaces {{iacl_intf_id}} unit 0 family inet filter output {{iacl_out_acl_name}}
</pre>

##### Unit

Link to github : [junos-unit](https://github.com/FRINXio/unitopo-units/tree/master/junos/junos-17/junos-17-acl-unit)

### Junos 18.2R1-S2.1

#### CLI

<pre>
set interfaces {{iacl_intf_index}} unit {{iacl_subintf_index}} family inet filter input {{iacl_in_acl_name}}
set interfaces {{iacl_intf_index}} unit {{iacl_subintf_index}} family inet filter output {{iacl_out_acl_name}}
</pre>

*iacl_intf_index* , *iacl_subintf_index* is a conversion of {{iacl_intf_id}} set {{iacl_intf_index}}.{{iacl_subintf_index}}

##### Unit

Link to github : [junos-unit](https://github.com/FRINXio/unitopo-units/tree/master/junos/junos-18/junos-18-acl-unit)
