# static routes

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance/<ni-name>/protocols/protocol/frinx-openconfig-policy-types:STATIC/<process-name>
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/local-routing/src/main/yang)

```javascript
{
    "protocol": [
        {
            "name": <process-name>,
            "identifier": "frinx-openconfig-policy-types:STATIC",
            "config": {
                "name": <process-name>,
                "identifier": "frinx-openconfig-policy-types:STATIC"
            },
            "static-routes": {
                "static": [
                    {
                        "prefix": "1.1.1.1/32"
                        "config": {
                            "prefix": "1.1.1.1/32"
                        }
                        "state": {
                            "prefix": "1.1.1.1/32"
                        }
                        "next-hops": {
                            "next-hop": [
                                {
                                     "index": "10.1.1.2"
                                     "config": {
                                        "index": "10.1.1.2"
                                        "next-hop": "10.1.1.2"
                                     }
                                     "state": {
                                        "index": "10.1.1.2"
                                        "next-hop": "10.1.1.2"
                                     }
                                }
                                {
                                     "index": "10.1.1.1 GigabitEthernet0/0/0/1"
                                     "config": {
                                        "index": "10.1.1.1 GigabitEthernet0/0/0/1"
                                        "next-hop": "10.1.1.1"
                                        "metric": 2
                                     }
                                     "state": {
                                        "index": "10.1.1.1 GigabitEthernet0/0/0/1"
                                        "next-hop": "10.1.1.1"
                                        "metric": 2
                                     }
                                     "interface-ref": {
                                        "interface" : "GigabitEthernet0/0/0/1"
                                     }
                                }
                                {
                                    "index": "GigabitEthernet0/0/0/2"
                                    "config": {
                                        "index": "GigabitEthernet0/0/0/2"
                                    }
                                    "state": {
                                        "index": "GigabitEthernet0/0/0/2"
                                    }
                                    "interface-ref": {
                                        "interface" : "GigabitEthernet0/0/0/2"
                                    }
                                }
                            ]
                        }
                    }
                    {
                        "prefix": "2001:1:1:1::/64"
                        "config": {
                            "prefix": "2001:1:1:1::/64"
                        }
                        "state": {
                            "prefix": "2001:1:1:1::/64"
                        }
                        "next-hops": {
                            "next-hop": [
                                {
                                     "index": "fe80::1 GigabitEthernet0/0/0/1"
                                     "config": {
                                        "index": "fe80::1 GigabitEthernet0/0/0/1"
                                        "next-hop": "fe80::1"
                                     }
                                     "state": {
                                        "index": "fe80::1 GigabitEthernet0/0/0/1"
                                        "next-hop": "fe80::1"
                                     }
                                     "interface-ref": {
                                        "interface" : "GigabitEthernet0/0/0/1"
                                     }
                                }
                            ]
                        }
                    }
                }
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
R121>sh ip route static
Codes: L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2
       i - IS-IS, su - IS-IS summary, L1 - IS-IS level-1, L2 - IS-IS level-2
       ia - IS-IS inter area, * - candidate default, U - per-user static route
       o - ODR, P - periodic downloaded static route, H - NHRP, l - LISP
       + - replicated route, % - next hop override

Gateway of last resort is not set

      10.0.0.0/8 is variably subnetted, 7 subnets, 2 masks
S        <b>10.255.1.0/24 [1/0] via 192.168.1.5</b>
                       is directly connected, Null0
      12.0.0.0/28 is subnetted, 1 subnets
S        <b>12.255.1.0 [1/0] via 192.168.1.24</b>

R121#
</pre>
---

##### Unit

Unit version range: 3.1.1.rc1-frinx

Link to github : [ios-unit](https://github.com/FRINXio/cli-units/tree/master/ios/local-routing)

### Cisco XR 6.1.2

#### Netconf

---
<pre>
P/0/0/CPU0:PE1#sh run router static

Mon May  6 13:10:22.244 UTC

router static

address-family ipv4 unicast
  1.1.1.1/32 10.1.1.2
  1.1.1.1/32 GigabitEthernet0/0/0/1 10.1.1.1 metric 2
!

address-family ipv6 unicast
  2001:1:1:1::/64 GigabitEthernet0/0/0/1 fe80::1
!
vrf Cust_A
  address-family ipv4 unicast
   1.1.1.1/32 GigabitEthernet0/0/0/2
  !
!
!
</pre>
---

#### Device YANG
Link to github : [xml-sample]()

##### Unit

Unit version range: 3.1.1.rc1-frinx

Link to github : [xr-unit](https://github.com/FRINXio/unitopo-units/tree/master/xr-6-lr-unit)
