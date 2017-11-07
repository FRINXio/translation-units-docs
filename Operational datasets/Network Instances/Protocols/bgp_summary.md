# BGP global + neighbors

## URL

```
openconfig-network-instance:network-instances/network-instance/<ni-name>/protocols/protocol/openconfig-policy-types:BGP/<process-name>
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/bgp)

```javascript
{
    "protocol": [
        {
            "identifier": "openconfig-policy-types:BGP",
            "name": "<process-name>",
            "config": {
                "name": "<process-name>",
                "identifier": "openconfig-policy-types:BGP"
            },
            "bgp": {
                "global": {
                    "config": {
                        "as": "<as>",
                        "router-id": "<router-id>"
                    }
                    "state": {
                        "as": "<as>",
                        "router-id": "<router-id>"
                    }
                },
                "neighbors": {
                    "neighbor": [
                        {
                            "neighbor-address": "<neighbor3>",
                            "config": {
                                "neighbor-address": "<neighbor3>"
                            },
                            "state": {
                                "session-state": "<state3>"
                            },
                            "afi-safis": {
                                "afi-safi": [
                                    {
                                        "afi-safi-name": "openconfig-bgp-types:IPV4_UNICAST"
                                        "config": {
                                            "afi-safi-name": "openconfig-bgp-types:IPV4_UNICAST"
                                        }
                                    }
                                ]
                            }
                        },
                        {
                            "neighbor-address": "<neighbor1>",
                            "config": {
                                "neighbor-address": "<neighbor1>"
                            },
                            "state": {
                                "session-state": "<state1>"
                            },
                            "afi-safis": {
                                "afi-safi": [
                                    {
                                        "afi-safi-name": "openconfig-bgp-types:IPV4_UNICAST"
                                        "config": {
                                            "afi-safi-name": "openconfig-bgp-types:IPV4_UNICAST"
                                        }
                                    }
                                ]
                            }
                        },
                        {
                            "neighbor-address": "<neighbor2>",
                            "config": {
                                "neighbor-address": "<neighbor2>"
                            },
                            "state": {
                                "session-state": "<state2>"
                            },
                            "afi-safis": {
                                "afi-safi": [
                                    {
                                        "afi-safi-name": "openconfig-bgp-types:IPV4_UNICAST"
                                        "config": {
                                            "afi-safi-name": "openconfig-bgp-types:IPV4_UNICAST"
                                        }
                                    },
                                    {
                                        "afi-safi-name": "openconfig-bgp-types:L3VPN_IPV4_UNICAST",
                                        "config": {
                                            "afi-safi-name": "openconfig-bgp-types:L3VPN_IPV4_UNICAST"
                                        },
                                        "state": {
                                            "prefixes": {
                                                "received": <prefs>
                                            }
                                        }
                                    }
                                ]
                            }
                        }
                    ]
                }
            },
            "state": {
                "name": "<process-name>",
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
XE2#show bgp all summary
For address family: IPv4 Unicast
BGP router identifier &lt;router-id&gt;, local AS number &lt;as&gt;
BGP table version is 2, main routing table version 2
1 network entries using 144 bytes of memory
1 path entries using 80 bytes of memory
1/1 BGP path/bestpath attribute entries using 136 bytes of memory
0 BGP route-map cache entries using 0 bytes of memory
0 BGP filter-list cache entries using 0 bytes of memory
BGP using 360 total bytes of memory
BGP activity 1/0 prefixes, 1/0 paths, scan interval 60 secs

Neighbor        V           AS MsgRcvd MsgSent   TblVer  InQ OutQ Up/Down  State/PfxRcd
&lt;neighbor1&gt;    4        65000       0       0        1    0    0 6d04h    &lt;state1&gt;
&lt;neighbor2&gt;    4        65000       0       0        1    0    0 never    &lt;state2&gt;
&lt;neighbor3&gt;    4        65000       0       0        1    0    0 never    &lt;state3&gt;

For address family: VPNv4 Unicast
BGP router identifier &lt;router-id&gt;, local AS number &lt;as&gt;
BGP table version is 1, main routing table version 1

Neighbor        V           AS MsgRcvd MsgSent   TblVer  InQ OutQ Up/Down  State/PfxRcd
&lt;prefix2&gt;    4        65000   11217   11215        1    0    0 1w0d            &lt;prefs&gt;


XE2#show bgp neighbor &lt;neighbor3&gt; | section family
For address family: IPv4 Unicast
  BGP table version 2, neighbor version 1/2
  Output queue size : 0
  Index 0, Advertise bit 0
  Slow-peer detection is disabled
  Slow-peer split-update-group dynamic is disabled
                                 Sent       Rcvd
  Prefix activity:               ----       ----
    Prefixes Current:               0          0
    Prefixes Total:                 0          0
    Implicit Withdraw:              0          0
    Explicit Withdraw:              0          0
    Used as bestpath:             n/a          0
    Used as multipath:            n/a          0

                                   Outbound    Inbound
  Local Policy Denied Prefixes:    --------    -------
    Total:                                0          0
  Number of NLRIs in the update sent: max 0, min 0
  Last detected as dynamic slow peer: never
  Dynamic slow peer recovered: never
  Refresh Epoch: 1
  Last Sent Refresh Start-of-rib: never
  Last Sent Refresh End-of-rib: never
  Last Received Refresh Start-of-rib: never
  Last Received Refresh End-of-rib: never


XE2#show bgp ipv4 unicast summary | section &lt;neighbor3&gt;
&lt;neighbor3&gt;   4        65000       0       0        1    0    0 never    &lt;state3&gt;

XE2#show bgp vpnv4 unicast all summary | section &lt;neighbor2&gt;
&lt;neighbor2&gt;    4        65000   11220   11219        1    0    0 1w0d            &lt;prefs&gt
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
Link to github : [xml-sample](https://github.com/FRINXio/unitopo-units/tree/master/xr-6-bgp-unit/src/test/resources/bgp-oper.xml)

##### Unit

Unit version range: 3.1.1.rc1-frinx

Link to github : [xr-unit](https://github.com/FRINXio/unitopo-units/tree/master/xr-6-bgp-unit)
