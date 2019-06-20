# L2P2P configuration

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance/{{l2p2p_ni_name1}}
```

## OPENCONFIG YANG

```javascript
{
    "network-instance": [
        {
            "config": {
                "name": "{{l2p2p_ni_name1}}"
                "type": "L2P2P" //matches vpws-instance-type in ietf
                "enabled": true
            }
            "connection-points": {
                "connection-point": [
                    {
                        "config": {
                            "connection-point-id": 1
                        }
                        "endpoints": {
                            "endpoint": [
                                {
                                    "config": {
                                        "endpoint-id": "{{l2p2p_endpoint_id}}"
                                        "type": "LOCAL"
                                        "local": {
                                            "config": {
                                                "interface": "{{l2p2p_show_interface3}}"
                                                "subinterface": {{l2p2p_vlan_id}}
                                            }
                                        }
                                    }
                                }
                            ]
                        }
                    }
                    {
                        "config": {
                            "connection-point-id": 2
                        }
                        "endpoints": {
                            "endpoint": [
                                {
                                    "config": {
                                        "endpoint-id": "{{l2p2p_endpoint_id}}"
                                        "type": "REMOTE"
                                        "remote": {
                                            "config": {
                                                "remote-system": "{{l2p2p_show_remoteip}}"
                                                "virtual-circuit-identifier": "{{l2p2p_vccid}}"
                                            }
                                        }
                                    }
                                }
                            ]
                        }
                    }
                ]
            }
        }
    ]
}
```


## OS Configuration Commands

### Cisco IOS (VIOS 15.6(2)T)

#### CLI

If connection points remote and local without subif
<pre>
interface {{l2p2p_show_interface3}}
 xconnect {{l2p2p_show_remoteip}} {{l2p2p_vccid}} encapsulation mpls
</pre>

If connection points remote and local with subif
<pre>
interface {{l2p2p_show_interface3}}.{{l2p2p_vlan_id}}
 encapsulation dot1Q {{l2p2p_vlan_id}}
 xconnect {{l2p2p_show_remoteip}} {{l2p2p_vccid}} encapsulation mpls
</pre>

If both connection points are type local without subif
<pre>
connect {{l2p2p_ni_name1}} &lt;(local_1)local_interface_id&gt &lt;(local_2)local_interface_id&gt; interworking ethernet
</pre>


If both connection points are type local with subif
<pre>
connect {{l2p2p_ni_name1}} &lt;(local_1)local_interface_id&gt.&lt;(local_1)local_vlan&gt; &lt;(local_2)local_interface_id&gt.&lt;(local_2)local_vlan&gt; interworking ethernet
</pre>

##### Unit

Link to github : [ios-unit](https://github.com/FRINXio/cli-units/tree/master/ios/network-instance/src/main/java/io/frinx/cli/unit/ios/network/instance/handler/l2p2p)

### CISCO IOS XR (5.1.3) (6.1.2)

#### CLI

If connection point type remote
<pre>
l2vpn
 xconnect group frinx
  p2p {{l2p2p_ni_name1}}
   neighbor ipv4 {{l2p2p_show_remoteip}} pw-id {{l2p2p_vccid}}
</pre>

If connection point type local without subif
<pre>
interface {{l2p2p_show_interface3}}
 l2transport

l2vpn
 xconnect group frinx
  p2p {{l2p2p_ni_name1}}
   interface {{l2p2p_show_interface3}}
</pre>

If connection point type local with subif (for XRv 5.1.3)
<pre>
interface {{l2p2p_show_interface3}}.{{l2p2p_vlan_id}} l2transport
 dot1q vlan {{l2p2p_vlan_id}}

l2vpn
 xconnect group frinx
  p2p {{l2p2p_ni_name1}}
   interface {{l2p2p_show_interface3}}.{{l2p2p_vlan_id}}
</pre>

If connection point type local with subif (for XRv 6.1.2)
<pre>
interface {{l2p2p_show_interface3}}.{{l2p2p_vlan_id}} l2transport
 encapsulation dot1q {{l2p2p_vlan_id}}
 rewrite ingress tag pop 1 symmetric
 
l2vpn
 xconnect group frinx
  p2p {{l2p2p_ni_name1}}
   interface {{l2p2p_show_interface3}}.{{l2p2p_vlan_id}}
</pre>

If both connection points are local we can use the same translation code as above .. the combined output will look like this example:
<pre>
interface &lt;(local_1)local_interface_id&gt
 l2transport
 
interface &lt;(local_2)local_interface_id&gt
 l2transport

l2vpn
 xconnect group frinx
  p2p {{l2p2p_ni_name1}}
   interface &lt;(local_1)local_interface_id&gt
   interface &lt;(local_2)local_interface_id&gt
</pre>

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/unitopo-units/tree/master/xr/xr-6/xr-6-network-instance-unit/src/main/kotlin/io/frinx/unitopo/unit/xr6/network/instance/handler/l2p2p)

### Brocade (V5.6.0fT163)

#### CLI

If connection point type remote
<pre>
router mpls
 vll {{l2p2p_ni_name1}} {{l2p2p_vccid}}
  vll-peer {{l2p2p_show_remoteip}}
</pre>

If connection point type local without subif
<pre>
router mpls
 vll {{l2p2p_ni_name1}} {{l2p2p_vccid}}
  untag {{l2p2p_show_interface3}}
</pre>

If both connection points are type local

With subif
<pre>
router mpls
 vll {{l2p2p_ni_name1}} {{l2p2p_vccid}}
  vlan {{l2p2p_vlan_id}}
   tag {{l2p2p_show_interface3}}
</pre>

If both connection points are type local without subif
<pre>
router mpls
 vll-local {{l2p2p_ni_name1}}
  untag {{l2p2p_show_interface3}}
</pre>

With subif
<pre>
router mpls
 vll-local {{l2p2p_ni_name1}}
  vlan {{l2p2p_vlan_id}}
   tag {{l2p2p_show_interface3}}
</pre>

##### Unit

Link to github : [brocade-unit](https://github.com/FRINXio/cli-units/tree/master/brocade/network-instance/src/main/java/io/frinx/cli/unit/brocade/network/instance/l2p2p)

