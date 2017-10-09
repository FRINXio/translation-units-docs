# show ip route static

## REST call

```
http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-network-instance:network-instances/network-instance/<ni-name>/protocols/protocol/openconfig-policy-types:STATIC/default
```

## REST response body

```
 

{
   "protocol": [
      {
         "name": "default",
         "identifier": "openconfig-policy-types:STATIC",
         "config": {
            "name": "default",
            "identifier": "openconfig-policy-types:STATIC"
         },
         "static-routes": {
            "static": [
               {
                  "prefix": "10.255.1.0/24",
                  "config": {
                     "prefix": "10.255.1.0/24"
                  },
                  "next-hops": {
                     "next-hop": [
                        {
                           "index": "Null0"
                        },
                        {
                           "index": "192.168.1.5"
                        }
                     ]
                  },
                  "state": {
                     "prefix": "10.255.1.0/24"
                  }
               }
            ]
         },
         "state": {
            "name": "default",
            "identifier": "openconfig-policy-types:STATIC"
         }
      }
   ]
}


```


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
S        10.255.1.0/24 [1/0] via 192.168.1.5
                       is directly connected, Null0
      12.0.0.0/28 is subnetted, 1 subnets
S        12.255.1.0 [1/0] via 192.168.1.24

R121#
</pre>



