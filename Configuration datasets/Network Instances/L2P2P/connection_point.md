# L2P2P configuration

## URL

```
openconfig-network-instance:network-instances/network-instance/<ni-name>/connection-points/connection-point/<connection-point-id>
```

## OPENCONFIG YANG

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

openconfig-network-instances:network-instances/network-instance/<name>/connection-points/connection-point/<connection-point-id>
{
    "connection-point": [
        {
            "config": {
                "connection-point-id": "<connection_point_id>"
            }
        }
    ]
}
openconfig-network-instances:network-instances/network-instance/<name>/connection-points/connection-point/<connection-point-id>/endpoints/endpoint/<endpoint-id>
{
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
    ]
}

openconfig-network-instances:network-instances/network-instance/<name>/connection-points/connection-point/<connection-point-id>/endpoints/endpoint/<endpoint-id>
{
    "endpoint": [
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
```


## OS Configuration Commands

### Brocade

#### CLI

##### if endpoint type remote

---
<pre>
router mpls
 vll <connection_point_id> <vccid>
  vll-peer <peer_ip>
</pre>
---

##### if endpoint type local
###### without subif
---
<pre>
router mpls
 vll <connection_point_id> <vccid>
  untag <local_interface_id>
</pre>
---

###### with subif
---
<pre>
router mpls
 vll <connection_point_id> <vccid>
  vlan <local_vlan>
   tag <local_interface_id>
</pre>
---

##### if both endpoints are type local
###### without subif
---
<pre>
router mpls
 vll-local <connection_point_id>
  untag <local_interface_id>
</pre>
---

###### with subif
---
<pre>
router mpls
 vll-local <connection_point_id>
  vlan <local_vlan>
   tag <local_interface_id>
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [brocade-unit][]

