# Show static routes

## REST call

```
http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/opeconfig-network-instance:network-instances/<vrf_id>/openconfig-local-routing:local-routes/static-routes/
```

## REST response body

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
        ]
    }
}

```

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
