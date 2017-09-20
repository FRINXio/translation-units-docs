# show ip vrf

## REST call

```
GET
http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/IOS1/yang-ext:mount/openconfig-network-instance:network-instances
```

## REST response body

```
{
    "network-instances": {
        "network-instance": [
            {
                "name": "default",
                "config": {
                    "name": "default",
                    "type": "openconfig-network-instance-types:L3VRF"
                },
                "interfaces": {
                    "interface": [
                        {
                            "id": "FastEthernet0/0"
                        }
                    ]
                }
            },
            {
                "name": "DEP_1",
                "config": {
                    "name": "DEP_1",
                    "type": "openconfig-network-instance-types:L3VRF"
                },
                "interfaces": {
                    "interface": [
                        {
                            "id": "GigabitEthernet1/0"
                        },
                        {
                            "id": "GigabitEthernet2/0"
                        }
                    ]
                }
            },
            {
                "name": "DEP_2",
                "config": {
                    "name": "DEP_2",
                    "type": "openconfig-network-instance-types:L3VRF"
                },
                "interfaces": {
                    "interface": [
                        {
                            "id": "GigabitEthernet3/0"
                        }
                    ]
                }
            }
        ]
    }
}
```


---

<pre>

R121#sh ip vrf              
  Name                             Default RD          Interfaces
  DEP_1                            <not set>           Gi1/0
  DEP_1                                                Gi2/0
  DEP_2                            <not set>           Gi3/0


R121#sh ip vrf interfaces 
Interface              IP-Address      VRF                              Protocol
Gi1/0                  unassigned      DEP_1                            down
Gi2/0                  unassigned      DEP_1                            down
Gi3/0                  unassigned      DEP_2                            down

</pre>
