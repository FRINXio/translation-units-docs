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
                            "sequence-id": "{{acl_seq_id}}"
                        },
                        "ipv4|ipv6": {
                            "config": {
                            	"protocol": {{acl_protocol}},
                            	"source-address": "{{acl_src_addr}}",
                            	"destination-address": "{{acl_dst_addr}}",
                            	"frinx-acl-extension:hop-range": "{{min_acl_ttl}}..{{max_acl_ttl}}",
				"frinx-acl-extension:source-address-wildcarded": {
                                    "wildcard-mask": "0.255.255.255",
                                    "address": "0.0.0.0"
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
                            }
                        },

                        "actions": {
                            "config": {
                            	"forwarding-action": "{{acl_fwd_action}}",
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
