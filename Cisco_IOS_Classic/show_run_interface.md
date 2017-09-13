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



