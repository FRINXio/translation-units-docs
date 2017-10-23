# BGP global + neighbors

## URL

```
openconfig-network-instance:network-instances/network-instance/<ni-name>/protocols/protocol/openconfig-policy-types:BGP/<process-name>
```

## OPENCONFIG YANG

```javascript
{
    "protocol": [
        {
            "identifier": "openconfig-policy-types:BGP",
            "name": <process-name>,
            "config": {
                "name": <process-name>,
                "identifier": "openconfig-policy-types:BGP"
            },
            "bgp": {
                "global": {
                    "config": {
                        "as": <as>,
                        "router-id": <router-id>
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


## OS Commands

### Cisco IOS Classic (15.2(4)S5) / XE (15.3(3)S2)

#### CLI

---
<pre>
XE2#sh bgp summary
BGP router identifier &lt;router-id&gt;, local AS number &lt;as&gt;
BGP table version is 1, main routing table version 1

Neighbor        V           AS MsgRcvd MsgSent   TblVer  InQ OutQ Up/Down  State/PfxRcd
10.255.255.2    4        65000       0       0        1    0    0 never    Idle
10.255.255.3    4        65000       0       0        1    0    0 never    Idle
10.255.255.5    4        65000       0       0        1    0    0 never    Idle

XE2#sh bgp ipv4 unicast summ

XE2#sh bgp vpnv4 unicast all summ
</pre>
---

##### Unit

Unit version range: 3.1.1.rc1-frinx

Link to github : [ios-unit](https://github.com/FRINXio/cli-units/tree/master/ios/bgp)

### Cisco XR 6.1.2

#### Netconf

---
<pre>
RP/0/0/CPU0:XR1#show run router bgp
Thu Jun  4 17:40:46.790 UTC

router bgp &lt;as&gt; instance &lt;process-name&gt;
 bgp router-id &lt;router-id&gt;
!
</pre>
---

#### Device YANG
Link to github : [xml-sample][]

##### Unit

Unit version range: 3.1.1.rc1-frinx

Link to github : [xr-unit][]
