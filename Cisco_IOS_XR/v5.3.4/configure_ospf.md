# configure OSPF

## Create REST call

```
PUT
http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-network-instance:network-instance

```
## Delete REST call

```
DELETE
http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-network-instance:network-instance/
```

## REST call body (required for create only)

```
{
    "network-instances": [ 
        {
            "protocols": [
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
                                 "set":true
                                 "include": [ { "MAX_METRIC_INCLUDE_STUB" } ]
                            }
                        }
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
                }
            }
        }
    ]
}
```


---

<pre>
router ospf &l;router-id&gt;
  max-metric router-lsa include-stub summary-lsa external-lsa
</pre>




