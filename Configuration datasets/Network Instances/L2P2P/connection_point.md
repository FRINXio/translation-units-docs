# L2P2P configuration

## URL

```
openconfig-network-instance:network-instances/network-instance/<ni-name>/connection-points/connection-point/<connection-point-id>
```

## OPENCONFIG YANG

```javascript
{
    "connection-point": [
        {
            "config": {
                "connection-point-id": "<connection_point_id>"
            }
            "endpoints": {
                "endpoint": [
                    {
                        "config": {
                            "endpoint-id": "<endpoint_id>"
                            "type": "LOCAL"
                            "local": {
                                "config": {
                                    "interface": "<local_interface_id>"
                                    "subinterface": "<local_vlan>"
                                }
                            }
                        }
                    }
                    {
                        "config": {
                            "endpoint-id": "<endpoint_id>"
                            "type": "REMOTE"
                            "remote": {
                                "config": {
                                    "remote-system": "<peer_ip>"
                                    "virtual-circuit-identifier": "<vccid>"
                                }
                            }
                        }
                    }
                ]
            }
        }
    ]
}
```

```javascript
openconfig-network-instances:network-instances/network-instance/<name>
{
    "network-instance": [
        {
            "config": {
                "name": "<ni-name>"
                "type": "L2P2P" //matches vpws-instance-type in ietf
                "enabled": true
            }
        }
    ]
}
```

## OS Configuration Commands

### Brocade

#### CLI

If endpoint type remote
---
<pre>
router mpls
 vll &lt;connection_point_id> &lt;vccid&gt;
  vll-peer &lt;peer_ip&gt;
</pre>
---

If endpoint type local without subif
---
<pre>
router mpls
 vll &lt;connection_point_id> &lt;vccid&gt;
  untag &lt;local_interface_id&gt;
</pre>
---

With subif
---
<pre>
router mpls
 vll &lt;connection_point_id> &lt;vccid&gt;
  vlan &lt;local_vlan&gt;
   tag &lt;local_interface_id&gt;
</pre>
---

If both endpoints are type local without subif
---
<pre>
router mpls
 vll-local &lt;connection_point_id&gt;
  untag &lt;local_interface_id&gt;
</pre>
---

With subif
---
<pre>
router mpls
 vll-local &lt;connection_point_id&gt;
  vlan &lt;local_vlan&gt;
   tag &lt;local_interface_id&gt;
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [brocade-unit][]

