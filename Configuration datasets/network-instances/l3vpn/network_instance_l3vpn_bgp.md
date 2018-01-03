# L3VPN configuration (BGP as CE-PE protocol)

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance/<vrf>
```

## OPENCONFIG YANG

```javascript
{
    "network-instance": [
        {
            "config": {
                "name": "<vrf>"
                "type": "L3VRF" //matches vpws-instance-type in ietf
                "route-distinguisher": "<rd>"
                "enabled-address-families": "<enabled-address-families>"
                "enabled": true
            }
            
            "interfaces": {
                "interface": [
                    {
                        "config": {
                            "id": <interface-id>
                        }
                    }
                ]
            }

            "protocols": {
                "protocol": [
                    {
                        "config": {
                            "identifier": "BGP"
                            "enabled": true
                        }
                        
                        "local-aggregates": {
                            "aggregate": [
                                {
                                    "config": {
                                        "prefix": "<network-prefix>"
                                    }
                                }
                            ]
                        }
                        
                        "bgp": {
                            "global": {
                                "as": "<as-number>"
                                "router-id": "<router-id>"
                                "afi-safis": {
                                    "afi-safi": [
                                        "config": {
                                            "afi-safi-name": "ipv4"
                                            "enabled": true
                                        }
                                    ]
                                }
                            }
                            "neighbors": {
                                "neighbor": [
                                    {
                                        "config": {
                                            "neighbor-address": "<neighbor-address>"
                                            "enabled": true
                                            "peer-as": "<remote-as>"
                                            "afi-safis": {
                                                "afi-safi": [
                                                    "config": {
                                                        "afi-safi-name": "ipv4"
                                                        "enabled": true
                                                    }
                                                    "apply-policy": {
                                                        "config": {
                                                            "import-policy": "<import-policy>"
                                                            "export-policy": "<export-policy>"
                                                        }
                                                    }
                                                ]
                                            }
                                        }
                                    }
                                ]
                            }
                        }
                    }
                ]
            }
        }
    ]
}
```

```
frinx-openconfig-routing-policy:routing-policy/defined-sets<vrf>
```

```
{
    "bgp-defined-sets" {
        ext-community-sets {
            ext-community-set [
                {            
                    "config": {
                        "ext-community-set-name": "<vrf>-route-target-export-set"
                        "ext-community-set-member": [
                            {<rt_exp_1>}
                            {<rt_exp_2>}
                            {<rt_exp_3>}
                        ]
                       }
                }
                {            
                    "config": {
                        "ext-community-set-name": "<vrf>-route-target-import-set"
                        "ext-community-set-member": [
                            {<rt_imp_1>}
                            {<rt_imp_2>}
                            {<rt_imp_3>}
                        ]
                       }
                }
            ]
        }
    }
}
```
CONSTRAINTS:
Network-instance with name &lt;vrf&gt; must exist before defined-sets or both must be created in the same transaction.  
Delete must be executed in reverse order or in the same transaction.  
Policy &lt;import-policy&gt; and &lt;export-policy&gt; must exist on device before are used in network-instance.

## OS Configuration Commands

### CISCO IOS XR (5.1.3) (6.1.2)

#### CLI

<pre>
vrf &lt;vrf&gt;
 address-family ipv4 unicast
  import route-target 
   {&lt;rt_imp_1&gt;}
   {&lt;rt_imp_2&gt;}
   {&lt;rt_imp_3&gt;}
  export route-target 
   {&lt;rt_exp_1&gt;}
   {&lt;rt_exp_2&gt;}
   {&lt;rt_exp_3&gt;}

interface &lt;interface-id&gt;
 vrf &lt;vrf&gt;
 
router bgp &lt;as-number&gt;
 vrf &lt;vrf&gt;
  rd &lt;rd&gt;
  
  address-family ipv4 unicast
   network &lt;network-prefix&gt;
   
  neighbor &lt;neighbor-address&gt;
   remote-as &lt;remote-as&gt;
   address-family ipv4 unicast
    route-policy &lt;import-policy&gt; in
    route-policy &lt;export-policy&gt; out
</pre>

### Cisco IOS (VIOS 15.6(2)T)

#### CLI

<pre>
ip vrf &lt;vrf&gt;
 rd &lt;rd&gt;
 route-target export {&lt;rt_exp_1&gt;}
 route-target export {&lt;rt_exp_2&gt;}
 route-target export {&lt;rt_exp_3&gt;}
 route-target import {&lt;rt_imp_1&gt;}
 route-target import {&lt;rt_imp_2&gt;}
 route-target import {&lt;rt_imp_3&gt;}

interface &lt;interface-id&gt;
 ip vrf forwarding &lt;vrf&gt;

router bgp &lt;as-number&gt;
 address-family ipv4 vrf &lt;vrf&gt;
  network &lt;network-prefix&gt;
  neighbor &lt;neighbor-address&gt; remote-as &lt;remote-as&gt;
  neighbor &lt;neighbor-address&gt; activate
</pre>
