# show ip bgp summary

## REST call

```
http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-network-instance:network-instances/network-instance/default/protocols/protocol/openconfig-policy-types:BGP/default
```

## REST response body

```
{
    "protocol": [
        {
            "identifier": "openconfig-policy-types:BGP",
            "name": "default",
            "config": {
                "name": "default",
                "identifier": "openconfig-policy-types:BGP"
            },
            "bgp": {
                "global": {
                    "config": {
                        "as": 65000,
                        "router-id": "99.99.99.99"
                    }
                },
                "neighbors": {
                    "neighbor": [
                        {
                            "neighbor-address": "10.255.255.5",
                            "state": {
                                "session-state": "IDLE"
                            },
                            "afi-safis": {
                                "afi-safi": [
                                    {
                                        "afi-safi-name": "openconfig-bgp-types:IPV4_UNICAST"
                                    }
                                ]
                            }
                        },
                        {
                            "neighbor-address": "10.255.255.2",
                            "state": {
                                "session-state": "IDLE"
                            },
                            "afi-safis": {
                                "afi-safi": [
                                    {
                                        "afi-safi-name": "openconfig-bgp-types:IPV4_UNICAST"
                                    }
                                ]
                            }
                        },
                        {
                            "neighbor-address": "10.255.255.3",
                            "state": {
                                "session-state": "IDLE"
                            },
                            "afi-safis": {
                                "afi-safi": [
                                    {
                                        "afi-safi-name": "openconfig-bgp-types:IPV4_UNICAST"
                                    }
                                ]
                            }
                        }
                    ]
                }
            },
            "state": {
                "name": "default",
                "identifier": "openconfig-policy-types:BGP"
            }
        }
    ]
}
```


---

<pre>
XE2#sh ip bgp summary
BGP router identifier 99.99.99.99, local AS number 65000
BGP table version is 1, main routing table version 1

Neighbor        V           AS MsgRcvd MsgSent   TblVer  InQ OutQ Up/Down  State/PfxRcd
10.255.255.2    4        65000       0       0        1    0    0 never    Idle
10.255.255.3    4        65000       0       0        1    0    0 never    Idle
10.255.255.5    4        65000       0       0        1    0    0 never    Idle
</pre>

   
