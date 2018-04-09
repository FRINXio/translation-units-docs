# Quality of Service

## URL

```
frinx-openconfig-qos:/qos/classifiers/classifier/{{class_name}}
```

## OPENCONFIG YANG

```javascript
{
    "classifier": [
        {
            "name": "{{class_name}}",
            "config": {
                "name": "{{class_name}}"
            },
            "terms": {
                "term": [
                    {
                        "id": "{{term_id}}",
                        "config": {
                            "id": "{{term_id}}"
                        },
                        "conditions": {
                            "frinx-qos-extension:qos-group": {{term_c_qos_grp}},
                            "frinx-qos-extension:precedence": {{term_c_common_prec}},
                            "ipv4|6": {
                                "config": {
                                    "frinx-qos-extension:precedence": "{{term_c_ipv4_prec}}"
                                    "frinx-qos-extension:acl-ref": "{{term_c_acl_ref}}",
                                }
                            },
                            "mpls": {
                                "config": {
                                    "traffic-class": "{{term_c_tc}}"
                                }
                            }
                        },
                        "actions": {
                            "config": {
                                "target-group": {{policy_name}}
                            },
                            "remark": {
                                "config": {
                                    "frinx-qos-extension:set-precedence": {{term_s_common_prec}},
                                    "frinx-qos-extension:set-qos-group": {{term_s_qos_grp}},
                                    "set-mpls-tc": {{term_s_tc}}
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

## URL

```
frinx-openconfig-qos:qos/scheduler-policies/scheduler-policy/{{policy_name}}
```

## OPENCONFIG YANG


```javascript
{
    "scheduler-policy": [
        {
            "name": "{{policy_name}}",
            "config": {
                "name": "{{policy_name}}"
            }
            "schedulers": {
                "scheduler": [
                    {
                        "sequence": "{{scheduler_seq}}", //internal value indicating the class-map sequence,starting with 1
                        "config": {
                            "sequence": "{{scheduler_seq}}"
                        },
                        "inputs": {
                            "input": [
                                {
                                    "id": "{{class_name}}",
                                    "config": {
                                        "id": "{{class_name}}",
                                        "queue": "{{class_name}}",
                                        "weight": "{{scheduler_priority}}"
                                    }
                                }
                            ]
                        },
                        "one-rate-two-color": {
                            "config": {
                                "cir-pct": {{scheduler_bw_pct}},
                                "cir-pct-remaining": {{scheduler_bw_pct_rem}},
                                "max-queue-depth-pct": {{scheduler_rate_pct}},
                                "frinx-qos-extension:max-queue-depth-ms": {{scheduler_max_queue_depth_ms}}
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
class-map <match-any/match-all> {{class_name}}
    match qos-group {{term_c_qos_grp}}
    match mpls experimental topmost {{term_c_tc}}
    match precedence {{term_c_common_prec}}
    match precedence ipv4 {{term_c_ipv4_prec}}
    match access-group ipv4|6 {{term_c_acl_ref}}
end-class-map

policy-map {{policy_name}}
 class {{class_name}}
  set qos-group {{term_s_qos_grp}}
  set mpls experimental topmost {{term_s_tc}}
  set precedence {{term_s_common_prec}}
  priority level {{scheduler_priority}}
  police rate percent {{scheduler_rate_pct}}
  queue-limit {{scheduler_max_queue_depth_ms}} ms
  bandwidth percent {{scheduler_bw_pct}}
  bandwidth remaining percent {{scheduler_bw_pct_rem}}
</pre>

#### Usage

A term marks one or more conditions depending on the class-map type. 
- When class-map type: match-all, there is just one term, that MUST be called 'all'.  
- When class-map type: match-any, the terms are numbered from 1 ... number_of_conditions. In this case, the {{term_id}} marks the line, where the conditions specified in conditions is written.

Example:

<pre>
class-map match-any {{class_name}}
    match qos-group {{term_c_qos_grp}}
    match mpls experimental topmost {{term_c_tc}}
    match precedence {{term_c_common_prec}}
    match precedence ipv4 {{term_c_ipv4_prec}}
    match access-group ipv4|6 {{term_c_acl_ref}}
end-class-map
</pre>

will create 5 terms numbered from 1 to 5, where term 1 contains condition for qos-group, term 2 contains condition for mpls, etc.

Writing will occur in ascending order. Reading is the same, first condition is put into first term, etc.


