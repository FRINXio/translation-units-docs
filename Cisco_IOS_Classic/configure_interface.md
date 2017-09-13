# configure interface

## Create REST call

```
PUT
http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-interfaces:interfaces/interface/<intf-id>

```
## Delete REST call

```
DELETE
http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-interfaces:interfaces/interface/<intf-id>
```

## REST call body (required for create only)

```
{
    "interface": [
        {
            "name": "<intf-id>",
            "config": {
                "type": "iana-if-type:softwareLoopback",
                "enabled": false,
                "name": "<intf-id>"
            }
        }
    ]
}
```


---

<pre>
interface &lt;intf-id&gt;
 description &lt;descr&gt;
 mtu &lt;mtu&gt;
 &lt;enabled?&gt; shutdown
</pre>




