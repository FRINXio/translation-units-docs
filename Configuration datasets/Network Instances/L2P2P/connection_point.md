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

### Cisco IOS (VIOS 15.6(2)T)

#### CLI

If endpoints remote and local without subif
<pre>
interface &lt;(local)local_interface_id&gt;
 xconnect &lt;(remote)peer_ip&gt; &lt;(remote)vccid&gt; encapsulation mpls
</pre>

If endpoints remote and local with subif
<pre>
interface &lt;(local)local_interface_id&gt.&lt;(local)local_vlan&gt;
 encapsulation dot1Q &lt;(local)local_vlan&gt;
 xconnect &lt;(remote)peer_ip&gt; &lt;(remote)vccid&gt; encapsulation mpls
</pre>

If both endpoints are type local without subif
<pre>
connect &lt;ni-name&gt; &lt;(local_1)local_interface_id&gt &lt;(local_2)local_interface_id&gt; interworking ethernet
</pre>


If both endpoints are type local with subif
<pre>
connect &lt;ni-name&gt; &lt;(local_1)local_interface_id&gt.&lt;(local_1)local_vlan&gt; &lt;(local_2)local_interface_id&gt.&lt;(local_2)local_vlan&gt; interworking ethernet
</pre>

### CISCO IOS XR (5.1.3) (6.1.2)

#### CLI

If endpoint type remote
<pre>
l2vpn
 xconnect group frinx
  p2p &lt;ni-name&gt;
   neighbor ipv4 &lt;peer_ip&gt; pw-id &lt;vccid&gt;
</pre>

If endpoint type local without subif
<pre>
interface &lt;local_interface_id&gt
 l2transport

l2vpn
 xconnect group frinx
  p2p &lt;ni-name&gt;
   interface &lt;local_interface_id&gt
</pre>

If endpoint type local with subif (for XRv 5.1.3)
<pre>
interface &lt;local_interface_id&gt.&lt;local_vlan&gt; l2transport
 dot1q vlan &lt;local_vlan&gt;

l2vpn
 xconnect group frinx
  p2p &lt;ni-name&gt;
   interface &lt;local_interface_id&gt.&lt;local_vlan&gt;
</pre>

If endpoint type local with subif (for XRv 6.1.2)
<pre>
interface &lt;local_interface_id&gt.&lt;local_vlan&gt; l2transport
 encapsulation dot1q &lt;local_vlan&gt;
 rewrite ingress tag pop 1 symmetric
 
l2vpn
 xconnect group frinx
  p2p &lt;ni-name&gt;
   interface &lt;local_interface_id&gt.&lt;local_vlan&gt;
</pre>

If both endpoints are local we can use the same translation code as above .. the combined output will look like this example:
<pre>
interface &lt;(local_1)local_interface_id&gt
 l2transport
 
interface &lt;(local_2)local_interface_id&gt
 l2transport

l2vpn
 xconnect group frinx
  p2p &lt;ni-name&gt;
   interface &lt;(local_1)local_interface_id&gt
   interface &lt;(local_2)local_interface_id&gt
</pre>

### Brocade (V5.6.0fT163)

#### CLI

If endpoint type remote
<pre>
router mpls
 vll &lt;ni-name&gt; &lt;vccid&gt;
  vll-peer &lt;peer_ip&gt;
</pre>

If endpoint type local without subif
<pre>
router mpls
 vll &lt;ni-name&gt; &lt;vccid&gt;
  untag &lt;local_interface_id&gt;
</pre>

If both endpoints are type local

With subif
<pre>
router mpls
 vll &lt;ni-name&gt; &lt;vccid&gt;
  vlan &lt;local_vlan&gt;
   tag &lt;local_interface_id&gt;
</pre>

If both endpoints are type local without subif
<pre>
router mpls
 vll-local &lt;ni-name&gt;
  untag &lt;local_interface_id&gt;
</pre>

With subif
<pre>
router mpls
 vll-local &lt;ni-name&gt;
  vlan &lt;local_vlan&gt;
   tag &lt;local_interface_id&gt;
</pre>

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [brocade-unit]()

