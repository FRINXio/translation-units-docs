# show ip interface

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
                    "type": "iana-if-type:gigabitEthernet",
                    "enabled": true,
                    "name": "GigabitEthernet1/0"
                },
                "state": {
                    "type": "iana-if-type:gigabitEthernet",
                    "enabled": true,
                    "oper-status": "UP",
                    "mtu": 1500,
                    "name": "GigabitEthernet1/0",
                    "admin-status": "UP"
                },
                "subinterfaces": {
                    "subinterface": [
                        {
                            "index": 0,
                            "openconfig-if-ip:ipv4": {
                                "addresses": {
                                    "address": [
                                        {
                                            "ip": "10.5.5.1",
                                            "config": {
                                                "prefix-length": 24,
                                                "ip": "10.5.5.1"
                                            }
                                        }
                                    ]
                                }
                            }
                        }
                    ]
                }
            },
            {
                "name": "GigabitEthernet3/0",
                "config": {
                    "type": "iana-if-type:gigabitEthernet",
                    "enabled": false,
                    "name": "GigabitEthernet3/0"
                },
                "state": {
                    "type": "iana-if-type:gigabitEthernet",
                    "enabled": false,
                    "oper-status": "DOWN",
                    "mtu": 1500,
                    "name": "GigabitEthernet3/0",
                    "admin-status": "DOWN"
                },
                "subinterfaces": {
                    "subinterface": [
                        {
                            "index": 0
                        }
                    ]
                }
            },
            {
                "name": "GigabitEthernet2/0",
                "config": {
                    "type": "iana-if-type:gigabitEthernet",
                    "enabled": false,
                    "name": "GigabitEthernet2/0"
                },
                "state": {
                    "type": "iana-if-type:gigabitEthernet",
                    "enabled": false,
                    "oper-status": "DOWN",
                    "mtu": 1500,
                    "name": "GigabitEthernet2/0",
                    "admin-status": "DOWN"
                },
                "subinterfaces": {
                    "subinterface": [
                        {
                            "index": 0
                        }
                    ]
                }
            },
            {
                "name": "FastEthernet0/0",
                "config": {
                    "type": "iana-if-type:fastEther",
                    "enabled": true,
                    "name": "FastEthernet0/0"
                },
                "state": {
                    "type": "iana-if-type:fastEther",
                    "enabled": true,
                    "oper-status": "UP",
                    "mtu": 1500,
                    "name": "FastEthernet0/0",
                    "admin-status": "UP"
                },
                "subinterfaces": {
                    "subinterface": [
                        {
                            "index": 0,
                            "openconfig-if-ip:ipv4": {
                                "addresses": {
                                    "address": [
                                        {
                                            "ip": "192.168.56.121",
                                            "config": {
                                                "prefix-length": 24,
                                                "ip": "192.168.56.121"
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
R121#sh ip interface 
<b><mark>FastEthernet0/0</b></mark> is <b><mark>up</b></mark>, line protocol is <b><mark>up</b></mark>
  Internet address is <b><mark>192.168.56.121/24</b></mark>
  Broadcast address is 255.255.255.255
  Address determined by non-volatile memory
  MTU is <b><mark>1500</b></mark> bytes
  Helper address is not set
  Directed broadcast forwarding is disabled
  Outgoing access list is not set
  Inbound  access list is not set
  Proxy ARP is enabled
  Local Proxy ARP is disabled
  Security level is default
  Split horizon is enabled
  ICMP redirects are always sent
  ICMP unreachables are always sent
  ICMP mask replies are never sent
  IP fast switching is enabled
  IP Flow switching is disabled
  IP CEF switching is enabled
  IP CEF switching turbo vector
  IP CEF turbo switching turbo vector
  Associated unicast routing topologies:
        Topology "base", operation state is UP
  IP multicast fast switching is enabled
  IP multicast distributed fast switching is disabled
  IP route-cache flags are Fast, CEF
  Router Discovery is disabled
  IP output packet accounting is disabled
  IP access violation accounting is disabled
  TCP/IP header compression is disabled
  RTP/IP header compression is disabled
  Probe proxy name replies are disabled
  Policy routing is disabled
  Network address translation is disabled
  BGP Policy Mapping is disabled
  Input features: MCI Check
  WCCP Redirect outbound is disabled
  WCCP Redirect inbound is disabled
  WCCP Redirect exclude is disabled
GigabitEthernet1/0 is up, line protocol is up
  Internet address is 10.5.5.1/24
  Broadcast address is 255.255.255.255
  Address determined by non-volatile memory
  MTU is 1500 bytes
  Helper address is not set
  Directed broadcast forwarding is disabled
  Outgoing access list is not set
  Inbound  access list is not set
  Proxy ARP is enabled
  Local Proxy ARP is disabled
  Security level is default
  Split horizon is enabled
  ICMP redirects are always sent
  ICMP unreachables are always sent
  ICMP mask replies are never sent
  IP fast switching is enabled
  IP Flow switching is disabled
  IP CEF switching is enabled
  IP CEF switching turbo vector
  IP CEF turbo switching turbo vector
  Associated unicast routing topologies:
        Topology "base", operation state is UP
  IP multicast fast switching is enabled
  IP multicast distributed fast switching is disabled
  IP route-cache flags are Fast, CEF
  Router Discovery is disabled
  IP output packet accounting is disabled
  IP access violation accounting is disabled
  TCP/IP header compression is disabled
  RTP/IP header compression is disabled
  Probe proxy name replies are disabled
  Policy routing is disabled
  Network address translation is disabled
  BGP Policy Mapping is disabled
  Input features: MCI Check
  WCCP Redirect outbound is disabled
  WCCP Redirect inbound is disabled
  WCCP Redirect exclude is disabled
GigabitEthernet2/0 is administratively down, line protocol is down
  Internet protocol processing disabled
GigabitEthernet3/0 is administratively down, line protocol is down
  Internet protocol processing disabled
</pre>



