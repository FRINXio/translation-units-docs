# Interface policy configuration

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance/default/frinx-openconfig-policy-forwarding:policy-forwarding/interfaces/interface/{{policy_interface}}
```

## OPENCONFIG YANG

[policy-forwarding YANG model](https://github.com/FRINXio/openconfig/tree/master/policy-forwarding/src/main/yang)

[extensions to policy-forwarding YANG model](https://github.com/FRINXio/openconfig/tree/master/network-instance/src/main/yang)

```javascript
{
    "interface": [
        {
            "interface-id": {{policy_interface}},
            "config": {
                "interface-id": {{policy_interface}},
                "frinx-cisco-pf-interfaces-extension:input-service-policy": "{{input_policy}}",
                "frinx-cisco-pf-interfaces-extension:output-service-policy": "{{output_policy}}",
                "frinx-juniper-pf-interfaces-extension:scheduler-map": "{{sched_map_name}}",
                "frinx-juniper-pf-interfaces-extension:classifiers" {
                    "exp": {
                        {
                            "name": "{{exp_name}}"
                        }
                    },
                    "inet-precedence": {
                        {
                            "name": "{{inet_precedence_name}}"
                        }
                    }
                }
            }
        }
    ]
}
```

## OS Configuration Commands

### Cisco IOS XR 5.3.4

#### CLI

<pre>
interface {{policy_interface}}
 service-policy input {{input_policy}}
 service-policy output {{output_policy}}
</pre>

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/network-instance)

### Cisco IOS XR 7.0.1

#### CLI

<pre>
interface {{policy_interface}}
 service-policy input {{input_policy}}
 service-policy output {{output_policy}}
</pre>

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/unitopo-units/tree/master/xr/xr-7-network-instance-unit)

### Junos 14.1X53-D40.8

#### CLI

<pre>
set class-of-service interfaces {{policy_interface}} unit 0 classifiers inet-precedence {{inet_precedence_name}}
</pre>

##### Unit

Link to github : [junos-unit](https://github.com/FRINXio/unitopo-units/tree/master/junos/junos-14-policy-forwarding-unit)

### Junos 17.3R1.10

#### CLI

<pre>
set class-of-service interfaces {{policy_interface}} scheduler-map {{sched_map_name}}
set class-of-service interfaces {{policy_interface}} unit 0 classifiers exp {{exp_name}}
set class-of-service interfaces {{policy_interface}} unit 0 classifiers inet-precedence {{inet_precedence_name}}
</pre>

##### Unit

Link to github : [junos-unit](https://github.com/FRINXio/unitopo-units/tree/master/junos/junos-17-policy-forwarding-unit)
