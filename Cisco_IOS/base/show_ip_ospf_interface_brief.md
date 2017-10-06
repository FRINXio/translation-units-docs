# show ip ospf interface brief

## REST call

```
http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-network-instance:network-instances/network-instance/<VRF-id>/protocols/protocol/openconfig-policy-types:OSPF/<OSPF-process-id>/ospfv2/areas/area/<area-id>/interfaces

```

## REST response body

```
{
    "interfaces": {
        "interface": [
            {
                "id": "Loopback99"
            }
        ]
    }
}

```


---

<pre>
R121#sh ip ospf interface brief
Interface    PID   Area            IP Address/Mask    Cost  State Nbrs F/C
<b><mark>Lo99</b></mark>          100   20              <b><mark>7.7.7.7/32</b></mark>         1     LOOP  0/0
R121#
</pre>



