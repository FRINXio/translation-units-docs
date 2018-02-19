# L2VPN (VPLS with BGP autodiscovery) configuration

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance/{{vpls_ni_name}}
```

## OPENCONFIG YANG

```javascript
{
    "network-instance": [
        {
            "config": {
                "name": "{{vpls_ni_name}}"
                "type": "L2VSI" //matches vpls-instance-type in ietf
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
                                                "interface": "{{vpls_show_interface3}}"
                                                "subinterface": {{vpls_show_sub_interface_index}}
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
                                        "endpoint-id": "{{vpls_endpoint_id}}"
                                        "type": "REMOTE"
                                        "remote": {
                                            "config": {
                                                "virtual-circuit-identifier": {{vpls_vccid}}
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
                                "as": {{vpls_bgp_as_number}}
                            }
                        }
                    }
                ]
            }
        }
    ]
}
```

## OS Configuration Commands

### Cisco IOS (not fully tested yet ... vIOS does not support VPLS)

#### CLI

If connection point type remote
<pre>
bridge-domain {{vpls_ni_name}}

l2 vfi {{vpls_ni_name}} autodiscovery
 vpn id {{vpls_vccid}}
 bridge-domain {{vpls_ni_name}}
</pre>

If connection point type local without subif
<pre>
bridge-domain {{vpls_ni_name}}

interface {{vpls_show_interface3}}
 service instance {{vpls_endpoint_id}} ethernet
  encapsulation untagged
  bridge-domain {{vpls_ni_name}}
</pre>

If connection point type local with subif
<pre>
bridge-domain {{vpls_ni_name}}

interface {{vpls_show_interface3}}
 service instance {{vpls_endpoint_id}} ethernet
  encapsulation dot1q{{vpls_show_sub_interface_index}}
  rewrite ingress tag pop 1 symmetric
  bridge-domain {{vpls_ni_name}}
</pre>

##### Unit

NOT IMPLEMENTED

### CISCO IOS XR (5.1.3) (6.1.2)

#### CLI

If connection point type remote
<pre>
l2vpn
 bridge group frinx
  bridge-domain {{vpls_ni_name}}
   vfi {{vpls_ni_name}}
    vpn-id {{vpls_vccid}}
    autodiscovery bgp
     rd auto
     route-target {{vpls_bgp_as_number}}:{{vpls_vccid}}
     signaling-protocol bgp
      ve-id {{vpls_endpoint_id}}
</pre>

If connection point type local without subif
<pre>
interface {{vpls_show_interface3}}
 l2transport

l2vpn
 bridge group frinx
  bridge-domain {{vpls_ni_name}}
   interface {{vpls_show_interface3}}
</pre>

If connection point type local with subif (for XRv 5.1.3)
<pre>
interface {{vpls_show_interface3}}.{{vpls_show_sub_interface_index}} l2transport
 dot1q vlan {{vpls_show_sub_interface_index}}

l2vpn
 bridge group frinx
  bridge-domain {{vpls_ni_name}}
   interface {{vpls_show_interface3}}.{{vpls_show_sub_interface_index}}
</pre>

If connection point type local with subif (for XRv 6.1.2)
<pre>
interface {{vpls_show_interface3}}.{{vpls_show_sub_interface_index}} l2transport
 encapsulation dot1q {{vpls_show_sub_interface_index}}
 rewrite ingress tag pop 1 symmetric
 
l2vpn
 bridge group frinx
  bridge-domain {{vpls_ni_name}}
   interface {{vpls_show_interface3}}.{{vpls_show_sub_interface_index}}
</pre>

##### Unit

NOT IMPLEMENTED
