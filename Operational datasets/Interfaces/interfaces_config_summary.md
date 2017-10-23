# Interface running configuration

## URL

```
openconfig-interfaces:interfaces
```

## OPENCONFIG YANG

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

## OS Commands

### Cisco IOS Classic (15.2(4)S5) / XE (15.3(3)S2)

#### CLI

---
<pre>
R121#sh run interface gigabitEthernet 1/0
Building configuration...

Current configuration : 139 bytes
!
interface GigabitEthernet1/0
 description <b><mark>Test interface description</b></mark>
 mtu <b><mark>1505</b></mark>
 ip address 10.5.5.1 255.255.255.0
 negotiation auto
end

R121#
R121#sh run interface gigabitEthernet 2/0
Building configuration...

Current configuration : 217 bytes
!
interface GigabitEthernet2/0
 no ip address
 <b><mark>shutdown</b></mark>
 negotiation auto
end

R121#
</pre>
---

##### Unit

Unit version range: 3.1.1.rc1-frinx

Link to github : [ios-unit][https://github.com/FRINXio/cli-units/tree/master/ios/interface]

### Cisco XR 6.1.2

#### Netconf

---
<pre>
RP/0/0/CPU0:PE3#sh run interface
Fri Oct  6 14:02:10.020 UTC
interface Loopback0
 ipv4 address 99.0.0.3 255.255.255.255
!
interface MgmtEth0/0/CPU0/0
 ipv4 address 192.168.1.213 255.255.255.0
!
interface GigabitEthernet0/0/0/0
 shutdown
!
interface GigabitEthernet0/0/0/1
 shutdown
!
interface GigabitEthernet0/0/0/2
 shutdown
!
interface GigabitEthernet0/0/0/3
 cdp
!
interface GigabitEthernet0/0/0/5
 shutdown
!
</pre>
---

#### Device YANG
Link to github : [xml-sample][]

##### Unit

Unit version range: 3.1.1.rc1-frinx

Link to github : [xr-unit][]


