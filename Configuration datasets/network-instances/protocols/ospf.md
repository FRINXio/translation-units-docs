# Open Shortest Path First (OSPF)

## URL

```
openconfig-network-instance:network-instance/network-instance/<ni-name>/protocols/protocol/OSPF2/<process-name>
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/ospf/src/main/yang)

```javascript
{
    "protocol": [
        {
            "name": <process-name>,
            "identifier": "openconfig-policy-types:OSPF",
            "config": {
                "name": <process-name>,
                "identifier": "openconfig-policy-types:OSPF"
            }
            "ospfv2": {
                "global": {
                    "timers": {
                        "max-metric": {
                            "config": {
                                "set": <true|false>,
                                "timeout": <timeout>,
                                "include": [ 
                                    "openconfig-ospf-types:MAX_METRIC_INCLUDE_STUB", 
                                    "openconfig-ospf-types:MAX_METRIC_INCLUDE_TYPE2_EXTERNAL", 
                                    "frinx-cisco-ospf-extension:MAX_METRIC_SUMMARY_LSA" 
                                ]
                            }
                        }
                    }
                },
                "areas": {
                    "area": [
                        {
                            "identifier": <area-id>,
                            "config": {
                                "identifier": <area-id>
                            },
                            "interfaces": {
                                "interface": [
                                    {
                                        "id": "<intf-id>",
                                        "config": {
                                            "metric": <cost>
                                        },
                                        "interface-ref": {
                                            "config": {
                                                "interface": <intf-id>
                                            }
                                        }
                                    }
                                ]
                            }
                        }
                    ]
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
router ospf &lt;process-name&gt;
 max-metric router-lsa on-startup &lt;timeout&gt; include-stub summary-lsa external-lsa
 area &lt;area-id&gt;
  interface &lt;intf-id&gt;
   cost &lt;cost&gt;
</pre>

##### Unit

Unit version range: 3.1.1.rc4

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/ospf)

### Cisco IOS Classic (IOSv 15.6(2)T)

#### CLI

<pre>
interface &lt;intf-id&gt;
 ip ospf &lt;process-name&gt; area &lt;area-id&gt;
 ip ospf cost &lt;cost&gt;
 
// TODO add max-metric if possible
</pre>

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : 

### Junos 15.1F-6.9

#### CLI

<pre>
set protocols ospf overload timeout &lt;timeout&gt;
set protocols ospf area &lt;area-id&gt; interface &lt;intf-id&gt; metric &lt;cost&gt;
</pre>

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit]()
