# show ip route static

## REST call

```
GET
http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-local-routing:local-routes/static-routes/
```

## REST response body

```
{
    "static-routes": {
        "static": [
            {
                "prefix": "10.10.2.0/24",
                "config": {
                    "prefix": "10.10.2.0/24"
                },
                "state": {
                    "prefix": "10.10.2.0/24"
                },
                "next-hops": {
                    "next-hop": [
                        {
                            "index": "10.10.1.1"
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
R121#sh ip route 
Codes: L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2
       i - IS-IS, su - IS-IS summary, L1 - IS-IS level-1, L2 - IS-IS level-2
       ia - IS-IS inter area, * - candidate default, U - per-user static route
       o - ODR, P - periodic downloaded static route, H - NHRP, l - LISP
       + - replicated route, % - next hop override

Gateway of last resort is not set

      10.0.0.0/8 is variably subnetted, 3 subnets, 2 masks
C        10.10.1.0/24 is directly connected, FastEthernet0/0
L        10.10.1.2/32 is directly connected, FastEthernet0/0
S        <b><mark>10.10.2.0/24</mark></b> [1/0] via <b><mark>10.10.1.1</mark></b>
      192.168.56.0/24 is variably subnetted, 2 subnets, 2 masks
C        192.168.56.0/24 is directly connected, GigabitEthernet1/0
L        192.168.56.121/32 is directly connected, GigabitEthernet1/0
R121#
</pre>



