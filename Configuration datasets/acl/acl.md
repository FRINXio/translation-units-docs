# Access Control List

## URL

```
frinx-openconfig-acl:acl/acl-sets/acl-set={{acl_name}},{{acl_type}}
```

## OPENCONFIG YANG


```javascript
{
    "acl-set": [
        {
            "name": "{{acl_name}}",
            "type": "{{acl_type}}"
            "config": {
            	"name": "{{acl_name}}",
            	"type": "{{acl_type}}",
		"frinx-acl-extension:default-fwd-action": "{{acl_default_fwd_action}}",
		"frinx-acl-extension:enabled": false
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

### Cisco IOS XR 6.6.2

#### CLI

<pre>
ipv4|ipv6 access-list {{acl_name}} 
    {{acl_seq_id}} {{acl_fwd_action}} {{acl_protocol}} {{acl_src_addr}} {range {{acl_src_port}} }  {{acl_dst_addr}} {range {{acl_dst_port}} }
</pre>

*ipv4|ipv6* is a conversion of {{acl_type}}

##### Examples

<pre>
ipv4 access-list test123
  10 deny ipv4 10.0.0.0/8 any
  20 deny ipv4 any 172.16.0.0/12
  30 permit ipv4 any any
</pre>

<pre>
ipv6 access-list test123
  10 permit icmpv6 any any
  20 deny ipv6 ::/8 any
  30 permit ipv6 any any
</pre>

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/acl)

### Cisco IOS XE 15.4(2)S

#### CLI

<pre>
ip access-list extend {{acl_name}}
	{{acl_seq_id}} {{acl_fwd_action}} {{acl_protocol}} {{acl_src_addr}} {range {{acl_src_port}} }  {{acl_dst_addr}} {range {{acl_dst_port}} }
</pre> 

<pre>
ipv6 access-list {{acl_name}}
	 {{acl_fwd_action}} {{acl_protocol}} {{acl_src_addr}} {range {{acl_src_port}} }  {{acl_dst_addr}} {range {{acl_dst_port}} } sequence {{acl_seq_id}}
</pre>


##### Examples

<pre>
ip access-list extended TEST1
    3 permit tcp host 1.1.1.1 eq 1024 host 2.2.2.2 eq 0
    10 deny ip any any
</pre>

<pre>
ipv6 access-list TEST2
    deny icmp any any sequence 10
    deny ipv6 any 2400:2000:3::/48 sequence 20
    deny udp host 10:11:12::2 any sequence 2
</pre>

##### Unit

Link to github : [xe-unit](https://github.com/FRINXio/cli-units/tree/master/ios/acl)

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

Link to github : [junos-unit](https://github.com/FRINXio/unitopo-units/tree/master/junos/junos-17/junos-17-acl-unit)

### Ciena SAOS 6.14

#### CLI

<pre>
access-list create acl-profile {{acl_name}} default-filter-action {{acl_default_fwd_action}}
access-list disable profile {{acl_name}}
access-list add profile {{acl_name}} rule {{acl_term_name}} precedence {{acl_seq_id}} filter-action {{acl_fwd_action}} any
</pre>

{{acl_default_fwd_action}} conversion is ACCEPT = allow, DROP = deny  
*access-list disable profile {{acl_name}}* is a conversion of *frinx-acl-extension:enabled* set to false. Default value is true.  


##### Unit

Link to github : [saos-unit]
