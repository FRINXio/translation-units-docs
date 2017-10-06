# show ip interface brief

## REST call

```
http://localhost:8181/restconf/operational/network-topology:network-topology/topology/unified/node/IOSXR-unified/yang-ext:mount/openconfig-interfaces:interfaces
```

## REST response body

```
{
    "interfaces": {
        "interface": [
            {
                "name": "GigabitEthernet0/0/0/3",
                "config": {
                    "type": "iana-if-type:ethernetCsmacd",
                    "enabled": true,
                    "name": "GigabitEthernet0/0/0/3"
                },
                "state": {
                    "oper-status": "UP",
                    "mtu": 1514,
                    "name": "GigabitEthernet0/0/0/3",
                    "admin-status": "UP",
                    "type": "iana-if-type:ethernetCsmacd",
                    "enabled": true,
                    "last-change": 0,
                    "ifindex": 0
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
                "name": "GigabitEthernet0/0/0/2",
                "config": {
                    "type": "iana-if-type:ethernetCsmacd",
                    "enabled": false,
                    "name": "GigabitEthernet0/0/0/2"
                },
                "state": {
                    "oper-status": "DOWN",
                    "mtu": 1514,
                    "name": "GigabitEthernet0/0/0/2",
                    "admin-status": "DOWN",
                    "type": "iana-if-type:ethernetCsmacd",
                    "enabled": false,
                    "last-change": 0,
                    "ifindex": 0
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
                "name": "GigabitEthernet0/0/0/5",
                "config": {
                    "type": "iana-if-type:ethernetCsmacd",
                    "enabled": false,
                    "name": "GigabitEthernet0/0/0/5"
                },
                "state": {
                    "oper-status": "DOWN",
                    "mtu": 1514,
                    "name": "GigabitEthernet0/0/0/5",
                    "admin-status": "DOWN",
                    "type": "iana-if-type:ethernetCsmacd",
                    "enabled": false,
                    "last-change": 0,
                    "ifindex": 0
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
                "name": "GigabitEthernet0/0/0/1",
                "config": {
                    "type": "iana-if-type:ethernetCsmacd",
                    "enabled": false,
                    "name": "GigabitEthernet0/0/0/1"
                },
                "state": {
                    "oper-status": "DOWN",
                    "mtu": 1514,
                    "name": "GigabitEthernet0/0/0/1",
                    "admin-status": "DOWN",
                    "type": "iana-if-type:ethernetCsmacd",
                    "enabled": false,
                    "last-change": 0,
                    "ifindex": 0
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
                "name": "GigabitEthernet0/0/0/0",
                "config": {
                    "type": "iana-if-type:ethernetCsmacd",
                    "enabled": false,
                    "name": "GigabitEthernet0/0/0/0"
                },
                "state": {
                    "oper-status": "DOWN",
                    "mtu": 1514,
                    "name": "GigabitEthernet0/0/0/0",
                    "admin-status": "DOWN",
                    "type": "iana-if-type:ethernetCsmacd",
                    "enabled": false,
                    "last-change": 0,
                    "ifindex": 0
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
                "name": "MgmtEth0/0/CPU0/0",
                "config": {
                    "type": "iana-if-type:ethernetCsmacd",
                    "enabled": true,
                    "name": "MgmtEth0/0/CPU0/0"
                },
                "state": {
                    "oper-status": "UP",
                    "mtu": 1514,
                    "name": "MgmtEth0/0/CPU0/0",
                    "admin-status": "UP",
                    "type": "iana-if-type:ethernetCsmacd",
                    "enabled": true,
                    "last-change": 0,
                    "ifindex": 0
                },
                "subinterfaces": {
                    "subinterface": [
                        {
                            "index": 0,
                            "openconfig-if-ip:ipv4": {
                                "addresses": {
                                    "address": [
                                        {
                                            "ip": "192.168.1.213",
                                            "config": {
                                                "prefix-length": 24,
                                                "ip": "192.168.1.213"
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
                "name": "Loopback0",
                "config": {
                    "type": "iana-if-type:softwareLoopback",
                    "enabled": true,
                    "name": "Loopback0"
                },
                "state": {
                    "oper-status": "UP",
                    "mtu": 1500,
                    "name": "Loopback0",
                    "admin-status": "UP",
                    "type": "iana-if-type:softwareLoopback",
                    "enabled": true,
                    "last-change": 0,
                    "ifindex": 0
                },
                "subinterfaces": {
                    "subinterface": [
                        {
                            "index": 0,
                            "openconfig-if-ip:ipv4": {
                                "addresses": {
                                    "address": [
                                        {
                                            "ip": "99.0.0.3",
                                            "config": {
                                                "prefix-length": 32,
                                                "ip": "99.0.0.3"
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

```
<rpc message-id="m-7" xmlns="urn:ietf:params:xml:ns:netconf:base:1.0">
<get>
<filter xmlns:ns0="urn:ietf:params:xml:ns:netconf:base:1.0" ns0:type="subtree">
<interface-properties xmlns="http://cisco.com/ns/yang/Cisco-IOS-XR-ifmgr-oper">
<data-nodes/>
</interface-properties>
</filter>
</get>
</rpc>


rpc-reply xmlns="urn:ietf:params:xml:ns:netconf:base:1.0" message-id="m-7">
 <data>
  <interface-properties xmlns="http://cisco.com/ns/yang/Cisco-IOS-XR-ifmgr-oper">
   <data-nodes>
    <data-node>
     <data-node-name>0/0/CPU0</data-node-name>
     <locationviews>
      <locationview>
       <locationview-name>0/0/CPU0</locationview-name>
       <interfaces>
        <interface>
         <interface-name>FINT0/0/CPU0</interface-name>
         <interface>FINT0/0/CPU0</interface>
         <type>IFT_FINT_INTF</type>
         <state>im-state-up</state>
         <actual-state>im-state-up</actual-state>
         <line-state>im-state-up</line-state>
         <actual-line-state>im-state-up</actual-line-state>
         <encapsulation>fint_base</encapsulation>
         <encapsulation-type-string>FINT_BASE_CAPS</encapsulation-type-string>
         <mtu>8000</mtu>
         <sub-interface-mtu-overhead>0</sub-interface-mtu-overhead>
         <l2-transport>false</l2-transport>
         <bandwidth>0</bandwidth>
        </interface>
        <interface>
         <interface-name>GigabitEthernet0/0/0/0</interface-name>
         <interface>GigabitEthernet0/0/0/0</interface>
         <type>IFT_GETHERNET</type>
         <state>im-state-admin-down</state>
         <actual-state>im-state-admin-down</actual-state>
         <line-state>im-state-admin-down</line-state>
         <actual-line-state>im-state-admin-down</actual-line-state>
         <encapsulation>ether</encapsulation>
         <encapsulation-type-string>ARPA</encapsulation-type-string>
         <mtu>1514</mtu>
         <sub-interface-mtu-overhead>0</sub-interface-mtu-overhead>
         <l2-transport>false</l2-transport>
         <bandwidth>1000000</bandwidth>
        </interface>
        <interface>
         <interface-name>GigabitEthernet0/0/0/1</interface-name>
         <interface>GigabitEthernet0/0/0/1</interface>
         <type>IFT_GETHERNET</type>
         <state>im-state-admin-down</state>
         <actual-state>im-state-admin-down</actual-state>
         <line-state>im-state-admin-down</line-state>
         <actual-line-state>im-state-admin-down</actual-line-state>
         <encapsulation>ether</encapsulation>
         <encapsulation-type-string>ARPA</encapsulation-type-string>
         <mtu>1514</mtu>
         <sub-interface-mtu-overhead>0</sub-interface-mtu-overhead>
         <l2-transport>false</l2-transport>
         <bandwidth>1000000</bandwidth>
        </interface>
        <interface>
         <interface-name>GigabitEthernet0/0/0/2</interface-name>
         <interface>GigabitEthernet0/0/0/2</interface>
         <type>IFT_GETHERNET</type>
         <state>im-state-admin-down</state>
         <actual-state>im-state-admin-down</actual-state>
         <line-state>im-state-admin-down</line-state>
         <actual-line-state>im-state-admin-down</actual-line-state>
         <encapsulation>ether</encapsulation>
         <encapsulation-type-string>ARPA</encapsulation-type-string>
         <mtu>1514</mtu>
         <sub-interface-mtu-overhead>0</sub-interface-mtu-overhead>
         <l2-transport>false</l2-transport>
         <bandwidth>1000000</bandwidth>
        </interface>
        <interface>
         <interface-name>GigabitEthernet0/0/0/3</interface-name>
         <interface>GigabitEthernet0/0/0/3</interface>
         <type>IFT_GETHERNET</type>
         <state>im-state-up</state>
         <actual-state>im-state-up</actual-state>
         <line-state>im-state-up</line-state>
         <actual-line-state>im-state-up</actual-line-state>
         <encapsulation>ether</encapsulation>
         <encapsulation-type-string>ARPA</encapsulation-type-string>
         <mtu>1514</mtu>
         <sub-interface-mtu-overhead>0</sub-interface-mtu-overhead>
         <l2-transport>false</l2-transport>
         <bandwidth>1000000</bandwidth>
        </interface>
        <interface>
         <interface-name>GigabitEthernet0/0/0/4</interface-name>
         <interface>GigabitEthernet0/0/0/4</interface>
         <type>IFT_GETHERNET</type>
         <state>im-state-up</state>
         <actual-state>im-state-up</actual-state>
         <line-state>im-state-up</line-state>
         <actual-line-state>im-state-up</actual-line-state>
         <encapsulation>ether</encapsulation>
         <encapsulation-type-string>ARPA</encapsulation-type-string>
         <mtu>1514</mtu>
         <sub-interface-mtu-overhead>0</sub-interface-mtu-overhead>
         <l2-transport>false</l2-transport>
         <bandwidth>1000000</bandwidth>
        </interface>
        <interface>
         <interface-name>GigabitEthernet0/0/0/5</interface-name>
         <interface>GigabitEthernet0/0/0/5</interface>
         <type>IFT_GETHERNET</type>
         <state>im-state-admin-down</state>
         <actual-state>im-state-admin-down</actual-state>
         <line-state>im-state-admin-down</line-state>
         <actual-line-state>im-state-admin-down</actual-line-state>
         <encapsulation>ether</encapsulation>
         <encapsulation-type-string>ARPA</encapsulation-type-string>
         <mtu>1514</mtu>
         <sub-interface-mtu-overhead>0</sub-interface-mtu-overhead>
         <l2-transport>false</l2-transport>
         <bandwidth>1000000</bandwidth>
        </interface>
        <interface>
         <interface-name>Loopback0</interface-name>
         <interface>Loopback0</interface>
         <type>IFT_LOOPBACK</type>
         <state>im-state-up</state>
         <actual-state>im-state-up</actual-state>
         <line-state>im-state-up</line-state>
         <actual-line-state>im-state-up</actual-line-state>
         <encapsulation>loopback</encapsulation>
         <encapsulation-type-string>Loopback</encapsulation-type-string>
         <mtu>1500</mtu>
         <sub-interface-mtu-overhead>0</sub-interface-mtu-overhead>
         <l2-transport>false</l2-transport>
         <bandwidth>0</bandwidth>
        </interface>
        <interface>
         <interface-name>MgmtEth0/0/CPU0/0</interface-name>
         <interface>MgmtEth0/0/CPU0/0</interface>
         <type>IFT_ETHERNET</type>
         <state>im-state-up</state>
         <actual-state>im-state-up</actual-state>
         <line-state>im-state-up</line-state>
         <actual-line-state>im-state-up</actual-line-state>
         <encapsulation>ether</encapsulation>
         <encapsulation-type-string>ARPA</encapsulation-type-string>
         <mtu>1514</mtu>
         <sub-interface-mtu-overhead>0</sub-interface-mtu-overhead>
         <l2-transport>false</l2-transport>
         <bandwidth>1000000</bandwidth>
        </interface>
        <interface>
         <interface-name>Null0</interface-name>
         <interface>Null0</interface>
         <type>IFT_NULL</type>
         <state>im-state-up</state>
         <actual-state>im-state-up</actual-state>
         <line-state>im-state-up</line-state>
         <actual-line-state>im-state-up</actual-line-state>
         <encapsulation>null</encapsulation>
         <encapsulation-type-string>Null</encapsulation-type-string>
         <mtu>1500</mtu>
         <sub-interface-mtu-overhead>0</sub-interface-mtu-overhead>
         <l2-transport>false</l2-transport>
         <bandwidth>0</bandwidth>
        </interface>
        <interface>
         <interface-name>nV-Loopback0</interface-name>
         <interface>nV-Loopback0</interface>
         <type>IFT_NV_LOOPBACK</type>
         <state>im-state-up</state>
         <actual-state>im-state-up</actual-state>
         <line-state>im-state-up</line-state>
         <actual-line-state>im-state-up</actual-line-state>
         <encapsulation>nv_loopback</encapsulation>
         <encapsulation-type-string>nV-Loopback</encapsulation-type-string>
         <mtu>1500</mtu>
         <sub-interface-mtu-overhead>0</sub-interface-mtu-overhead>
         <l2-transport>false</l2-transport>
         <bandwidth>0</bandwidth>
        </interface>
        <interface>
         <interface-name>nV-Loopback1</interface-name>
         <interface>nV-Loopback1</interface>
         <type>IFT_NV_LOOPBACK</type>
         <state>im-state-up</state>
         <actual-state>im-state-up</actual-state>
         <line-state>im-state-up</line-state>
         <actual-line-state>im-state-up</actual-line-state>
         <encapsulation>nv_loopback</encapsulation>
         <encapsulation-type-string>nV-Loopback</encapsulation-type-string>
         <mtu>1500</mtu>
         <sub-interface-mtu-overhead>0</sub-interface-mtu-overhead>
         <l2-transport>false</l2-transport>
         <bandwidth>0</bandwidth>
        </interface>
       </interfaces>
      </locationview>
     </locationviews>
     <system-view>
      <interfaces>
       <interface>
        <interface-name>FINT0/0/CPU0</interface-name>
        <interface>FINT0/0/CPU0</interface>
        <type>IFT_FINT_INTF</type>
        <state>im-state-up</state>
        <actual-state>im-state-up</actual-state>
        <line-state>im-state-up</line-state>
        <actual-line-state>im-state-up</actual-line-state>
        <encapsulation>fint_base</encapsulation>
        <encapsulation-type-string>FINT_BASE_CAPS</encapsulation-type-string>
        <mtu>8000</mtu>
        <sub-interface-mtu-overhead>0</sub-interface-mtu-overhead>
        <l2-transport>false</l2-transport>
        <bandwidth>0</bandwidth>
       </interface>
       <interface>
        <interface-name>GigabitEthernet0/0/0/0</interface-name>
        <interface>GigabitEthernet0/0/0/0</interface>
        <type>IFT_GETHERNET</type>
        <state>im-state-admin-down</state>
        <actual-state>im-state-admin-down</actual-state>
        <line-state>im-state-admin-down</line-state>
        <actual-line-state>im-state-admin-down</actual-line-state>
        <encapsulation>ether</encapsulation>
        <encapsulation-type-string>ARPA</encapsulation-type-string>
        <mtu>1514</mtu>
        <sub-interface-mtu-overhead>0</sub-interface-mtu-overhead>
        <l2-transport>false</l2-transport>
        <bandwidth>1000000</bandwidth>
       </interface>
       <interface>
        <interface-name>GigabitEthernet0/0/0/1</interface-name>
        <interface>GigabitEthernet0/0/0/1</interface>
        <type>IFT_GETHERNET</type>
        <state>im-state-admin-down</state>
        <actual-state>im-state-admin-down</actual-state>
        <line-state>im-state-admin-down</line-state>
        <actual-line-state>im-state-admin-down</actual-line-state>
        <encapsulation>ether</encapsulation>
        <encapsulation-type-string>ARPA</encapsulation-type-string>
        <mtu>1514</mtu>
        <sub-interface-mtu-overhead>0</sub-interface-mtu-overhead>
        <l2-transport>false</l2-transport>
        <bandwidth>1000000</bandwidth>
       </interface>
       <interface>
        <interface-name>GigabitEthernet0/0/0/2</interface-name>
        <interface>GigabitEthernet0/0/0/2</interface>
        <type>IFT_GETHERNET</type>
        <state>im-state-admin-down</state>
        <actual-state>im-state-admin-down</actual-state>
        <line-state>im-state-admin-down</line-state>
        <actual-line-state>im-state-admin-down</actual-line-state>
        <encapsulation>ether</encapsulation>
        <encapsulation-type-string>ARPA</encapsulation-type-string>
        <mtu>1514</mtu>
        <sub-interface-mtu-overhead>0</sub-interface-mtu-overhead>
        <l2-transport>false</l2-transport>
        <bandwidth>1000000</bandwidth>
       </interface>
       <interface>
        <interface-name>GigabitEthernet0/0/0/3</interface-name>
        <interface>GigabitEthernet0/0/0/3</interface>
        <type>IFT_GETHERNET</type>
        <state>im-state-up</state>
        <actual-state>im-state-up</actual-state>
        <line-state>im-state-up</line-state>
        <actual-line-state>im-state-up</actual-line-state>
        <encapsulation>ether</encapsulation>
        <encapsulation-type-string>ARPA</encapsulation-type-string>
        <mtu>1514</mtu>
        <sub-interface-mtu-overhead>0</sub-interface-mtu-overhead>
        <l2-transport>false</l2-transport>
        <bandwidth>1000000</bandwidth>
       </interface>
       <interface>
        <interface-name>GigabitEthernet0/0/0/4</interface-name>
        <interface>GigabitEthernet0/0/0/4</interface>
        <type>IFT_GETHERNET</type>
        <state>im-state-up</state>
        <actual-state>im-state-up</actual-state>
        <line-state>im-state-up</line-state>
        <actual-line-state>im-state-up</actual-line-state>
        <encapsulation>ether</encapsulation>
        <encapsulation-type-string>ARPA</encapsulation-type-string>
        <mtu>1514</mtu>
        <sub-interface-mtu-overhead>0</sub-interface-mtu-overhead>
        <l2-transport>false</l2-transport>
        <bandwidth>1000000</bandwidth>
       </interface>
       <interface>
        <interface-name>GigabitEthernet0/0/0/5</interface-name>
        <interface>GigabitEthernet0/0/0/5</interface>
        <type>IFT_GETHERNET</type>
        <state>im-state-admin-down</state>
        <actual-state>im-state-admin-down</actual-state>
        <line-state>im-state-admin-down</line-state>
        <actual-line-state>im-state-admin-down</actual-line-state>
        <encapsulation>ether</encapsulation>
        <encapsulation-type-string>ARPA</encapsulation-type-string>
        <mtu>1514</mtu>
        <sub-interface-mtu-overhead>0</sub-interface-mtu-overhead>
        <l2-transport>false</l2-transport>
        <bandwidth>1000000</bandwidth>
       </interface>
       <interface>
        <interface-name>Loopback0</interface-name>
        <interface>Loopback0</interface>
        <type>IFT_LOOPBACK</type>
        <state>im-state-up</state>
        <actual-state>im-state-up</actual-state>
        <line-state>im-state-up</line-state>
        <actual-line-state>im-state-up</actual-line-state>
        <encapsulation>loopback</encapsulation>
        <encapsulation-type-string>Loopback</encapsulation-type-string>
        <mtu>1500</mtu>
        <sub-interface-mtu-overhead>0</sub-interface-mtu-overhead>
        <l2-transport>false</l2-transport>
        <bandwidth>0</bandwidth>
       </interface>
       <interface>
        <interface-name>MgmtEth0/0/CPU0/0</interface-name>
        <interface>MgmtEth0/0/CPU0/0</interface>
        <type>IFT_ETHERNET</type>
        <state>im-state-up</state>
        <actual-state>im-state-up</actual-state>
        <line-state>im-state-up</line-state>
        <actual-line-state>im-state-up</actual-line-state>
        <encapsulation>ether</encapsulation>
        <encapsulation-type-string>ARPA</encapsulation-type-string>
        <mtu>1514</mtu>
        <sub-interface-mtu-overhead>0</sub-interface-mtu-overhead>
        <l2-transport>false</l2-transport>
        <bandwidth>1000000</bandwidth>
       </interface>
       <interface>
        <interface-name>Null0</interface-name>
        <interface>Null0</interface>
        <type>IFT_NULL</type>
        <state>im-state-up</state>
        <actual-state>im-state-up</actual-state>
        <line-state>im-state-up</line-state>
        <actual-line-state>im-state-up</actual-line-state>
        <encapsulation>null</encapsulation>
        <encapsulation-type-string>Null</encapsulation-type-string>
        <mtu>1500</mtu>
        <sub-interface-mtu-overhead>0</sub-interface-mtu-overhead>
        <l2-transport>false</l2-transport>
        <bandwidth>0</bandwidth>
       </interface>
       <interface>
        <interface-name>nV-Loopback0</interface-name>
        <interface>nV-Loopback0</interface>
        <type>IFT_NV_LOOPBACK</type>
        <state>im-state-up</state>
        <actual-state>im-state-up</actual-state>
        <line-state>im-state-up</line-state>
        <actual-line-state>im-state-up</actual-line-state>
        <encapsulation>nv_loopback</encapsulation>
        <encapsulation-type-string>nV-Loopback</encapsulation-type-string>
        <mtu>1500</mtu>
        <sub-interface-mtu-overhead>0</sub-interface-mtu-overhead>
        <l2-transport>false</l2-transport>
        <bandwidth>0</bandwidth>
       </interface>
       <interface>
        <interface-name>nV-Loopback1</interface-name>
        <interface>nV-Loopback1</interface>
        <type>IFT_NV_LOOPBACK</type>
        <state>im-state-up</state>
        <actual-state>im-state-up</actual-state>
        <line-state>im-state-up</line-state>
        <actual-line-state>im-state-up</actual-line-state>
        <encapsulation>nv_loopback</encapsulation>
        <encapsulation-type-string>nV-Loopback</encapsulation-type-string>
        <mtu>1500</mtu>
        <sub-interface-mtu-overhead>0</sub-interface-mtu-overhead>
        <l2-transport>false</l2-transport>
        <bandwidth>0</bandwidth>
       </interface>
      </interfaces>
     </system-view>
    </data-node>
   </data-nodes>
  </interface-properties>
 </data>
</rpc-reply>

```