# configure interface

## Create REST call

```
PUT
http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-interfaces:interfaces/
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
interface &lt;intf-id&gt;
 no shutdown
</pre>
