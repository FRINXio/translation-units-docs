# IETF L3VPN YANG 

## IETF YANG

```javascript
{
    "l3vpn-svc": [
        "vpn-services": {
            "vpn-service": [
                {
                    "vpn-id": <vrf>
                    "vpn-service-topology": any-to-any
                }
            ]
        }
		"sites": {
            "site": [
                {
                    "site-id": <site-id>
                }
                "site-network-accesses": {
            		"site-network-access": [
                		{
                    		"site-network-access-id": <site-network-access-id>
                        	"bearer": {
                            	"bearer-reference": <node-id>/<interface-id>
                        	}
                        	"routing-protocols": {
            					"routing-protocol": [
                					{
                    					"type": bgp
                    					"bgp": {
                            				"address-family": ipv4
                            				"autonomous-system": <remote-as>
                        				}
                					}
            					]
        					}
            				"ip-connection": [
                				{
                					"ipv4": {
                						"addresses": {
                        					"provider-address": <interface-ip>
                        					"customer-address": <neighbor-address>
                        					"prefix-length": <interface-mask>
                    					}
                    				}
            					}
            				]
                		}
            		]
        		}
            ]
        }
    ]
}
```

## OPENCONFIG YANG 

```javascript
{
    "network-instance": [
        {
            "config": {
                "name": "<vrf>"
                "type": "L3VRF" //matches vpws-instance-type in ietf
                "route-distinguisher": "auto"
                "enabled-address-families": "ipv4"
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
                                        "prefix": "<network-prefix>" // is a transformation of <interface-ip> and <interface-mask>
                                    }
                                }
                            ]
                        }
                        
                        "bgp": {
                            "global": {
                                "as": "<as-number>" //to be filled out based on reconciliation
                                "router-id": "<router-id>" //to be filled out based on reconciliation
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
                                                            "import-policy": "RPL_PASS_ALL"
                                                            "export-policy": "RPL_PASS_ALL
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
                            {<rt_exp_1>} //autoprovisioning
                        ]
                       }
                }
                {            
                    "config": {
                        "ext-community-set-name": "<vrf>-route-target-import-set"
                        "ext-community-set-member": [
                            {<rt_imp_1>} //autoprovisioning
                        ]
                       }
                }
            ]
        }
    }
}
```