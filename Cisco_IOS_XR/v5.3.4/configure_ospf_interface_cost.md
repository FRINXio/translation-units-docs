# configure OSPF interface cost

## Create REST call

```
PUT
http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-network-instance:network-instance

```
## Delete REST call

```
DELETE
http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-network-instance:network-instance/
```

## REST call body (required for create only)

```
{
    "network-instances": [ 
        {
            "protocols": [
                {
                    "config": {
                        "identifier": "OSPF"
                    }
                    "ospfv-2": {
                        "global": {
                            "config": {
                                 "router-id":<router-id>
                            }
                        } 
                        "area": [
                            {
                                "config": {
                                    "identifier":<area-id>
                                }
                                "interfaces": [
                                    {
                                        {
                                            "id":<interface-id>
                                            "metric:"<cost>
                                        }
                                    }
                                ]
                            }
                        ]
                    }
                }
            }
        }
    ]
}
```


---

<pre>
router ospf &lt;router-id&gt;
 area &lt;area-id&gt;
  interface &lt;interface-id&gt;
   cost &lt;cost&gt;
</pre>




