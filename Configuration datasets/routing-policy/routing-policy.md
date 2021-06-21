# Routing Policy

## URL

```
frinx-openconfig-routing-policy:routing-policy/policy-definitions/policy-definition={{rpol_name}}?content=nonconfig
```

## OPENCONFIG YANG


```javascript
{
    "frinx-openconfig-routing-policy:policy-definition": [
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
                                    "prefix-set": "{{pset_name}}",
                                    "match-set-options": "{{rpol_s_c_prefixset_opts}}"
                                }
                            },
                            "frinx-openconfig-bgp-policy:bgp-conditions": {
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
                                    "protocol-identifier": "{{rpol_s_c_protocol_type}}",
                                    "protocol-name": "{{rpol_s_c_protocol_name}}"
                                }
                            }
                        },
                        "actions": {
                            "config": {
                                "policy-result": {{rpol_s_a_result}}
                            },
                            "frinx-openconfig-bgp-policy:bgp-actions": {
                                "config": {
                                    "set-local-pref": {{rpol_s_a_bgp_set_localpref}},
                                    "set-next-hop": {{rpol_s_a_bgp_set_nexthop}},
                                    "set-med": {{rpol_s_a_bgp_set_med}}
                                },
                                "set-community": {
                                    "config": {
                                        "method": "REFERENCE|INLINE",
                                        "options": "{{rpol_s_a_bgp_comset_opts}}"
                                    },
                                    "reference": {
                                        "config": {
                                            "community-set-ref": "{{cset_name}}"
                                        }
                                    },
                                    "inline": {
                                        "config": {
                                            "communities": [
                                                {{rpol_s_a_bgp_well_known_comm}},
                                                {{rpol_s_a_bgp_comm}}
                                            ]
                                        }
                                    }
                                },
                                "set-as-path-prepend": {
                                    "config": {
                                        "asn": "{{rpol_s_a_bgp_aspathprep_asn}}",
                                        "repeat-n": "{{rpol_s_a_bgp_aspathprep_repeatn}}"
                                    }
                                }
                            },
                            "ospf-actions": {
                                "set-metric": {
                                    "config": {
                                        "metric": {{rpol_s_a_ospf_metric}}
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
frinx-openconfig-routing-policy:routing-policy/defined-sets/prefix-sets/prefix-set={{pset_name}}?content=nonconfig
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
                        "ip-prefix": "{{prefix}}/{{prefix_length}}",
                        "masklength-range": "{{prefix_range}}",
                        "config": {
                            "ip-prefix": "{{prefix}}/{{prefix_length}}",
                            "masklength-range": "{{prefix_range}}",
                            "frinx-cisco-routing-policy-extension:sequence-id": {{sequence_id}},
                            "frinx-cisco-routing-policy-extension:operation": "{{operation}}",
                            "frinx-cisco-routing-policy-extension:minimum-prefix-length": {{minimum_prefix_length}},
                            "frinx-cisco-routing-policy-extension:maximum-prefix-length": {{maximum_prefix_length}}
                        }
                    }
                ]
            }
        }
    ]
}
```

```
frinx-openconfig-routing-policy:routing-policy/defined-sets/bgp-defined-sets/community-sets/community-set={{cset_name}}?content=nonconfig
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
frinx-openconfig-routing-policy:routing-policy/defined-sets/bgp-defined-sets/as-path-sets/as-path-set={{aset_name}}
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

### Cisco IOS 12, IOS 15

<pre>
ip prefix-list {{pset_name}} seq {{sequence_id}} {{operation}} {{prefix}}/{{prefix_length}} ge {{minimum_prefix_length}} le {{maximum_prefix_length}}
</pre>

*permit* is a conversion of {{operation}} set to *frinx-cisco-routing-policy-extension:PERMIT*  
*deny* is a conversion of {{operation}} set to *frinx-cisco-routing-policy-extension:DENY*  

### Cisco IOS XR 5.3.4, IOS XR 6.6.2

#### CLI


<pre>
prefix-set {{pset_name}}
  {{prefix}}/{{prefix_length}} [{{prefix_range_options}}] 
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
    if [not] destination in {{pset_name}} /
            and as-path length le|ge|eq {{rpol_s_c_bgp_aslen_val}}/
            and community match-any|match-every {{cset_name}} /
            and [not] as-path in {{aset_name}} then
        drop
        done
        pass
        apply {{rpol_s_c_callpolicy}}
        set local-preference {{rpol_s_a_bgp_set_localpref}}
        set next-hop {{rpol_s_a_bgp_set_nexthop}}
        set med {{rpol_s_a_bgp_set_med}}
        set community {{cset_name}} {{rpol_s_a_bgp_comset_opts}}
        set community (no-export, no-advertise, local-as, {{rpol_s_a_bgp_comm}})
        prepend as-path {{rpol_s_a_bgp_aspathprep_asn}} {{rpol_s_a_bgp_aspathprep_repeatn}}
    endif
end-policy

</pre>

{{prefix_range_options}} is parsed from {{prefix_range}}.
* If {{prefix_range}} is *"exact"*, then {{prefix_range_options}} is not set.
* If {{prefix_range}} matches to pattern of *{{le_range}}..{{ge_range}}* , then {{prefix_range_options}} is set as *"le {{le_range}} ge {{ge_range}}"*.

*destination in {{pset_name}}* is a conversion of {{rpol_s_c_prefixset_opts}} set to *ANY*  
*not destination in {{pset_name}}* is a conversion of {{rpol_s_c_prefixset_opts}} set to *INVERT*  

*as-path length le* is a conversion of {{rpol_s_c_bgp_aslen_oper}} set to *frinx-openconfig-policy-types:ATTRIBUTE_LE*  
*as-path length ge* is a conversion of {{rpol_s_c_bgp_aslen_oper}} set to *frinx-openconfig-policy-types:ATTRIBUTE_GE*  
*as-path length eq* is a conversion of {{rpol_s_c_bgp_aslen_oper}} set to *frinx-openconfig-policy-types:ATTRIBUTE_EQ*  

*community match-any* is a conversion of {{rpol_s_c_bgp_comset_opts}} set to *ANY*  
*community match-every* is a conversion of {{rpol_s_c_bgp_comset_opts}} set to *ALL*  

*drop* is a conversion of {{rpol_s_a_result}} set to *REJECT_ROUTE*  
*done* is a conversion of {{rpol_s_a_result}} set to *ACCEPT_ROUTE*  
*pass* is a conversion of {{rpol_s_a_result}} set to *PASS_ROUTE*  

*set community (no-export)* is a conversion of {{rpol_s_a_bgp_well_known_comm}} set to *frinx-openconfig-bgp-types:NO_EXPORT*  
*set community (no-advertise)* is a conversion of {{rpol_s_a_bgp_well_known_comm}} set to *frinx-openconfig-bgp-types:NO_ADVERTISE*  
*set community (local-as)* is a conversion of {{rpol_s_a_bgp_well_known_comm}} set to *frinx-openconfig-bgp-types:NO_EXPORT_SUBCONFED*  

*as-path in {{aset_name}}* is a conversion of {{rpol_s_c_bgp_aspathset_opts}} set to *ANY*  
*not as-path in {{aset_name}}* is a conversion of {{rpol_s_c_bgp_aspathset_opts}} set to *INVERT*  

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
                        },
                        "actions": {
                            "frinx-openconfig-bgp-policy:bgp-actions": {
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
                            "frinx-openconfig-bgp-policy:bgp-conditions": {
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
                    },
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
                            "frinx-openconfig-bgp-policy:bgp-actions": {
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
                    },
                    {
                        "name": "statement_3",
                        "config": {
                            "name": "statement_3"
                        },
                        "conditions": {
                            "frinx-openconfig-bgp-policy:bgp-conditions": {
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
                            "frinx-openconfig-bgp-policy:bgp-actions": {
                                "config": {
                                    "set-med": 20
                                }
                            }
                        }
                    },
                    {
                        "name": "statement_4",
                        "config": {
                            "name": "statement_4"
                        },
                        "actions": {
                            "config": {
                                "policy-result": "ACCEPT_ROUTE"
                            },
                            "frinx-openconfig-bgp-policy:bgp-actions": {
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
                    },
                    {
                        "name": "statement_2",
                        "config": {
                            "name": "statement_2"
                        },
                        "conditions": {
                            "frinx-openconfig-bgp-policy:bgp-conditions": {
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
                            "frinx-openconfig-bgp-policy:bgp-actions": {
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
                    },
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
                            },
                            "frinx-openconfig-bgp-policy:bgp-conditions": {
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
                            "frinx-openconfig-bgp-policy:bgp-actions": {
                                "config": {
                                    "set-med": 2
                                }
                            }
                        }
                    },
                    {
                        "name": "statement_4",
                        "config": {
                            "name": "statement_4"
                        },
                        "actions": {
                            "config": {
                                "policy-result": "ACCEPT_ROUTE"
                            },
                            "frinx-openconfig-bgp-policy:bgp-actions": {
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

<pre>
route-policy route_policy_4
    if destination in pset_name then
        pass
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
                        "name": "1",
                        "config": {
                            "name": "1"
                        },
                        "conditions": {
                            "match-prefix-set": {
                                "config": {
                                    "match-set-options": "ANY",
                                    "prefix-set": "pset_name"
                                }
                            }
                        },
                        "actions": {
                            "config": {
                                "policy-result": "PASS_ROUTE"
                            }
                        }
                    }
                ]
            }
        }
    ]
}
```

### Junos 14.1X53-D40.8

#### CLI

<pre>
set policy-options policy-statement {{rpol_name}} term {{rpol_s_name}} from instance {{rpol_s_c_protocol_name}}
set policy-options policy-statement {{rpol_name}} term {{rpol_s_name}} then {{rpol_s_a_result}}
</pre>

<pre>
set policy-options policy-statement {{rpol_name}} term {{rpol_s_name}} from protocol {{rpol_s_c_protocol_type}}
set policy-options policy-statement {{rpol_name}} term {{rpol_s_name}} then metric {{rpol_s_a_ospf_metric}}
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
           "config": {
               "name": "IMPORT"
           },
           "name": "IMPORT",
           "statements": {
               "statement": [
                   {
                       "name": "1",
                       "config": {
                           "name": "1"
                       },
                       "conditions": {
                           "frinx-openconfig-network-instance-policy:match-protocol-instance": {
                               "config": {
                                   "protocol-name": "master"
                               }
                           }
                       },
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

<pre>
set policy-options policy-statement OUT-FIL term 1 from protocol direct
set policy-options policy-statement OUT-FIL term 1 then metric 100
set policy-options policy-statement OUT-FIL term 1 then accept
</pre>

```javascript
{
    "policy-definition": [
       {
           "name": "OUT-FIL",
           "config": {
               "name": "OUT-FIL"
           },
           "statements": {
               "statement": [
                   {
                       "name": "1",
                       "config": {
                           "name": "1"
                       },
                       "conditions": {
                           "frinx-openconfig-network-instance-policy:match-protocol-instance": {
                               "config": {
                                   "protocol-identifier": "frinx-openconfig-policy-types:DIRECTLY_CONNECTED"
                               }
                           }
                       },
                       "actions": {
                           "config": {
                               "policy-result": "ACCEPT_ROUTE"
                           },
                           "frinx-openconfig-ospf-policy:ospf-actions": {
                               "set-metric": {
                                   "config": {
                                       "metric": 100
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
