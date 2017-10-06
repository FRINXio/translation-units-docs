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
                            },
                            "openconfig-if-ip:ipv6": {
                                "addresses": {
                                    "address": [
                                        {
                                            "ip": "fe80::260:3eff:fe11:6770",
                                            "config": {
                                                "prefix-length": 64,
                                                "ip": "fe80::260:3eff:fe11:6770"
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
RP/0/0/CPU0:PE3#sh ipv6 int
Fri Oct  6 14:08:42.693 UTC
Loopback0 is Up, ipv6 protocol is Up, Vrfid is default (0x60000000)
  IPv6 is enabled, link-local address is fe80::260:3eff:fe11:6770 
  No global unicast address is configured
  Joined group address(es): ff02::1:ff11:6770 ff02::2 ff02::1
  MTU is 1500 (1500 is available to IPv6)
  ICMP redirects are disabled
  ICMP unreachables are always on
  ND DAD is disabled, number of DAD attempts 0
  ND reachable time is 0 milliseconds
  ND cache entry limit is 0
  ND advertised retransmit interval is 0 milliseconds
  Hosts use stateless autoconfig for addresses.
  Outgoing access list is not set
  Inbound  common access list is not set, access list is not set
  Table Id is 0xe0800000
  Complete protocol adjacency: 0
  Complete glean adjacency: 0
  Incomplete protocol adjacency: 0
  Incomplete glean adjacency: 0
  Dropped protocol request: 0
  Dropped glean request: 0
MgmtEth0/0/CPU0/0 is Up, ipv6 protocol is Up, Vrfid is default (0x60000000)
  IPv6 is disabled, link-local address unassigned
  No global unicast address is configured
GigabitEthernet0/0/0/0 is Shutdown, ipv6 protocol is Down, Vrfid is default (0x60000000)
  IPv6 is disabled, link-local address unassigned
  No global unicast address is configured
GigabitEthernet0/0/0/1 is Shutdown, ipv6 protocol is Down, Vrfid is default (0x60000000)
  IPv6 is disabled, link-local address unassigned
  No global unicast address is configured
GigabitEthernet0/0/0/2 is Shutdown, ipv6 protocol is Down, Vrfid is default (0x60000000)
  IPv6 is disabled, link-local address unassigned
  No global unicast address is configured
GigabitEthernet0/0/0/3 is Up, ipv6 protocol is Up, Vrfid is default (0x60000000)
  IPv6 is disabled, link-local address unassigned
  No global unicast address is configured
GigabitEthernet0/0/0/4 is Up, ipv6 protocol is Up, Vrfid is default (0x60000000)
  IPv6 is disabled, link-local address unassigned
  No global unicast address is configured
GigabitEthernet0/0/0/5 is Shutdown, ipv6 protocol is Down, Vrfid is default (0x60000000)
  IPv6 is disabled, link-local address unassigned
  No global unicast address is configured


</pre>

---

```
<rpc message-id="m-6" xmlns="urn:ietf:params:xml:ns:netconf:base:1.0">
<get>
<filter xmlns:ns0="urn:ietf:params:xml:ns:netconf:base:1.0" ns0:type="subtree">
<interface-configurations xmlns="http://cisco.com/ns/yang/Cisco-IOS-XR-ifmgr-cfg"/>
</filter>
</get>
</rpc>


<rpc-reply xmlns="urn:ietf:params:xml:ns:netconf:base:1.0" message-id="m-11">
 <data>
  <interface-configurations xmlns="http://cisco.com/ns/yang/Cisco-IOS-XR-ifmgr-cfg">
   <interface-configuration>
    <active>act</active>
    <interface-name>Loopback0</interface-name>
    <interface-virtual/>
    <ipv4-network xmlns="http://cisco.com/ns/yang/Cisco-IOS-XR-ipv4-io-cfg">
     <addresses>
      <primary>
       <address>99.0.0.3</address>
       <netmask>255.255.255.255</netmask>
      </primary>
     </addresses>
    </ipv4-network>
    <ipv6-network xmlns="http://cisco.com/ns/yang/Cisco-IOS-XR-ipv6-ma-cfg">
     <addresses>
      <link-local-address>
       <address>fe80::260:3eff:fe11:6770</address>
       <zone>0</zone>
      </link-local-address>
     </addresses>
    </ipv6-network>
   </interface-configuration>
   <interface-configuration>
    <active>act</active>
    <interface-name>MgmtEth0/0/CPU0/0</interface-name>
    <ipv4-network xmlns="http://cisco.com/ns/yang/Cisco-IOS-XR-ipv4-io-cfg">
     <addresses>
      <primary>
       <address>192.168.1.213</address>
       <netmask>255.255.255.0</netmask>
      </primary>
     </addresses>
    </ipv4-network>
   </interface-configuration>
   <interface-configuration>
    <active>act</active>
    <interface-name>GigabitEthernet0/0/0/0</interface-name>
    <shutdown/>
   </interface-configuration>
   <interface-configuration>
    <active>act</active>
    <interface-name>GigabitEthernet0/0/0/1</interface-name>
    <shutdown/>
   </interface-configuration>
   <interface-configuration>
    <active>act</active>
    <interface-name>GigabitEthernet0/0/0/2</interface-name>
    <shutdown/>
   </interface-configuration>
   <interface-configuration>
    <active>act</active>
    <interface-name>GigabitEthernet0/0/0/3</interface-name>
    <cdp xmlns="http://cisco.com/ns/yang/Cisco-IOS-XR-cdp-cfg">
     <enable/>
    </cdp>
   </interface-configuration>
   <interface-configuration>
    <active>act</active>
    <interface-name>GigabitEthernet0/0/0/5</interface-name>
    <shutdown/>
   </interface-configuration>
  </interface-configurations>
 </data>
</rpc-reply>

```