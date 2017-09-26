# configure RSVP

## Create REST call

```
PUT
http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-network-instance:network-instances/network-instance/<ni-name>/openconfig-mpls:mpls/signaling-protocols/rsvp-te

```
## Delete REST call

```
DELETE
http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-network-instance:network-instances/network-instance/<ni-name>/openconfig-mpls:mpls/signaling-protocols/rsvp-te
```

## REST call body (required for create only)

```
{
    "interface-attributes": {
	"interface": [
	    {
		"config": {
		     "interface-id": <interface-id>
		}
		"bandwidth-reservations": {
		     "bandwidth-reservation": [
			 {
			     "reserved-bandwidth": <bandwidth>
			 }
		     ]
		}
	    }
	]
    }
}


TODO: bandwidth is not configurable @see https://github.com/openconfig/public/blob/master/release/models/mpls/openconfig-mpls-rsvp.yang
```


---

<pre>
rsvp
 interface &lt;interface-id&gt;
  bandwidth &lt;bandwidth&gt;
</pre>

---

## show REST call

```
GET
http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-network-instance:network-instances/network-instance/<ni-name>/openconfig-mpls:mpls/signaling-protocols/rsvp-te
```

