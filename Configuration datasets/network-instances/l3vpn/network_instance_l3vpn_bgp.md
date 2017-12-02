# L3VPN configuration

## URL

```
openconfig-network-instance:network-instances/network-instance/<vrf>
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
openconfig-routing-policy:routing-policy/defined-sets<vrf>
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
openconfig-routing-policy:routing-policy/policy-definitions<vrf>
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