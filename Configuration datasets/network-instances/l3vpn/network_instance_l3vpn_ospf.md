# L3VPN configuration (OSPF as CE-PE protocol)

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
            
            "inter-instance-policies": {
                "apply-policy": [
                    "config": {
                        "export-policy": "<vrf>-route-target-export"
                        "import-policy": "<vrf>-route-target-import"
                    }
                ]
            }
            
            "protocols": {
                "protocol": [
                    {
                        "config": {
                            "identifier": "ospf <ospf-process-id>"
                            "enabled": true
                        }
                        
                        "ospfv2": {
                            "global": {
                                "as": "<as-number>"
                                "router-id": "<router-id>"
                            }
                            "areas": {
                                "area": [
                                    {
                                        "config": {
                                            "identifier": "<area-id>"
                                        }
                                        "interfaces" {
                                            "interface" [
                                                "config": {
                                                    "identifier": "<interface-id>"
                                                }
                                            ]
                                        }
                                    }
                                ]
                            }
                        }
                    }
                    {
                        "config": {
                            "identifier": "bgp"
                            "enabled": true
                        }
                        
                        "bgp": {
                            "global": {
                                "as": "<as-number>"
                                "afi-safis": {
                                    "afi-safi": [
                                        "config": {
                                            "afi-safi-name": "ipv4"
                                            "enabled": true
                                        }
                                    ]
                                }
                            }
                        }
                    }
                ]
            }
            "tables": {
                "table": [
                    {
                        "config": {
                            "protocol": "ospf <ospf-process-id>"
                        }
                        "address-family": "ipv4"
                    }
                    {
                        "config": {
                            "protocol": "bgp <as-number>"
                        }
                        "address-family": "ipv4"
                    }
                ]
            }
            "table-connections": {
                "table-connection": [
                    {
                        "config": {
                            "src-protocol": "<redistribute2_from>" = "ospf <ospf-process-id>"
                            "dst-protocol": "<redistribute2_to>" = "bgp <as-number>"
                        }
                        "address-family": "ipv4"
                    }
                    {
                        "config": {
                            "src-protocol": "<redistribute1_from>" = "bgp <as-number>"
                            "dst-protocol": "<redistribute1_to>" = "ospf <ospf-process-id>"
                        }
                        "address-family": "ipv4"
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

```
frinx-openconfig-routing-policy:routing-policy/policy-definitions<vrf>
```

```
{
    "policy-definition" [
        {            
            "config": {
                "name": "<vrf>-route-target-import"
                "statements": {
                    "statement" [
                        {
                            "conditions" {
                                "bgp-conditions" {
                                    "match-ext-community-set" {
                                        "config": {
                                            "ext-community-set": "<vrf>-route-target-import-set"
                                        }
                                    }
                                }
                            }
                            "actions" {
                                "config": {
                                    "policy-result": "ACCEPT_ROUTE"
                                }
                            }
                        }
                    ]
                }
            }
        }
        {            
            "config": {
                "name": "<vrf>-route-target-export"
                "statements": {
                    "statement" [
                        {
                            "name": "<vrf>-route-target-export-statement"
                            "actions" {
                                "bgp-actions" {
                                    "set-ext-community" {
                                        "config": {
                                            "method": "REFERENCE"
                                            "reference" {
                                                "config": {
                                                    "ext-community-set-ref": "<vrf>-route-target-export-set"
                                                }
                                            }
                                        }
                                    }
                                }
                            }
                        }
                    ]
                }
            }
        }
    ]
}
```

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

router ospf &lt;ospf-process-id&gt;
 vrf &lt;vrf&gt;
  router-id &lt;router-id&gt;
  
  area &lt;area-id&gt;
   interface &lt;interface-id&gt;
   
router bgp &lt;as-number&gt;
 vrf &lt;vrf&gt;
  address-family ipv4 unicast
  
router &lt;redistribute1-to&gt;
 vrf &lt;vrf&gt;
  address-family ipv4 unicast
   redistribute &lt;redistribute1-from&gt;
   
router &lt;redistribute2-to&gt;
 vrf &lt;vrf&gt;
  address-family ipv4 unicast
   redistribute &lt;redistribute2-from&gt;
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
 ip ospf &lt;ospf-process-id&gt; area &lt;area-id&gt;

router &lt;ospf-process-id&gt; vrf &lt;vrf&gt;

router &lt;redistribute1-to&gt; vrf &lt;vrf&gt;
 redistribute b&lt;redistribute1-from&gt; subnets

router &lt;redistribute2-to&gt;
 address-family ipv4 vrf &lt;vrf&gt;
  redistribute &lt;redistribute2-from&gt; 
</pre>
