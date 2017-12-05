# Interface policy configuration

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance/<ni-name>/frinx-openconfig-policy-forwarding:policy-forwarding/interfaces/interface/<intf-id>
```

## OPENCONFIG YANG

[policy-forwarding YANG model](https://github.com/FRINXio/openconfig/tree/master/policy-forwarding/src/main/yang)

[extensions to policy-forwarding YANG model](https://github.com/FRINXio/openconfig/tree/master/network-instance/src/main/yang)

```javascript
{
    "interface": [
        {
            "interface-id": <intf-id>
            "config": {
                "interface-id": <intf-id>
                "frinx-cisco-pf-interfaces-extension:input-service-policy": <in-policy-name>
                "frinx-cisco-pf-interfaces-extension:output-service-policy": <out-policy-name>
                "frinx-juniper-pf-interfaces-extension:scheduler-map": <sched-map-name>
                "frinx-juniper-pf-interfaces-extension:classifiers" {
                    "exp": [
                        {
                            "name": <exp-name>
                        }
                    ]
                    "inet-precedence": [
                        {
                            "name": <inet-precedence-name>
                        }
                    ]
                }
            }
            "interface-ref": {
                "config": {
                    "interface": <intf-id>
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
interface &lt;intf-id&gt;
 service-policy input &lt;in-policy-name&gt;
 service-policy output &lt;out-policy-name&gt;
</pre>

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [xr-unit]()

### Junos 15.1F-6.9

#### CLI

<pre>
set class-of-service interfaces &lt;intf-id&gt; scheduler-map &lt;sched-map-name&gt;
set class-of-service interfaces &lt;intf-id&gt; unit 0 classifiers exp <exp-name>
set class-of-service interfaces &lt;intf-id&gt; unit 0 classifiers inet-precedence <inet-precedence-name>
</pre>

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit]()
