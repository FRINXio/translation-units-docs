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
RP/0/0/CPU0:PE3#sh ip inter brie
Fri Oct  6 13:51:23.435 UTC

Interface                      IP-Address      Status          Protocol Vrf-Name
Loopback0                      99.0.0.3        Up              Up       default 
MgmtEth0/0/CPU0/0              192.168.1.213   Up              Up       default 
GigabitEthernet0/0/0/0         unassigned      Shutdown        Down     default 
GigabitEthernet0/0/0/1         unassigned      Shutdown        Down     default 
GigabitEthernet0/0/0/2         unassigned      Shutdown        Down     default 
GigabitEthernet0/0/0/3         unassigned      Up              Up       default 
GigabitEthernet0/0/0/4         unassigned      Up              Up       default 
GigabitEthernet0/0/0/5         unassigned      Shutdown        Down     default 

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


<rpc-reply xmlns="urn:ietf:params:xml:ns:netconf:base:1.0" message-id="m-1">
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