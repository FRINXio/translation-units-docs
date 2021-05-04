# L3VPN configuration (OSPF as CE-PE protocol)

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance={{vrf}}
```

## OPENCONFIG YANG

```javascript
{
    "network-instance": [
        {
            "name": "{{vrf}}"
            "config": {
                "name": "{{vrf}}"
                "type": "L3VRF" //matches vpws-instance-type in ietf
                "route-distinguisher": "{{rd}}"
                "enabled-address-families": "{{enabled-address-families}}"
                "enabled": true
            }
            
            "interfaces": {
                "interface": [
                    {
                        "config": {
                            "id": {{interface-id}}
                        }
                    }
                ]
            }
            
            "inter-instance-policies": {
                "apply-policy": {
                    "config": {
                        "import-policy": [
                            "{{vrf}}-route-target-import"
                        ]
                    }
                }
            }
            
            "protocols": {
                "protocol": [
                    {
                        "config": {
                            "identifier": "ospf {{ospf-process-id}}"
                            "enabled": true
                            "frinx-ospf-extension:export-policy": [
                                "{{ospf-export-policy}}"
                            ]
                        }
                        
                        "ospfv2": {
                            "global": {
                                "as": "{{as-number}}"
                                "router-id": "{{router-id}}"
                            }
                            "areas": {
                                "area": [
                                    {
                                        "config": {
                                            "identifier": "{{area-id}}"
                                        }
                                        "interfaces" {
                                            "interface" [
                                                "id": "{{ospf_interface}}"
                                                "config": {
                                                    "id": "{{ospf_interface}}"
                                                    "network-type": "{{ospf_network_type}}"
                                                    "frinx-ospf-extension:enabled": "{{ospf_interface_enabled}}"
                                                    "metric": {{ospf_cost}}
                                                    "priority": {{ospf_priority}}
                                                }
                                                "frinx-bfd-extension:bfd": {
                                                    "config": {
                                                        "multiplier": {{bfd_interface_multiplier}}
                                                        "min-interval": {{bfd_interface_min_interval}}
                                                        "min-receive-interval": {{bfd_interface_min_recieve_interval}}
                                                    }
                                                }
                                                "frinx-ospf-extension:authentication": {
                                                    "config": {
                                                        "enabled": "{{ospf_auth_enabled}}"
                                                        "type": "auth-type:md5"
                                                        "passwords": {
                                                            "password": [
                                                                {
                                                                    "auth-id": "{{ospf_auth_id}}"
                                                                    "config": {
                                                                        "auth-id": "{{ospf_auth_id}}"
                                                                        "auth-password": "{{ospf_auth_password}}"
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
                        "name": "{{ospfv3-process-id}}"
                        "identifier": "frinx-openconfig-policy-types:OSPF3"
                        "config": {
                            "name": "{{ospfv3-process-id}}"
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
                                "as": "{{as-number}}"
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
                            "protocol": "ospf {{ospf-process-id}}"
                        }
                        "address-family": "ipv4"
                    }
                    {
                        "config": {
                            "protocol": "bgp {{as-number}}"
                        }
                        "address-family": "ipv4"
                    }
                ]
            }
            "table-connections": {
                "table-connection": [
                    {
                        "config": {
                            "src-protocol": "{{redistribute2_from}}" = "ospf {{ospf-process-id}}"
                            "dst-protocol": "{{redistribute2_to}}" = "bgp {{as-number}}"
                        }
                        "address-family": "ipv4"
                    }
                    {
                        "config": {
                            "src-protocol": "{{redistribute1_from}}" = "bgp {{as-number}}"
                            "dst-protocol": "{{redistribute1_to}}" = "ospf {{ospf-process-id}}"
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
frinx-openconfig-routing-policy:routing-policy/defined-sets{{vrf}}
```

```
{
    "bgp-defined-sets" {
        ext-community-sets {
            ext-community-set [
                {            
                    "config": {
                        "ext-community-set-name": "{{vrf}}-route-target-export-set"
                        "ext-community-set-member": [
                            {{rt_exp_1}}
                            {{rt_exp_2}}
                            {{rt_exp_3}}
                        ]
                    }
                }
                {            
                    "config": {
                        "ext-community-set-name": "{{vrf}}-route-target-import-set"
                        "ext-community-set-member": [
                            {{rt_imp_1}}
                            {{rt_imp_2}}
                            {{rt_imp_3}}
                        ]
                    }
                }
            ]
        }
    }
}
```

```
frinx-openconfig-routing-policy:routing-policy/policy-definitions{{vrf}}
```

```
{
    "policy-definition" [
        {            
            "config": {
                "name": "{{vrf}}-route-target-import"
                "statements": {
                    "statement" [
                        {
                            "conditions" {
                                "bgp-conditions" {
                                    "match-ext-community-set" {
                                        "config": {
                                            "ext-community-set": "{{vrf}}-route-target-import-set"
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
                "name": "{{vrf}}-route-target-export"
                "statements": {
                    "statement" [
                        {
                            "name": "{{vrf}}-route-target-export-statement"
                            "actions" {
                                "bgp-actions" {
                                    "set-ext-community" {
                                        "config": {
                                            "method": "REFERENCE"
                                            "reference" {
                                                "config": {
                                                    "ext-community-set-ref": "{{vrf}}-route-target-export-set"
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
vrf {{vrf}}
 address-family ipv4 unicast
  import route-target 
   {{rt_imp_1}}
   {{rt_imp_2}}
   {{rt_imp_3}}
  export route-target 
   {{rt_exp_1}}
   {{rt_exp_2}}
   {{rt_exp_3}}

interface {{interface-id}}
 vrf {{vrf}}

router ospf {{ospf-process-id}}
 vrf {{vrf}}
  router-id {{router-id}}
  
  area {{area-id}}
   interface {{interface-id}}
   
router ospfv3 {{ospfv3-process-id}}
 vrf {{vrf}}
  stub-router router-lsa max-metric
   always
     
router bgp {{as-number}}
 vrf {{vrf}}
  address-family ipv4 unicast
  
router {{redistribute1-to}}
 vrf {{vrf}}
  address-family ipv4 unicast
   redistribute {{redistribute1-from}}
   
router {{redistribute2-to}}
 vrf {{vrf}}
  address-family ipv4 unicast
   redistribute {{redistribute2-from}}
</pre>

### CISCO IOS XR (6.2.3)

#### CLI

<pre>
interface {{interface-id}}
 vrf {{vrf}}

router ospf {{ospf-process-id}}
 vrf {{vrf}}
  area {{area-id}}
   interface {{interface-id}}
    cost {{ospf_cost}}
</pre>

### CISCO IOS XR (6.6.1)

#### CLI

<pre>
vrf {{vrf}}
 address-family ipv4 unicast
  import route-target 
   {{rt_imp_1}}
   {{rt_imp_2}}
   {{rt_imp_3}}
  export route-target 
   {{rt_exp_1}}
   {{rt_exp_2}}
   {{rt_exp_3}}

interface {{interface-id}}
 vrf {{vrf}}

router ospf {{ospf-process-id}}
 vrf {{vrf}}
  area {{area-id}}
   interface {{interface-id}}
    cost {{ospf_cost}}

</pre>
##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/unitopo-units/tree/master/xr/xr-6.6/xr-6.6-network-instance-unit)

### Cisco IOS (VIOS 15.6(2)T)

#### CLI

<pre>
ip vrf {{vrf}}
 rd {{rd}}
 route-target export {{rt_exp_1}}
 route-target export {{rt_exp_2}}
 route-target export {{rt_exp_3}}
 route-target import {{rt_imp_1}}
 route-target import {{rt_imp_2}}
 route-target import {{rt_imp_3}}

interface {{interface-id}}
 ip vrf forwarding {{vrf}}
 ip ospf {{ospf-process-id}} area {{area-id}}

router {{ospf-process-id}} vrf {{vrf}}

router {{redistribute1-to}} vrf {{vrf}}
 redistribute b{{redistribute1-from}} subnets

router {{redistribute2-to}}
 address-family ipv4 vrf {{vrf}}
  redistribute {{redistribute2-from}} 
</pre>


### Junos 14.1X53-D40.8

#### CLI

<pre>
set routing-instances {{vrf}} instance-type virtual-router
set routing-instances {{vrf}} interface {{interface-id}}
set routing-instances {{vrf}} protocols ospf area {{ospf_area_id}} interface {{ospf_interface}} interface-type {{ospf_network_type}}
set routing-instances {{vrf}} protocols ospf area {{ospf_area_id}} interface {{ospf_interface}} metric {{ospf_cost}}
set routing-instances {{vrf}} protocols ospf area {{ospf_area_id}} interface {{ospf_interface}} priority {{ospf_priority}}
delete routing-instances {{vrf}} protocols ospf area {{ospf_area_id}} interface {{ospf_interface}} disable 
| set routing-instances {{vrf}} protocols ospf area {{ospf_area_id}} interface {{ospf_interface}} disable
set routing-instances {{vrf}} protocols ospf area {{ospf_area_id}} interface {{ospf_interface}} authentication md5 {{ospf_auth_id}} key {{ospf_auth_password}}
| delete routing-instances {{vrf}} protocols ospf area {{ospf_area_id}} interface {{ospf_interface}} authentication
set routing-instances {{vrf}} protocols ospf area {{ospf_area_id}} interface {{ospf_interface}} bfd-liveness-detection minimum-interval {{bfd_interface_min_interval}}
set routing-instances {{vrf}} protocols ospf area {{ospf_area_id}} interface {{ospf_interface}} bfd-liveness-detection minimum-receive-interval {{bfd_interface_min_recieve_interval}}
set routing-instances {{vrf}} protocols ospf area {{ospf_area_id}} interface {{ospf_interface}} bfd-liveness-detection multiplier {{bfd_interface_multiplier}}
</pre>

*virtual-router* is a conversion of {{type}} set *L3VRF*  
*delete routing-instances {{vrf}} protocols ospf area {{ospf_area_id}} interface {{ospf_interface}} disable* is a conversion of {{ospf_interface_enabled}} set *true*  
*set routing-instances {{vrf}} protocols ospf area {{ospf_area_id}} interface {{ospf_interface}} disable* is a conversion of {{ospf_interface_enabled}} set *false*  
*set routing-instances {{vrf}} protocols ospf area {{ospf_area_id}} interface {{ospf_interface}} authentication* is a conversion of {{ospf_auth_enabled}} set *true*  
*delete routing-instances {{vrf}} protocols ospf area {{ospf_area_id}} interface {{ospf_interface}} authentication* is a conversion of {{ospf_auth_enabled}} set *false*  

<pre>
set routing-instances {{vrf}} routing-options instance-import {{vrf}}-route-target-import
set routing-instances {{vrf}} protocols ospf export {{ospf-export-policy}}
</pre>

### Junos 18.2R1-S2.1

#### CLI

<pre>
set routing-instances {{vrf}} interface {{interface-id}}
</pre>