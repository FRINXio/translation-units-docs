# show ipv6 interface

## REST call

```

http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/IOS1/yang-ext:mount/openconfig-interfaces:interfaces

```

## REST response body

```

 {
    "interfaces": {
        "interface": [
            {
                "name": "GigabitEthernet1/0",
                "config": {
                    "type": "iana-if-type:ethernetCsmacd",
                    "enabled": false,
                    "name": "GigabitEthernet1/0"
                },
                "state": {
                    "type": "iana-if-type:ethernetCsmacd",
                    "enabled": false,
                    "oper-status": "DOWN",
                    "mtu": 1500,
                    "name": "GigabitEthernet1/0",
                    "admin-status": "DOWN"
                },
                "subinterfaces": {
                    "subinterface": [
                        {
                            "index": 0,
                            "openconfig-if-ip:ipv6": {
                                "addresses": {
                                    "address": [
                                        {
                                            "ip": "2003::1",
                                            "config": {
                                                "prefix-length": 63,
                                                "ip": "2003::1"
                                            }
                                        },
                                        {
                                            "ip": "FE80::C801:7FF:FE99:1C",
                                            "config": {
                                                "prefix-length": 64,
                                                "ip": "FE80::C801:7FF:FE99:1C"
                                            }
                                        }
                                    ]
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
R121#sh ipv6 int
<b><mark>GigabitEthernet1/0</b></mark> is administratively <b><mark>down</b></mark>, line protocol is <b><mark>down</b></mark>
  IPv6 is tentative, link-local address is <b><mark>FE80::C801:7FF:FE99:1C</b></mark> [TEN]
  No Virtual link-local address(es):
  Stateless address autoconfig enabled
  Global unicast address(es):
    <b><mark>2003::1</b></mark>, subnet is 2003::/<b><mark>63</b></mark> [TEN]
  Joined group address(es):
    FF02::1
  MTU is <b><mark>1500</b></mark> bytes
  ICMP error messages limited to one every 100 milliseconds
  ICMP redirects are enabled
  ICMP unreachables are sent
  ND DAD is enabled, number of DAD attempts: 1
  ND reachable time is 30000 milliseconds (using 30000)
  ND NS retransmit interval is 1000 milliseconds
</pre>



