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
                "apply-policy": {
                    "config": {
                        "import-policy": [
                            "<vrf>-route-target-import"
                        ]
                    }
                }
            }
            
            "protocols": {
                "protocol": [
                    {
                        "config": {
                            "identifier": "ospf <ospf-process-id>"
                            "enabled": true
                            "frinx-ospf-extension:export-policy": [
                                "<ospf-export-policy>"
                            ]
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
                                                "id": "<ospf_interface>"
                                                "config": {
                                                    "id": "<ospf_interface>"
                                                    "network-type": "<ospf_network_type>"
                                                    "frinx-ospf-extension:enabled": "<ospf_interface_enabled>"
                                                    "metric": <ospf_cost>
                                                    "priority": <ospf_priority>
                                                }
                                                "frinx-bfd-extension:bfd": {
                                                    "config": {
                                                        "multiplier": <bfd_interface_multiplier>
                                                        "min-interval": <bfd_interface_min_interval>
                                                        "min-receive-interval": <bfd_interface_min_recieve_interval>
                                                    }
                                                }
                                                "frinx-ospf-extension:authentication": {
                                                    "config": {
                                                        "enabled": "<ospf_auth_enabled>"
                                                        "type": "auth-type:md5"
                                                        "passwords": {
                                                            "password": [
                                                                {
                                                                    "auth-id": "<ospf_auth_id>"
                                                                    "config": {
                                                                        "auth-id": "<ospf_auth_id>"
                                                                        "auth-password": "<ospf_auth_password>"
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
                        }
                    }
                    {
                        "name": "<ospfv3-process-id>"
                        "identifier": "frinx-openconfig-policy-types:OSPF3"
                        "config": {
                            "name": "<ospfv3-process-id>"
                            "identifier": "frinx-openconfig-policy-types:OSPF3"
                        }
                        "ospfv3": {
                            "global": {
                                "stub-router": {
                                    "config": {
                                        "set": true
                                        "advertise-lsas-types": "STUB_ROUTER_MAX_METRIC"
                                        "always": true
                                    }
                                }
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
   
router ospfv3 &lt;ospfv3-process-id&gt;
 vrf &lt;vrf&gt;
  stub-router router-lsa max-metric
   always
     
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

### CISCO IOS XR (6.2.3)

#### CLI

<pre>
interface &lt;interface-id&gt;
 vrf &lt;vrf&gt;

router ospf &lt;ospf-process-id&gt;
 vrf &lt;vrf&gt;
  area &lt;area-id&gt;
   interface &lt;interface-id&gt;
    cost &lt;ospf_cost&gt;
</pre>

### CISCO IOS XR (6.6.1)

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
  area &lt;area-id&gt;
   interface &lt;interface-id&gt;
    cost &lt;ospf_cost&gt;

</pre>
##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/unitopo-units/tree/master/xr/xr-6.6/xr-6.6-network-instance-unit)

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


### Junos 14.1X53-D40.8

#### CLI

<pre>
set routing-instances &lt;vrf&gt; instance-type virtual-router
set routing-instances &lt;vrf&gt; interface &lt;interface-id&gt;
set routing-instances &lt;vrf&gt; protocols ospf area &lt;ospf_area_id&gt; interface &lt;ospf_interface&gt; interface-type &lt;ospf_network_type&gt;
set routing-instances &lt;vrf&gt; protocols ospf area &lt;ospf_area_id&gt; interface &lt;ospf_interface&gt; metric &lt;ospf_cost&gt;
set routing-instances &lt;vrf&gt; protocols ospf area &lt;ospf_area_id&gt; interface &lt;ospf_interface&gt; priority &lt;ospf_priority&gt;
delete routing-instances &lt;vrf&gt; protocols ospf area &lt;ospf_area_id&gt; interface &lt;ospf_interface&gt; disable 
| set routing-instances &lt;vrf&gt; protocols ospf area &lt;ospf_area_id&gt; interface &lt;ospf_interface&gt; disable
set routing-instances &lt;vrf&gt; protocols ospf area &lt;ospf_area_id&gt; interface &lt;ospf_interface&gt; authentication md5 &lt;ospf_auth_id&gt; key &lt;ospf_auth_password&gt;
| delete routing-instances &lt;vrf&gt; protocols ospf area &lt;ospf_area_id&gt; interface &lt;ospf_interface&gt; authentication
set routing-instances &lt;vrf&gt; protocols ospf area &lt;ospf_area_id&gt; interface &lt;ospf_interface&gt; bfd-liveness-detection minimum-interval &lt;bfd_interface_min_interval&gt;
set routing-instances &lt;vrf&gt; protocols ospf area &lt;ospf_area_id&gt; interface &lt;ospf_interface&gt; bfd-liveness-detection minimum-receive-interval &lt;bfd_interface_min_recieve_interval&gt;
set routing-instances &lt;vrf&gt; protocols ospf area &lt;ospf_area_id&gt; interface &lt;ospf_interface&gt; bfd-liveness-detection multiplier &lt;bfd_interface_multiplier&gt;
</pre>

*virtual-router* is a conversion of &lt;type&gt; set *L3VRF*  
*delete routing-instances &lt;vrf&gt; protocols ospf area &lt;ospf_area_id&gt; interface &lt;ospf_interface&gt; disable* is a conversion of &lt;ospf_interface_enabled&gt; set *true*  
*set routing-instances &lt;vrf&gt; protocols ospf area &lt;ospf_area_id&gt; interface &lt;ospf_interface&gt; disable* is a conversion of &lt;ospf_interface_enabled&gt; set *false*  
*set routing-instances &lt;vrf&gt; protocols ospf area &lt;ospf_area_id&gt; interface &lt;ospf_interface&gt; authentication* is a conversion of &lt;ospf_auth_enabled&gt; set *true*  
*delete routing-instances &lt;vrf&gt; protocols ospf area &lt;ospf_area_id&gt; interface &lt;ospf_interface&gt; authentication* is a conversion of &lt;ospf_auth_enabled&gt; set *false*  

<pre>
set routing-instances &lt;vrf&gt; routing-options instance-import &lt;vrf&gt;-route-target-import
set routing-instances &lt;vrf&gt; protocols ospf export &lt;ospf-export-policy&gt;
</pre>

### Junos 18.2R1-S2.1

#### CLI

<pre>
set routing-instances &lt;vrf&gt; interface &lt;interface-id&gt;
</pre>