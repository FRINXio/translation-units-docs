# OSPF interface cost configuration

## URL

```
openconfig-network-instance:network-instance/network-instance/<ni-name>/protocols/protocol/OSPF2
```

## OPENCONFIG YANG

```json
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

#### Cisco IOS XR 5.4.3

---
<pre>
router ospf &lt;process-name&gt;
 area &lt;area-id&gt;
  interface &lt;intf-id&gt;
   cost &lt;cost&gt;
</pre>
---

#### Junos

---
<pre>
set protocols ospf area &lt;area-id&gt; interface &lt;intf-id&gt; metric &lt;cost&gt;
</pre>
---

