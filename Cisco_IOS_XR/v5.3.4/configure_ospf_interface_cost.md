# configure OSPF interface cost

## Create REST call

```
PUT
http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-network-instance:network-instance/network-instance/<ni-name>/protocols/OSPF
```
## Delete REST call

```
DELETE
http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-network-instance:network-instance/network-instance/<ni-name>/protocols/OSPF
```

## REST call body (required for create only)

```
{
    "config": {
	"identifier": "OSPF"
    }
    "ospfv-2": {
	"global": {
	    "config": {
		 "router-id":<router-id>
	    }
	} 
	"area": [
	    {
		"config": {
		    "identifier":<area-id>
		}
		"interfaces": [
		    {
                        "id":<interface-id>
                        "config": {
			    "metric:"<cost>
			}
		    }
		]
	    }
	]
    }
}
```


---

<pre>
router ospf &lt;router-id&gt;
 area &lt;area-id&gt;
  interface &lt;interface-id&gt;
   cost &lt;cost&gt;
</pre>

---

## show REST call

```
GET
http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-network-instance:network-instance/network-instance/<ni-name>/protocols/OSPF
```





