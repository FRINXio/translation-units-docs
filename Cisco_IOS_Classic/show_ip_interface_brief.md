# show ip interface brief

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
                    "enabled": true,
                    "name": "GigabitEthernet2/0"
                },
                "state": {
                    "type": "iana-if-type:gigabitEthernet",
                    "enabled": true,
                    "oper-status": "UP",
                    "mtu": 1500,
                    "name": "GigabitEthernet2/0",
                    "admin-status": "UP"
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
R121#show ip interface brief
Interface              IP-Address      OK? Method Status                Protocol
<b><mark>FastEthernet0/0</b></mark>        192.168.56.121  YES NVRAM  up                    up      
<b><mark>GigabitEthernet1/0</b></mark>     10.5.5.1        YES NVRAM  up                    up      
<b><mark>GigabitEthernet2/0</b></mark>     unassigned      YES NVRAM  up                    up      
<b><mark>GigabitEthernet3/0</b></mark>     8.8.8.1         YES NVRAM  up                    up      
<b><mark>Loopback1</b></mark>              7.7.7.7         YES NVRAM  up                    up      
<b><mark>Loopback2</b></mark>             9.9.9.9         YES NVRAM  up                    up      
R121#

</pre>



