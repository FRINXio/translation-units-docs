# Quality of Service

## URL

```
frinx-openconfig-qos:qos
```

## OPENCONFIG YANG

```javascript
{
    "qos": {
        "config": {
            "frinx-saos-qos-extension:enabled": true
        },
        "interfaces": {
            "interface": [
                {
                    "interface-id": {{eth_ifc_name}},
                    "config": {
                        "interface-id": {{eth_ifc_name}},
                        "frinx-saos-qos-extension:enabled": true,
                        "frinx-saos-qos-extension:mode": {{mode}}
                    },
                    "input": {
                        "config": {
                            "frinx-qos-extension:service-policy": "{{qos_input_policy_name}}"
                        }
                    },
                    "output": {
                        "config": {
                            "frinx-qos-extension:service-policy": "{{qos_output_policy_name}}"
                        }
                    }
                }
            ]
        }
    }
}
```

## URL

```
frinx-openconfig-qos:qos/classifiers/classifier={{class_name}}?content=nonconfig
```

## OPENCONFIG YANG

```javascript
{
    "classifier": [
        {
            "name": "{{class_name}}",
            "config": {
                "name": "{{class_name}}"
                "frinx-qos-extension:operation": {{matching_rule}}
            },
            "terms": {
                "term": [
                    {
                        "id": "{{term_id}}",
                        "config": {
                            "id": "{{term_id}}"
                        },
                        "conditions": {
                            "frinx-qos-extension:qos-group": [{{term_c_qos_grp}}],
                            "frinx-qos-extension:precedence": [{{term_c_common_prec}}],
                            "ipv4|6": {
                                "config": {
                                    "frinx-qos-extension:precedence": "[{{term_c_ipv4_prec}}]"
                                    "frinx-qos-extension:acl-ref": "{{term_c_acl_ref}}",
                                    "frinx-qos-extension:dscp-enum": "{{term_c_dscp_enum}}"
                                }
                            },
                            "mpls": {
                                "config": {
                                    "traffic-class": ["{{term_c_tc}}"]
                                }
                            },
                            "frinx-qos-extension:multiple-cos": {
                                "cos-sets": [
                                    {
                                        "id": {{id_number_of_set}},
                                        "elements": {
                                            "inner": {{term_c_cos_inner}}, //true or false
                                            "element": [
                                                {
                                                    "id": {{term_c_cos}}
                                                }
                                            ]
                                        }
                                    }
                                ]
                            }
                        },
                        "actions": {
                            "config": {
                                "target-group": {{policy_name}}
                            },
                            "remark": {
                                "config": {
                                    "frinx-qos-extension:set-precedence": [{{term_s_common_prec}}],
                                    "frinx-qos-extension:set-qos-group": [{{term_s_qos_grp}}],
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
frinx-openconfig-qos:qos/scheduler-policies/scheduler-policy={{policy_name}}
```

## OPENCONFIG YANG


```javascript
{
    "scheduler-policy": [
        {
            "name": "{{policy_name}}",
            "config": {
                "name": "{{policy_name}}",
                "frinx-saos-qos-extension:interface-id": "{{eth_ifc_name}}"
            }
            "schedulers": {
                "scheduler": [
                    {
                        "sequence": "{{scheduler_seq}}", //internal value indicating the class-map sequence,starting with 1
                        "config": {
                            "sequence": "{{scheduler_seq}}",
                            "frinx-saos-qos-extension:type": {{scheduler_type}},
                            "frinx-saos-qos-extension:vs-name": {{vs_ni_name}},
                            "priority": "{{scheduler_strict_priority}}", // STRICT or null
                            "frinx-qos-extension:service-policy": "{{scheduler_policy_name}}",
                            "frinx-qos-extension:vrp-precedence": "{{precedence_name}}",        
                            "frinx-qos-extension:behavior": "{{behavior_name}}" 
                        },
                        "inputs": {
                            "input": [
                                {
                                    "id": "{{class_name}}",
                                    "config": {
                                        "id": "{{class_name}}",
                                        "queue": "{{class_name}}",
                                        "weight": "{{scheduler_priority}}",
                                        "frinx-qos-extension:cos": {{scheduler_cos}},
                                        "frinx-qos-extension:statistic": "{{traffic_statistics}}"
                                    }
                                }
                            ]
                        },
                        "one-rate-two-color": {
                            "config": {
                                "cir": {{1r2c_scheduler_cir}},
                                "bc": {{1r2c_scheduler_bc}},
                                "cir-pct": {{1r2c_scheduler_bw_pct}},
                                "cir-pct-remaining": {{1r2c_scheduler_bw_rem}},
                                "frinx-qos-extension:max-queue-depth-bps": {{1r2c_scheduler_max_queue_depth_bps}},
                                "frinx-qos-extension:drop-method": "{{drop_method_name}}",
                                "frinx-qos-extension:color-mode": "{{color_mode_name}}"
                            },
                            "conform-action": {
                                "config": {
                                    "frinx-qos-extension:cos-transmit": {{1r2c_conform_cos}},
                                    "frinx-qos-extension:dei-transmit": {{1r2c_conform_dei}},
                                    "frinx-qos-extension:dscp-transmit": {{1r2c_conform_dscp}},
                                    "frinx-qos-extension:qos-transmit": {{1r2c_conform_qos}},
                                    "frinx-qos-extension:transmit": {{1r2c_conform_transmit}} // true or false
                                }
                            },
                            "exceed-action": {
                                "config": {
                                    "frinx-qos-extension:cos-transmit": {{1r2c_exceed_cos}},
                                    "frinx-qos-extension:dei-transmit": {{1r2c_exceed_dei}},
                                    "frinx-qos-extension:dscp-transmit": {{1r2c_exceed_dscp}},
                                    "frinx-qos-extension:qos-transmit": {{1r2c_exceed_qos}},
                                    "frinx-qos-extension:transmit": {{1r2c_exceed_transmit}}, // true or false
                                    "drop": {{1r2c_exceed_drop}} // true or false
                                }
                            },
                            "frinx-qos-extension:yellow-action": {
                                "config": {
                                    "frinx-qos-extension:cos-transmit": {{1r2c_yellow_cos}},
                                    "frinx-qos-extension:dei-transmit": {{1r2c_yellow_dei}},
                                    "frinx-qos-extension:dscp-transmit": {{1r2c_yellow_dscp}},
                                    "frinx-qos-extension:qos-transmit": {{1r2c_yellow_qos}},
                                    "frinx-qos-extension:transmit": {{1r2c_yellow_transmit}}, // true or false
                                    "drop": {{1r2c_yellow_drop}} // true or false
                                }
                            }
                        },
                        "two-rate-three-color": {
                            "config": {
                                "cir": {{scheduler_cir}},
                                "cir-pct": {{scheduler_bw_pct}},
                                "cir-pct-remaining": {{scheduler_bw_pct_rem}},
                                "pir": {{scheduler_pir}},
                                "be": {{scheduler_be}},
                                "max-queue-depth-pct": {{scheduler_rate_pct}},
                                "frinx-qos-extension:max-queue-depth-ms": {{scheduler_max_queue_depth_ms}},
                                "frinx-saos-qos-extension:congestion-avoidance": {{scheduler_congestion}},
                                "frinx-saos-qos-extension:weight": {{scheduler_saos_weight}},
                                "frinx-qos-extension:traffic-action": "{{traffic_action_name}}" 
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

### Cisco IOS 12, 15, 16 / IOS XE 15, 16, 17

#### CLI

<pre>
interface {{eth_ifc_name}}
    service-policy input {{qos_input_policy_name}}
    service-policy output {{qos_output_policy_name}}

class-map match-any|match-all {{class_name}}
    match cos {{term_c_cos_inner}} {{term_c_cos}}
    match qos-group {{term_c_qos_grp}}
    match ip dscp {{term_c_dscp_enum}}

policy-map {{policy_name}}
    class {{class_name}}
        set cos {{scheduler_cos}}
        police cir {{1r2c_scheduler_cir}} bc {{1r2c_scheduler_bc}} conform-action {{1r2c_conform_transmit}} exceed-action {{1r2c_exceed_transmit}}
        police cir {{1r2c_scheduler_cir}} bc {{1r2c_scheduler_bc}} conform-action {{1r2c_conform_transmit}} exceed-action {{1r2c_exceed_drop}}
        police cir {{1r2c_scheduler_cir}} bc {{1r2c_scheduler_bc}} conform-action set-cos-transmit {{1r2c_conform_cos}} exceed-action set-cos-transmit {{1r2c_exceed_cos}}
        police cir {{1r2c_scheduler_cir}} bc {{1r2c_scheduler_bc}} conform-action set-dot1ad-dei-transmit {{1r2c_conform_dei}} exceed-action set-dot1ad-dei-transmit {{1r2c_exceed_dei}}
        police cir {{1r2c_scheduler_cir}} bc {{1r2c_scheduler_bc}} conform-action set-dscp-transmit {{1r2c_conform_dscp}} exceed-action set-dscp-transmit {{1r2c_exceed_dscp}}
        police cir {{1r2c_scheduler_cir}} bc {{1r2c_scheduler_bc}} conform-action set-qos-transmit {{1r2c_conform_qos}} exceed-action set-qos-transmit {{1r2c_exceed_qos}}
        priority|no priority // based on {{scheduler_strict_priority}}
        bandwidth percent {{1r2c_scheduler_bw_pct}}
        bandwidth remaining percent {{1r2c_scheduler_bw_rem}}
        shape average {{1r2c_scheduler_max_queue_depth_bps}}
        service-policy {{scheduler_policy_name}}
</pre>

#### Usage

A term marks one or more conditions depending on the class-map type.
- When class-map type: match-all, there is just one term, that MUST be called 'all'.
- When class-map type: match-any, the terms are numbered from 1 ... number_of_conditions. In this case, the {{term_id}} marks the line, where the conditions specified in conditions is written.

### Cisco IOS XR 5.3.4

#### CLI

<pre>
class-map match-any|match-all {{class_name}}
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

### Huawei NE5000E (V800R009C10SPC310)

#### CLI

---
<pre>
traffic classifier {{class_name}} operator {{matching_rule}}
 if-match dscp {{term_c_dscp_enum}}

traffic behavior {{behavior_name}}
 statistic {{traffic_statistics}}
 queue {{traffic_action_name}} bandwidth pct {{scheduler_bw_pct}}
 car cir pct {{1r2c_scheduler_bw_pct}} mode {{color_mode_name}} green pass {{1r2c_conform_transmit}} {{1r2c_conform_cos}} yellow pass {{1r2c_yellow_transmit}} {{1r2c_yellow_cos}} red pass {{1r2c_exceed_transmit}} {{1r2c_exceed_cos}}

traffic policy {{policy_name}}          
 classifier {{class_name}} behavior {{behavior_name} precedence {{precedence_name}}
</pre>
---

##### Unit

Link to github : [huawei-unit](https://github.com/FRINXio/cli-units/tree/master/huawei/qos)

### Ciena SAOS 6.14

#### CLI

<pre>
traffic-profiling enable
traffic-profiling enable port {{eth_ifc_name}}
traffic-profiling set port {{eth_ifc_name}} mode {{mode}}
traffic-profiling standard-profile create port {{eth_ifc_name}} name {{policy_name}} vs {{vsi_ni_name}} cir {{scheduler_cir}}
</pre>

*traffic-profiling enable* is a conversion of {{qos_enabled}} set to *true*  
*traffic-profiling disable* is a conversion of {{qos_enabled}} set to *false*  

{{scheduler_type}} can be *port_policy* - this issues *traffic-profiling* commands. The {{scheduler_seq}} will be always 0, there can be just one scheduler of this type.  
{{scheduler_type}} can be *queue_group_policy* - this issues *traffic-services* command. The {{scheduler_seq}} is represented by queue number.  

<pre>
traffic-services queuing egress-port-queue-group set queue {{scheduler_seq}} port {{eth_ifc_name}} eir {{scheduler_pir}} ebs {{scheduler_be}} scheduler-weight {{scheduler_saos_weight}} congestion-avoidance-profile {{scheduler_congestion}}
traffic-services queuing egress-port-queue-group set queue {{scheduler_seq}} port {{eth_ifc_name}} eir {{scheduler_pir}} scheduler-weight {{scheduler_saos_weight}} congestion-avoidance-profile {{scheduler_congestion}}
</pre>

