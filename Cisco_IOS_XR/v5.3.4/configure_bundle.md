# configure interface

## Create REST call

```
PUT
http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-network-instance/network-instances/<ni-name>/interfaces/
```
## Remove REST call

```
DELETE
http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-network-instance/network-instances/<ni-name>/interfaces/

```

## REST call body 

```
{
    "config": {
        "type": "iana-if-type:ieee8023adLag",
        "enabled": true,
        "name": "<intf-id>"
    }
    "aggregation": {
        "config": {
            "min-links": <min-links>
        }
    }
}
```

---

<pre>
interface &lt;intf-id&gt;
 bundle minimum-active links &lt;min-links&gt;
</pre>

---

## show RPC call

```
GET
http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-network-instance/network-instances/<ni-name>/interfaces/

```
