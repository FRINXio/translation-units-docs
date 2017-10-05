# Show router ospf type, ID, interfaces

## REST call

```
http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-network-instance:network-instance/network-instance/<ni-name>/protocols/protocol/OSPF2/<process-name>
```

## REST response body

```
{
    	"name": <process-name>
        "config": {
            "identifier": "OSPF2"
            "name": <process-name>
        }
        "state": {
            "identifier": "OSPF2"
            "name": <process-name>
        }
        "ospfv-2": {
            "global": {
                "config": {
                     "router-id":<router-id>
                }
                "state": {
                     "router-id":<router-id>
                }
            }
            "areas": {
                "area": [
                    {
                        "identifier": <area-id>
                        "config": {
                            "identifier":<area-id>
                        }
                        "state": {
                            "identifier":<area-id>
                        }
                        "interfaces": {
                            "interface": [
                                {
                                    "id": <intf-id>
                                    "config": {
                                       "id": <intf-id>
                                    }
                                    "state": {
                                       "id": <intf-id>
                                    }
                                }
                            ]
                        }
                    }
                ]
            }
        }
    }
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
