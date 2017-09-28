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
  <b><mark>DEP_1</b></mark>                            <not set>           <b><mark>Gi1/0</b></mark>
  <b><mark>DEP_1</b></mark>                                                <b><mark>Gi2/0</b></mark>
  <b><mark>DEP_2</b></mark>                            <not set>           <b><mark>Gi3/0</b></mark>


R121#sh ip vrf interfaces 
Interface              IP-Address      VRF                              Protocol
<b><mark>Gi1/0</b></mark>                  unassigned      <b><mark>DEP_1</b></mark>                            down
<b><mark>Gi2/0</b></mark>                  unassigned      <b><mark>DEP_1</b></mark>                            down
<b><mark>Gi3/0</b></mark>                  unassigned      <b><mark>DEP_2</b></mark>                            down

</pre>
