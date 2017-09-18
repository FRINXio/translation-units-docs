# configure RSVP

## Create REST call

```
PUT
http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-mpls:mpls/

```
## Delete REST call

```
DELETE
http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-mpls:mpls/
```

## REST call body (required for create only)

```
{
    "mpls": [ 
        {
            "signaling-protocols": {
                "rsvp-te": {
                    "interface-attributes": {
                        "interfaces": [
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
            }
        }
    ]
}
```


---

<pre>
rsvp
 interface &lt;interface-id&gt;
  bandwidth &lt;bandwidth&gt;
</pre>




