# Show interfaces

## URL

```
openconfig-interfaces:interfaces
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/interfaces/src/main/yang)

```javascript
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


## OS Commands

### Cisco IOS Classic (15.2(4)S5) / XE (15.3(3)S2)

#### CLI

---
<pre>
R121#sh ip interface brie

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

R121#sh ip inter gigabitEthernet 1/0 | include Internet address
</pre>
---

##### Unit

Unit version range: 3.1.1.rc1-frinx

Link to github : [ios-unit](https://github.com/FRINXio/cli-units/tree/master/ios/interface)

### Cisco XR 6.1.2

#### Netconf

---
<pre>
RP/0/0/CPU0:PE3#sh int
Fri Oct  6 14:02:48.618 UTC
Loopback0 is up, line protocol is up
  Interface state transitions: 1
  Hardware is Loopback interface(s)
  Internet address is 99.0.0.3/32
  MTU 1500 bytes, BW 0 Kbit
     reliability Unknown, txload Unknown, rxload Unknown
  Encapsulation Loopback,  loopback not set,
  Last link flapped 1d04h
  Last input Unknown, output Unknown
  Last clearing of "show interface" counters Unknown
  Input/output data rate is disabled.

Null0 is up, line protocol is up
  Interface state transitions: 1
  Hardware is Null interface
  Internet address is Unknown
  MTU 1500 bytes, BW 0 Kbit
     reliability 255/255, txload Unknown, rxload Unknown
  Encapsulation Null,  loopback not set,
  Last link flapped 1d04h
  Last input never, output never
  Last clearing of "show interface" counters never
  5 minute input rate 0 bits/sec, 0 packets/sec
  5 minute output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 total input drops
     0 drops for unrecognized upper-level protocol
     Received 0 broadcast packets, 0 multicast packets
     0 packets output, 0 bytes, 0 total output drops
     Output 0 broadcast packets, 0 multicast packets

MgmtEth0/0/CPU0/0 is up, line protocol is up
  Interface state transitions: 1
  Hardware is Management Ethernet, address is 0068.e7b4.4600 (bia 0068.e7b4.4600)
  Internet address is 192.168.1.213/24
  MTU 1514 bytes, BW 1000000 Kbit (Max: 1000000 Kbit)
     reliability 255/255, txload 0/255, rxload 0/255
  Encapsulation ARPA,
  Duplex unknown, 1000Mb/s, unknown, link type is autonegotiation
  output flow control is off, input flow control is off
  Carrier delay (up) is 10 msec
  loopback not set,
  Last link flapped 1d04h
  ARP type ARPA, ARP timeout 04:00:00
  Last input 00:00:00, output 00:00:00
  Last clearing of "show interface" counters never
  5 minute input rate 247000 bits/sec, 510 packets/sec
  5 minute output rate 70000 bits/sec, 7 packets/sec
     444275 packets input, 33099533 bytes, 0 total input drops
     0 drops for unrecognized upper-level protocol
     Received 381403 broadcast packets, 28207 multicast packets
              0 runts, 0 giants, 0 throttles, 0 parity
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored, 0 abort
     48977 packets output, 56596696 bytes, 0 total output drops
     Output 1 broadcast packets, 0 multicast packets
     0 output errors, 0 underruns, 0 applique, 0 resets
     0 output buffer failures, 0 output buffers swapped out
     1 carrier transitions

GigabitEthernet0/0/0/0 is administratively down, line protocol is administratively down
  Interface state transitions: 0
  Hardware is GigabitEthernet, address is 0068.e7b4.4601 (bia 0068.e7b4.4601)
  Internet address is Unknown
  MTU 1514 bytes, BW 1000000 Kbit (Max: 1000000 Kbit)
     reliability 255/255, txload 0/255, rxload 0/255
  Encapsulation ARPA,
  Full-duplex, 1000Mb/s, unknown, link type is force-up
  output flow control is off, input flow control is off
  Carrier delay (up) is 10 msec
  loopback not set,
  Last input never, output never
  Last clearing of "show interface" counters never
  5 minute input rate 0 bits/sec, 0 packets/sec
  5 minute output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 total input drops
     0 drops for unrecognized upper-level protocol
     Received 0 broadcast packets, 0 multicast packets
              0 runts, 0 giants, 0 throttles, 0 parity
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored, 0 abort
     0 packets output, 0 bytes, 0 total output drops
     Output 0 broadcast packets, 0 multicast packets
     0 output errors, 0 underruns, 0 applique, 0 resets
     0 output buffer failures, 0 output buffers swapped out
     0 carrier transitions

GigabitEthernet0/0/0/1 is administratively down, line protocol is administratively down
  Interface state transitions: 0
  Hardware is GigabitEthernet, address is 0068.e7b4.4602 (bia 0068.e7b4.4602)
  Internet address is Unknown
  MTU 1514 bytes, BW 1000000 Kbit (Max: 1000000 Kbit)
     reliability 255/255, txload 0/255, rxload 0/255
  Encapsulation ARPA,
  Full-duplex, 1000Mb/s, unknown, link type is force-up
  output flow control is off, input flow control is off
  Carrier delay (up) is 10 msec
  loopback not set,
  Last input never, output never
  Last clearing of "show interface" counters never
  5 minute input rate 0 bits/sec, 0 packets/sec
  5 minute output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 total input drops
     0 drops for unrecognized upper-level protocol
     Received 0 broadcast packets, 0 multicast packets
              0 runts, 0 giants, 0 throttles, 0 parity
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored, 0 abort
     0 packets output, 0 bytes, 0 total output drops
     Output 0 broadcast packets, 0 multicast packets
     0 output errors, 0 underruns, 0 applique, 0 resets
     0 output buffer failures, 0 output buffers swapped out
     0 carrier transitions

GigabitEthernet0/0/0/2 is administratively down, line protocol is administratively down
  Interface state transitions: 0
  Hardware is GigabitEthernet, address is 0068.e7b4.4603 (bia 0068.e7b4.4603)
  Internet address is Unknown
  MTU 1514 bytes, BW 1000000 Kbit (Max: 1000000 Kbit)
     reliability 255/255, txload 0/255, rxload 0/255
  Encapsulation ARPA,
  Full-duplex, 1000Mb/s, unknown, link type is force-up
  output flow control is off, input flow control is off
  Carrier delay (up) is 10 msec
  loopback not set,
  Last input never, output never
  Last clearing of "show interface" counters never
  5 minute input rate 0 bits/sec, 0 packets/sec
  5 minute output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 total input drops
     0 drops for unrecognized upper-level protocol
     Received 0 broadcast packets, 0 multicast packets
              0 runts, 0 giants, 0 throttles, 0 parity
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored, 0 abort
     0 packets output, 0 bytes, 0 total output drops
     Output 0 broadcast packets, 0 multicast packets
     0 output errors, 0 underruns, 0 applique, 0 resets
     0 output buffer failures, 0 output buffers swapped out
     0 carrier transitions

GigabitEthernet0/0/0/3 is up, line protocol is up
  Interface state transitions: 1
  Hardware is GigabitEthernet, address is 0068.e7b4.4604 (bia 0068.e7b4.4604)
  Internet address is Unknown
  MTU 1514 bytes, BW 1000000 Kbit (Max: 1000000 Kbit)
     reliability 255/255, txload 0/255, rxload 0/255
  Encapsulation ARPA,
  Full-duplex, 1000Mb/s, unknown, link type is force-up
  output flow control is off, input flow control is off
  Carrier delay (up) is 10 msec
  loopback not set,
  Last link flapped 1d04h
  Last input never, output 00:00:14
  Last clearing of "show interface" counters never
  5 minute input rate 0 bits/sec, 0 packets/sec
  5 minute output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 total input drops
     0 drops for unrecognized upper-level protocol
     Received 0 broadcast packets, 0 multicast packets
              0 runts, 0 giants, 0 throttles, 0 parity
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored, 0 abort
     1709 packets output, 418705 bytes, 0 total output drops
     Output 0 broadcast packets, 1709 multicast packets
     0 output errors, 0 underruns, 0 applique, 0 resets
     0 output buffer failures, 0 output buffers swapped out
     1 carrier transitions

GigabitEthernet0/0/0/4 is up, line protocol is up
  Interface state transitions: 1
  Hardware is GigabitEthernet, address is 0068.e7b4.4605 (bia 0068.e7b4.4605)
  Internet address is Unknown
  MTU 1514 bytes, BW 1000000 Kbit (Max: 1000000 Kbit)
     reliability 255/255, txload 0/255, rxload 0/255
  Encapsulation ARPA,
  Full-duplex, 1000Mb/s, unknown, link type is force-up
  output flow control is off, input flow control is off
  Carrier delay (up) is 10 msec
  loopback not set,
  Last link flapped 1d00h
  Last input never, output never
  Last clearing of "show interface" counters never
  5 minute input rate 0 bits/sec, 0 packets/sec
  5 minute output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 total input drops
     0 drops for unrecognized upper-level protocol
     Received 0 broadcast packets, 0 multicast packets
              0 runts, 0 giants, 0 throttles, 0 parity
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored, 0 abort
     0 packets output, 0 bytes, 0 total output drops
     Output 0 broadcast packets, 0 multicast packets
     0 output errors, 0 underruns, 0 applique, 0 resets
     0 output buffer failures, 0 output buffers swapped out
     1 carrier transitions

GigabitEthernet0/0/0/5 is administratively down, line protocol is administratively down
  Interface state transitions: 0
  Hardware is GigabitEthernet, address is 0068.e7b4.4606 (bia 0068.e7b4.4606)
  Internet address is Unknown
  MTU 1514 bytes, BW 1000000 Kbit (Max: 1000000 Kbit)
     reliability 255/255, txload 0/255, rxload 0/255
  Encapsulation ARPA,
  Full-duplex, 1000Mb/s, unknown, link type is force-up
  output flow control is off, input flow control is off
  Carrier delay (up) is 10 msec
  loopback not set,
  Last input never, output never
  Last clearing of "show interface" counters never
  5 minute input rate 0 bits/sec, 0 packets/sec
  5 minute output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 total input drops
     0 drops for unrecognized upper-level protocol
     Received 0 broadcast packets, 0 multicast packets
              0 runts, 0 giants, 0 throttles, 0 parity
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored, 0 abort
     0 packets output, 0 bytes, 0 total output drops
     Output 0 broadcast packets, 0 multicast packets
     0 output errors, 0 underruns, 0 applique, 0 resets
     0 output buffer failures, 0 output buffers swapped out
     0 carrier transitions

</pre>
---

#### Device YANG
Link to github : [xml-sample](https://github.com/FRINXio/unitopo-units/blob/master/xr-6-interface-unit/src/test/resources/data_nodes.xml)

##### Unit

Unit version range: 3.1.1.rc1-frinx

Link to github : [xr-unit](https://github.com/FRINXio/unitopo-units/tree/master/xr-6-interface-unit)