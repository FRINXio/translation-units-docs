# configure ipv4 interface

## Create REST call

```
PUT
http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/IOS2/yang-ext:mount/openconfig-interfaces:interfaces/interface/Loopback99/subinterfaces/subinterface/0/ipv4/addresses/address/44.44.44.44
```

## Delete REST call

```
DELETE
http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/IOS2/yang-ext:mount/openconfig-interfaces:interfaces/interface/Loopback99/subinterfaces/subinterface/0/ipv4/addresses/address/44.44.44.44
```

## REST call body (required for create only)

```
{
    "openconfig-if-ip:address": [
        {
            "ip": "44.44.44.44",
            "config": {
                "prefix-length": 24,
                "ip": "44.44.44.44"
            }
        }
    ]
}
```

---

<pre>
configure terminal
interface Loopback99
ip address 44.44.44.44 255.255.255.0
exit
exit


configure terminal
interface Loopback99
no ip address 44.44.44.44 255.255.255.0
</pre>





