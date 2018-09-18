# Routing Policy

## URL

```
frinx-openconfig-routing-policy:routing-policy/policy-definitions/policy-definition/{{rpol_name}}
```

## OPENCONFIG YANG


```javascript
{
    "policy-definition": [
        {
            "name": "{{rpol_name}}",
            "config": {
                "name": "{{rpol_name}}"
            },
            "statements": {
                "statement": [
                    {
                        "name": "{{rpol_s_name}}",
                        "config": {
                            "name": "{{rpol_s_name}}"
                        },
                        "conditions": {
                            "config": {
                                "call-policy": {{rpol_s_c_callpolicy}},
                                "install-protocol-eq": {{rpol_s_c_protocol_eq}}
                            },
                            "match-prefix-set": {
                                "config": {
                                    "prefix-set": "{{pset}}",
                                    "match-set-options": "{{rpol_s_c_prefixset_opts}}"
                                }
                            },
                            "bgp-conditions": {
                                "as-path-length": {
                                    "config": {
                                        "operator": "{{rpol_s_c_bgp_aslen_oper}}",
                                        "value": "{{rpol_s_c_bgp_aslen_val}}"
                                    }
                                },
                                "match-community-set": {
                                    "config": {
                                        "community-set": "{{cset_name}}",
                                        "match-set-options": "{{rpol_s_c_bgp_comset_opts}}"
                                    }
                                },
                                "match-as-path-set": {
                                    "config": {
                                        "as-path-set": "{{aset_name}}",
                                        "match-set-options": "{{rpol_s_c_bgp_aspathset_opts}}"
                                    }
                                }
                            },
                            "match-protocol-instance": {
                                "config": {
                                    "prefix-set": "{{pset}}",
                                    "match-set-options": "{{rpol_s_c_prefixset_opts}}"
                                }
                            },
                        },
                        "actions": {
                            "config": {
                                "policy-result": {{rpol_s_a_result}}
                            },
                            "bgp-actions": {
                                "config": {
                                    "set-local-pref": {{rpol_s_a_bgp_set_localpref}},
                                    "set-next-hop": {{rpol_s_a_bgp_set_nexthop}},
                                    "set-med": {{rpol_s_a_bgp_set_med}}
                                },
                                "set-community": {
                                    "config": {
                                        "method": "REFERENCE",
                                        "options": "{{rpol_s_a_bgp_comset_opts}}"
                                    },
                                    "reference": {
                                        "config": {
                                            "community-set-ref": "{{cset_name}}"
                                        }
                                    }
                                },
                                "set-as-path-prepend": {
                                    "config": {
                                        "asn": "{{rpol_s_a_bgp_aspathprep_asn}}",
                                        "repeat-n": "{{rpol_s_a_bgp_aspathprep_repeatn}}"
                                    }
                                }
                            }
                        }
                    }
                ]
            }
        }
    ]
}
```

```
frinx-openconfig-routing-policy:routing-policy/defined-sets/prefix-sets/prefix-set/{{pset_name}}
```

```javascript
{
    "prefix-set": [
        {
            "name": "{{pset_name}}",
            "config": {
                "name": "{{pset_name}}"
            },
            "prefixes": {
                "prefix": [
                    {
                        "ip-prefix": "{{prefix}}",
                        "masklength-range": "{{prefix_mask}}"
                        "config": {
                            "ip-prefix": "{{prefix}}",
                            "masklength-range": "{{prefix_masklength}}"
                        }
                    }
                ]
            }
        }
    ]
}
```

```
frinx-openconfig-routing-policy:routing-policy/defined-sets/bgp-defined-sets/community-sets/community-set/{{cset_name}}
```

```javascript
{
    "community-set": [
        {
            "community-set-name": "{{cset_name}}",
            "config": {
                "community-set-name": "{{cset_name}}",
                "community-member": [
                    "cset_member1",
                    "cset_member2",
                    "cset_member3"
                ]
            }
        }
    ]
}
```

```
frinx-openconfig-routing-policy:routing-policy/defined-sets/bgp-defined-sets/as-path-sets/as-path-set/{{aset_name}}
```

```javascript
{
    "as-path-set": [
        {
            "as-path-set-name": "{{aset_name}}",
            "config": {
                "as-path-set-name": "{{aset_name}}",
                "as-path-set-member": [
                    "aset_member1",
                    "aset_member2",
                    "aset_member3"
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
prefix-set {{pset_name}}
  {{pset_member1}}/{{prefix_masklength1}},
  {{pset_member2}}/{{prefix_masklength2}},
  {{pset_member3}}/{{prefix_masklength3}}
end-set

community-set {{cset_name}}
  {{cset_member1}},
  {{cset_member2}},
  {{cset_member3}}
end-set

as-path-set {{aset_name}}
  ios-regex '_{{aset_member1}}$',
  ios-regex '_{{aset_member2}}$',
  ios-regex '_{{aset_member3}}$'
end-set

route-policy {{rpol_name}}
    if destination in {{pset_name}} /
            and as-path length {{rpol_s_c_bgp_aslen_oper}} /
            and community match-{{rpol_s_c_bgp_comset_opts}} {{cset_name}} /
            and as-path in {{aset_name}} then
        drop
        done
        apply {{rpol_s_c_callpolicy}}
        set local-preference {{rpol_s_a_bgp_set_localpref}}
        set next-hop {{rpol_s_a_bgp_set_nexthop}}
        set med {{rpol_s_a_bgp_set_med}}
        set community {{cset_name}} {{rpol_s_a_bgp_comset_opts}}
        prepend as-path {{rpol_s_a_bgp_aspathprep_asn}} {{rpol_s_a_bgp_aspathprep_repeatn}}
    endif
end-policy

</pre>

##### Examples

<pre>
route-policy route_policy_1
    set next-hop {{rpol_s_a_bgp_set_nexthop}}
    apply route_subpolicy_1
end-policy
</pre>

```javascript
{
    "policy-definition": [
        {
            "name": "route_policy_1",
            "config": {
                "name": "route_policy_1"
            },
            "statements": {
                "statement": [
                    {
                        "name": "statement_1",
                        "config": {
                            "name": "statement_1"
                        },
                        "conditions": {
                            "config": {
                                "call-policy": route_subpolicy_1
                            }
                        }
                        "actions": {
                            "bgp-actions": {
                                "config": {
                                    "set-next-hop": {{rpol_s_a_bgp_set_nexthop}}
                                }
                            }
                        }
                    }
                ]
            }
        }
    ]
}
```

<pre>
route-policy route_policy_2
    if as-path length ge 100 then
        drop
    elseif destination in pset_name then
        set med 10
        set local-preference 15
        set community cset_name [additive]
        done
    elseif as-path in aset_name then 
        set med 20
        done
    else
        set local-preference 15
        done
    endif
end-policy
</pre>

```javascript
{
    "policy-definition": [
        {
            "name": "route_policy_2",
            "config": {
                "name": "route_policy_2"
            },
            "statements": {
                "statement": [
                    {
                        "name": "statement_1",
                        "config": {
                            "name": "statement_1"
                        },
                        "conditions": {
                            "bgp-conditions": {
                                "as-path-length": {
                                    "config": {
                                        "operator": "ATTRIBUTE_GE",
                                        "value": "100"
                                    }
                                }
                            }
                        },
                        "actions": {
                            "config": {
                                "policy-result": "REJECT_ROUTE"
                            }
                        }
                    }
                    {
                        "name": "statement_2",
                        "config": {
                            "name": "statement_2"
                        },
                        "conditions": {
                            "match-prefix-set": {
                                "config": {
                                    "prefix-set": "pset_name",
                                    "match-set-options": "ANY"
                                }
                            }
                        },
                        "actions": {
                            "config": {
                                "policy-result": "ACCEPT_ROUTE"
                            },
                            "bgp-actions": {
                                "config": {
                                    "set-local-pref": 15,
                                    "set-med": 10
                                },
                                "set-community": {
                                    "config": {
                                        "method": "INLINE",
                                        "options": "ADD|REMOVE|REPLACE"
                                    },
                                    "inline": {
                                        "config": {
                                            "communities": "123:333"
                                        }
                                    }
                                }
                            }
                        }
                    }
                    {
                        "name": "statement_3",
                        "config": {
                            "name": "statement_3"
                        },
                        "conditions": {
                            "bgp-conditions": {
                                "as-path-set": {
                                    "config": {
                                        "as-path-set": "aset_name",
                                        "match-set-options": "ANY"
                                    }
                                }
                            }
                        },
                        "actions": {
                            "config": {
                                "policy-result": "ACCEPT_ROUTE"
                            },
                            "bgp-actions": {
                                "config": {
                                    "set-med": 20
                                }
                            }
                        }
                    }
                    {
                        "name": "statement_4",
                        "config": {
                            "name": "statement_4"
                        },
                        "actions": {
                            "config": {
                                "policy-result": "ACCEPT_ROUTE"
                            },
                            "bgp-actions": {
                                "config": {
                                    "set-local-pref": 15
                                }
                            }
                        }
                    }
                ]
            }
        }
    ]
}
```


<pre>
route-policy route_policy_3
    if destination in pset_name then
        drop
    elseif community match-any cset_name then 
        set med 1
        prepend as-path 123 3
        done
    elseif destination in pset_name and as-path in aset_name then 
        set med 2
        done
    else
        set med 3
        done
    endif
end-policy
</pre>

```javascript
{
    "policy-definition": [
        {
            "name": "route_policy_4",
            "config": {
                "name": "route_policy_4"
            },
            "statements": {
                "statement": [
                    {
                        "name": "statement_1",
                        "config": {
                            "name": "statement_1"
                        },
                        "conditions": {
                            "match-prefix-set": {
                                "config": {
                                    "prefix-set": "pset_name",
                                    "match-set-options": "ANY"
                                }
                            }
                        },
                        "actions": {
                            "config": {
                                "policy-result": "REJECT_ROUTE"
                            }
                        }
                    }
                    {
                        "name": "statement_2",
                        "config": {
                            "name": "statement_2"
                        },
                        "conditions": {
                            "bgp-conditions": {
                                "match-community-set": {
                                    "config": {
                                        "community-set": "cset_name",
                                        "match-set-options": "ANY"
                                    }
                                }
                            }
                        },
                        "actions": {
                            "config": {
                                "policy-result": "ACCEPT_ROUTE"
                            },
                            "bgp-actions": {
                                "config": {
                                    "set-med": 1
                                },
                                "set-as-path-prepend": {
                                    "config": {
                                        "asn": 123,
                                        "repeat-n": 3
                                    }
                                }
                            }
                        }
                    }
                    {
                        "name": "statement_3",
                        "config": {
                            "name": "statement_3"
                        },
                        "conditions": {
                            "match-prefix-set": {
                                "config": {
                                    "prefix-set": "pset_name",
                                    "match-set-options": "ANY"
                                }
                            }
                            "bgp-conditions": {
                                "as-path-set": {
                                    "config": {
                                        "as-path-set": "aset_name",
                                        "match-set-options": "ANY"
                                    }
                                }
                            }
                        },
                        "actions": {
                            "config": {
                                "policy-result": "ACCEPT_ROUTE"
                            },
                            "bgp-actions": {
                                "config": {
                                    "set-med": 2
                                }
                            }
                        }
                    }
                    {
                        "name": "statement_4",
                        "config": {
                            "name": "statement_4"
                        },
                        "actions": {
                            "config": {
                                "policy-result": "ACCEPT_ROUTE"
                            },
                            "bgp-actions": {
                                "config": {
                                    "set-med": 3
                                }
                            }
                        }
                    }
                ]
            }
        }
    ]
}
```

### Junos 17.3R1.10

#### CLI

<pre>
set policy-options policy-statement {{rpol_name}} term {{rpol_s_name}} from instance master
set policy-options policy-statement {{rpol_name}} term {{rpol_s_name}} then {{rpol_s_a_result}}
</pre>

<pre>
set policy-options policy-statement {{rpol_name}} term {{rpol_s_name}} from protocol direct
set policy-options policy-statement {{rpol_name}} term {{rpol_s_name}} then metric <1-65535>
set policy-options policy-statement {{rpol_name}} term {{rpol_s_name}} then {{rpol_s_a_result}}
</pre>


##### Examples

<pre>
set policy-options policy-statement IMPORT term 1 from instance master
set policy-options policy-statement IMPORT term 1 then accept
</pre>

```javascript
{
    "policy-definition": [
        {
            "name": "IMPORT",
            "config": {
                "name": "IMPORT"
            },
            "statements": {
                "statement": [
                    {
                        "name": "1",
                        "config": {
                            "name": "1"
                        },
                        "conditions": {
                            "oc-ni-pol:match-protocol-instance": {
                                "config": {
                                    "protocol-name": default
                                }
                            }
                        }
                        "actions": {
                            "config": {
                                "policy-result": "ACCEPT_ROUTE"
                            }
                        }
                    }
                ]
            }
        }
    ]
}
```
