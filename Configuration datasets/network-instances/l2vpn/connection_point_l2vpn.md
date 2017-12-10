# L2VPN (VPLS with BGP autodiscovery) configuration

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance/<ni-name>
```

## OPENCONFIG YANG

```javascript
{
    "network-instance": [
        {
            "config": {
                "name": "<ni-name>"
                "type": "L2VSI" //matches vpws-instance-type in ietf
                "enabled": true
            }
            "connection-points": {
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
                            ]
                        }
                    }
                    {
                        "config": {
                            "connection-point-id": "<connection_point_id>"
                        }
                        "endpoints": {
                            "endpoint": [
                                {
                                    "config": {
                                        "endpoint-id": "<endpoint_id>"
                                        "type": "REMOTE"
                                        "remote": {
                                            "config": {
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
        }
    ]
}
```

```javascript
{
    "network-instance": [
        {
            "config": {
                "name": "default"
            }
            "protocols": {
                "protocol": [
                    {
                        "config": {
                            "identifier": "BGP"
                            "enabled": true
                        }
                        "bgp": {
                            "global": {
                                "as": "<as-number>"
                            }
                        }
                    }
                ]
            }
        }
    ]
}

## OS Configuration Commands

### Cisco IOS (not fully tested yet ... vIOS does not support VPLS)

#### CLI

If connection point type remote
<pre>
bridge-domain &lt;ni-name&gt;

l2 vfi &lt;ni-name&gt; autodiscovery
 vpn id &lt;vccid&gt;
 bridge-domain &lt;ni-name&gt;
</pre>

If connection point type local without subif
<pre>
bridge-domain &lt;ni-name&gt;

interface &lt;local_interface_id&gt;
 service instance &lt;endpoint_id&gt; ethernet
  encapsulation untagged
  bridge-domain &lt;ni-name&gt;
</pre>

If connection point type local with subif
<pre>
bridge-domain &lt;ni-name&gt;

interface &lt;local_interface_id&gt;
 service instance &lt;endpoint_id&gt; ethernet
  encapsulation dot1q &lt;local_vlan&gt;
  rewrite ingress tag pop 1 symmetric
  bridge-domain &lt;ni-name&gt;
</pre>

### CISCO IOS XR (5.1.3) (6.1.2)

#### CLI

If connection point type remote
<pre>
l2vpn
 bridge group frinx
  bridge-domain &lt;ni-name&gt;
   vfi &lt;ni-name&gt;
    vpn-id &lt;vccid&gt;
    autodiscovery bgp
     rd auto
     route-target &lt;as-number&gt;:&lt;vccid&gt;
     signaling-protocol bgp
      ve-id &lt;endpoint_id&gt;
</pre>

If connection point type local without subif
<pre>
interface &lt;local_interface_id&gt
 l2transport

l2vpn
 bridge group frinx
  bridge-domain &lt;ni-name&gt;
   interface &lt;local_interface_id&gt
</pre>

If connection point type local with subif (for XRv 5.1.3)
<pre>
interface &lt;local_interface_id&gt.&lt;local_vlan&gt; l2transport
 dot1q vlan &lt;local_vlan&gt;

l2vpn
 bridge group frinx
  bridge-domain &lt;ni-name&gt;
   interface &lt;local_interface_id&gt.&lt;local_vlan&gt;
</pre>

If connection point type local with subif (for XRv 6.1.2)
<pre>
interface &lt;local_interface_id&gt.&lt;local_vlan&gt; l2transport
 encapsulation dot1q &lt;local_vlan&gt;
 rewrite ingress tag pop 1 symmetric
 
l2vpn
 bridge group frinx
  bridge-domain &lt;ni-name&gt;
   interface &lt;local_interface_id&gt.&lt;local_vlan&gt;
</pre>

