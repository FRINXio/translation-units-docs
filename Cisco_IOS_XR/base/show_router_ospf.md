# Show router ospf type, ID, interfaces

## REST call

```
http://localhost:8181/restconf/operational/network-topology:network-topology/topology/unified/node/<node-id>/yang-ext:mount/openconfig-network-instance:network-instances/network-instance/<ni-name>/protocols/protocol/openconfig-policy-types:OSPF/<process-name>
```

## REST response body

```
{
    "protocol": [
        {
            "name": <process-name>,
            "identifier": "openconfig-policy-types:OSPF",
            "config": {
                "name": <process-name>,
                "identifier": "openconfig-policy-types:OSPF"
            },
            "state": {
                "name": <process-name>,
                "identifier": "openconfig-policy-types:OSPF"
            },
            "ospfv2": {
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
                                        "id": <intf-id>
                                        "config": {
                                            "id": <intf-id>
                                        },
                                        "state": {
                                            "id": <intf-id>
                                        }
                                    }
                                ]
                            },
                            "state": {
                                "identifier": <area-id>
                            }
                        }
                    ]
                }
            }
        }
    ]
}
```


---

<pre>
RP/0/0/CPU0:XR1#show run router ospf
Thu Jun  4 17:40:46.790 UTC
router ospf &lt;process-name&gt;
 router-id &lt;router-id&gt;
 address-family ipv4 unicast
 area &lt;area-id&gt;
  interface &lt;intf-id&gt;
  !
 !
!
</pre>

---
