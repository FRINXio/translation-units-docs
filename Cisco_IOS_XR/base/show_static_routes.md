# show static routes

## Show REST call

```
PUT
http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-local-routing:local-routes/static-routes/

```

## REST call body (required for create only)

```
{
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
                             "index": 1
                             "config": {
                                "index": 1
                                "next-hop": "10.1.1.2"
                             }
                             "state": {
                                "index": 1
                                "next-hop": "10.1.1.2"
                             }
                        }
                        {
                             "index": 2
                             "config": {
                                "index": 2
                                "next-hop": "10.1.1.1"
                                "metric": 200
                             }
                             "state": {
                                "index": 2
                                "next-hop": "10.1.1.1"
                                "metric": 200
                             }
                             "interface-ref": {
                                "interface" : "GigabitEthernet0/0/0/1"
                             }
                        }
                        {
                            "index": 3
                            "config": {
                                "index": 3
                            }
                            "state": {
                                "index": 3
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
                             "index": 1
                             "config": {
                                "index": 1
                                "next-hop": "fe80::1"
                             }
                             "state": {
                                "index": 1
                                "next-hop": "fe80::1"
                             }
                             "interface-ref": {
                                "interface" : "GigabitEthernet0/0/0/1"
                             }
                        }
                    ]
                }
            }
        ]
    }
}

TODO: check permanent (router) vs reuse (openconfig)
TODO: figure out link from interface-ref to vrf

```

---

<pre>
P/0/0/CPU0:PE1#sh run router static

Mon May  6 13:10:22.244 UTC

router static

address-family ipv4 unicast
  1.1.1.1/32 10.1.1.2
  1.1.1.1/32 GigabitEthernet0/0/0/1 10.1.1.1 200 permanent
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
