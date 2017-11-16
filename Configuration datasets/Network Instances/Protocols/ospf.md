# OSPF interface cost configuration

## URL

```
openconfig-network-instance:network-instance/network-instance/<ni-name>/protocols/protocol/OSPF2
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
            "global": {
                "timers": {
                    "max-metric": {
                        "config": {
                            "set": <true|false>
                            "timeout": <timeout>
                            "include": [ { "MAX_METRIC_INCLUDE_STUB", "AS_EXTERNAL_LSA", "SUMMARY_ASBR_LSA" } ]
                        }
                    }
                }
            }
            "ospfv2": {
                "areas": {
                    "area": [
                        {
                            "identifier": <area-id>,
                            "config": {
                                "identifier": <area-id>
                            },
                            "interfaces": [
                                {
                                    "id":<intf-id>
                                    "config": {
                                        "metric:"<cost>
                                    }
                                    "interface-ref": {
                                        "config": {
                                            "interface": <intf-id>
                                        }
                                    }
                                }
                            ]
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

Unit version range: NOT IMPLEMENTED

Link to github : [xr-unit]()

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
