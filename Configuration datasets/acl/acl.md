# Access Control List

## URL

```
frinx-openconfig-acl:/acl/acl-sets/acl-set/{{acl_name}}
```

## OPENCONFIG YANG


```javascript
{
    "acl-set": [
        {
            "name": "{{acl_name}}",
            "config": {
            	"name": "{{acl_name}}",
            	"type": "{{acl_type}}"
            },
            "acl-entries": {
                "acl-entry": [
                    {
                        "sequence-id": "{{acl_seq_id}}",
                        "config": {
                            "sequence-id": "{{acl_seq_id}}",
                            "frinx-acl-extension:term-name": "{{acl_term_name}}"
                        },
                        "ipv4|ipv6": {
                            "config": {
                            	"protocol": {{acl_protocol}},
                            	"source-address": "{{acl_src_addr}}",
                            	"destination-address": "{{acl_dst_addr}}",
                            	"frinx-acl-extension:hop-range": "{{min_acl_ttl}}..{{max_acl_ttl}}",
				"frinx-acl-extension:source-address-wildcarded": {
                                    "wildcard-mask": "{{wildcard-mask}}",
                                    "address": "{{wildcard_addr}}"
                                },
				"frinx-acl-extension:destination-address-wildcarded": {
                                    "wildcard-mask": "{{wildcard-mask}}",
                                    "address": "{{wildcard_addr}}"
                                },
                            }
                        },
                        "icmp": {
                            "config": {
                            	"msg-type": "{{acl_icmp_msg_type}} | ANY"
                            }
                        },
                        "transport": {
                            "config": {
                            	"source-port": "{{acl_src_port}}",
                            	"destination-port": "{{acl_dst_port}}"
				"frinx-acl-extension:source-port-named": "{{source-port-named}}"
				"frinx-acl-extension:destination-port-named": "{{destination-port-named}}"
                            }
                        },

                        "actions": {
                            "config": {
                                "forwarding-action": "{{acl_fwd_action}}",
                                "frinx-acl-extension:instance-name": "{{acl_instance_name}}",
                                "log-action": "{{}}"
                            }
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
ipv4|ipv6 access-list {{acl_name}} 
	{{acl_seq_id}} {{acl_fwd_action}} {{acl_protocol}} {{acl_src_addr}} {range {{acl_src_port}} }  {{acl_dst_addr}} {range {{acl_dst_port}} } {{acl_icmp_msg_type}} ttl range {{min_acl_ttl}} {{max_acl_ttl}}
</pre>

*ipv4|ipv6* is a conversion of {{acl_type}}


##### Examples

<pre>
ipv4 access-list test123
	2 permit 4.4.4.4/32 7.7.7.7/32
</pre>

<pre>
ipv4 access-list test123
	3 permit tcp 1.1.1.1/32 range 1024 65535 2.2.2.2/32 range 0 1023
</pre>

<pre>
ipv4 access-list test123
	5 deny icmp 1.1.1.1/32 2.2.2.2/32 8 ttl range 0 10
</pre>

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/acl)

### Junos 14.1X53-D40.8

#### CLI

<pre>
set firewall family inet filter {{acl_name}} term {{acl_term_name}} from source-address {{acl_src_addr}}
set firewall family inet filter {{acl_name}} term {{acl_term_name}} from protocol {{acl_protocol}}
set firewall family inet filter {{acl_name}} term {{acl_term_name}} from destination-port {{acl_dst_port}}
set firewall family inet filter {{acl_name}} term {{acl_term_name}} then {{acl_fwd_action}}
</pre>

<pre>
set firewall family inet filter {{acl_name}} term {{acl_term_name}} then routing-instance {{acl_instance_name}}
</pre>

##### Unit

Link to github : [junos-unit](https://github.com/FRINXio/unitopo-units/tree/master/junos/junos-17-acl-unit)
