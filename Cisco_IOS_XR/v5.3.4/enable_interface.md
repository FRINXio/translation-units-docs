# configure interface

## Create REST call

```
PUT
http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-interfaces:interfaces/interface/<intf-id>/config
```

## REST call body 

```
{
    "config": {
        "type": "iana-if-type:softwareLoopback",
        "enabled": true,
        "name": "<intf-id>"
    }
}
```

---

<pre>
configure terminal
interface &lt;intf-id&gt;
description null
no shutdown
exit
exit
</pre>




