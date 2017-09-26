# configure OSPF

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
	    "max-metric": {
                "config": {
		    "set":true
		    "include": [ { "MAX_METRIC_INCLUDE_STUB" } ]
                }
	    }
	}
        areas {
            "area": [
                {
		    "identifier": <area-id>
		    "lsdb": {
			"lsa-types": [{
			     "lsa-type": {
				 "type":"ROUTER_LSA"
			     }
			     "lsa-type": {
				 "type":"SUMMARY_ASBR_LSA"
			     }
			     "lsa-type": {
				 "type":"AS_EXTERNAL_LSA"
			     }
			}]
		    }
                }
            ]
        }
    }
}

TODO: lsdb parameters are not configurable @see https://github.com/openconfig/public/blob/master/release/models/ospf/openconfig-ospfv2-lsdb.yang

```

---

<pre>
router ospf &l;router-id&gt;
  max-metric router-lsa include-stub summary-lsa external-lsa
</pre>

---

## show REST call

```
GET 
http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-network-instance:network-instance/network-instance/<ni-name>/protocols/OSPF

```

