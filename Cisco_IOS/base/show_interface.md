# show run interface

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
                    "mtu": 1505,
                    "name": "GigabitEthernet1/0",
                    "description": "Test interface description"
                },
                "state": {
                    "oper-status": "UP",
                    "mtu": 1505,
                    "name": "GigabitEthernet1/0",
                    "description": "Test interface description",
                    "admin-status": "UP",
                    "type": "iana-if-type:gigabitEthernet",
                    "enabled": true
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
                    "enabled": true,
                    "name": "GigabitEthernet3/0"
                },
                "state": {
                    "type": "iana-if-type:gigabitEthernet",
                    "enabled": true,
                    "oper-status": "UP",
                    "mtu": 1500,
                    "name": "GigabitEthernet3/0",
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
                                            "ip": "8.8.8.1",
                                            "config": {
                                                "prefix-length": 24,
                                                "ip": "8.8.8.1"
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
                "name": "Loopback1",
                "config": {
                    "type": "iana-if-type:softwareLoopback",
                    "enabled": true,
                    "name": "Loopback1"
                },
                "state": {
                    "type": "iana-if-type:softwareLoopback",
                    "enabled": true,
                    "oper-status": "UP",
                    "mtu": 1514,
                    "name": "Loopback1",
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
                                            "ip": "7.7.7.7",
                                            "config": {
                                                "prefix-length": 32,
                                                "ip": "7.7.7.7"
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
            },
            {
                "name": "Loopback2",
                "config": {
                    "type": "iana-if-type:softwareLoopback",
                    "enabled": true,
                    "name": "Loopback2"
                },
                "state": {
                    "type": "iana-if-type:softwareLoopback",
                    "enabled": true,
                    "oper-status": "UP",
                    "mtu": 1514,
                    "name": "Loopback2",
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
                                            "ip": "9.9.9.9",
                                            "config": {
                                                "prefix-length": 32,
                                                "ip": "9.9.9.9"
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
R121#
R121#sh interfaces gigabitEthernet 1/0
GigabitEthernet1/0 is up, line protocol is up 
  Hardware is 82543, address is ca01.07b0.001c (bia ca01.07b0.001c)
  Description: Test interface description
  Internet address is <b><mark>10.5.5.1</b></mark>/<b><mark>24</b></mark>
  MTU 1505 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive set (10 sec)
  Full Duplex, 1000Mbps, link type is auto, media type is SX
  output flow-control is unsupported, input flow-control is unsupported
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input never, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/75/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  5 minute input rate 0 bits/sec, 0 packets/sec
  5 minute output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles 
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     6453 packets output, 650162 bytes, 0 underruns
     0 output errors, 0 collisions, 267 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
R121#
</pre>



