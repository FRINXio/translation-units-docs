# OSPF metric configuration

## URL

```
openconfig-network-instance:network-instances/network-instance/<ni-name>/protocols/protocol/openconfig-policy-types:OSPF/<process-name>
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
                    "max-metric": {
                        "config": {
                            "set":true
                            "include": [ { "MAX_METRIC_INCLUDE_STUB", "AS_EXTERNAL_LSA", "SUMMARY_ASBR_LSA" } ]
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

---
<pre>
router ospf &lt;process-name&gt;
  max-metric router-lsa include-stub summary-lsa external-lsa
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [xr-unit]()

### Junos 15.1F5

#### CLI

---
<pre>
set protocols ospf overload timeout 1200
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit]()
