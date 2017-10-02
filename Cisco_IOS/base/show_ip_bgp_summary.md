# show ip bgp summary

## REST call

```
GET
http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-network-instance:network-instances
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
                            "id": "GigabitEthernet4/0"
                        },
                        {
                            "id": "FastEthernet0/0"
                        },
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
                "name": "vpn1",
                "config": {
                    "name": "vpn1",
                    "type": "openconfig-network-instance-types:L3VRF"
                },
                "interfaces": {
                    "interface": [
                        {
                            "id": "GigabitEthernet3/0"
                        }
                    ]
                },
                "protocols": {
                    "protocol": [
                        {
                            "identifier": "openconfig-policy-types:BGP",
                            "name": "vpn1",
                            "bgp": {
                                "global": {
                                    "config": {
                                        "as": 45000,
                                        "router-id": "172.17.1.99"
                                    }
                                }
                            }
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
R254#sh ip bgp summary

BGP router identifier <b><mark>172.17.1.99</mark></b>, local AS number <b><mark>45000</mark></b>
BGP table version is 3, main routing table version 3
2 network entries using 288 bytes of memory
2 path entries using 160 bytes of memory
2/2 BGP path/bestpath attribute entries using 272 bytes of memory
2 BGP AS-PATH entries using 48 bytes of memory
1 BGP extended community entries using 24 bytes of memory
0 BGP route-map cache entries using 0 bytes of memory
0 BGP filter-list cache entries using 0 bytes of memory
BGP using 792 total bytes of memory
BGP activity 3/0 prefixes, 3/0 paths, scan interval 60 secs

Neighbor        V           AS MsgRcvd MsgSent   TblVer  InQ OutQ Up/Down  State/PfxRcd
192.168.1.2     4        40000      28      29        3    0    0 00:15:37        1

</pre>

   