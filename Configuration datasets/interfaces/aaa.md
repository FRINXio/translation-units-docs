# AAA - Authentication Authorization Accounting


## URL

```
frinx-openconfig-aaa:aaa
```

## OPENCONFIG YANG

```javascript
{
    "frinx-openconfig-aaa:aaa": {
        "authentication": {
            "users": {
                "user": [
                    {
                        "username": "{{user_name}}",
                        "config": {
                            "password-hashed": "{{user_hashed_password}}",
                            "frinx-huawei-aaa-extension:service-type": [
                                "{{user_service_types}}"
                            ],
                            "frinx-huawei-aaa-extension:privilege-level": "{{user_privilege_level}}"
                        }
                    }
                ]
            }
        },
        "frinx-huawei-aaa-extension:domain-list": {
            "domain": [
                {
                    "name": "{{domain_name}}",
                    "config": {
                        "radius-server": "{{radius_name}}",
                        "accounting-scheme": "{{accounting_name}}",
                        "authentication-scheme": "{{authentication_name}}"
                    }
                }
            ]
        },
        "frinx-huawei-aaa-extension:radius": {
            "template": [
                {
                    "name": "{{radius_name}}",
                    "config": {
                        "retransmit-attempts": "{{radius_retransmit_attempts}}",
                        "secret-key-hashed": "{{radius_hashed_secret_key}}",
                        "authentication-data": [
                            {
                                "source-address": "{{source_ip_address}}",
                                "vrf-name": "{{vrf_name}}"
                            }
                        ]
                    }
                }
            ]
        },
        "frinx-huawei-aaa-extension:authentication-schemes": {
            "authentication": [
                {
                    "name": "{{authentication_name}}",
                    "config": {
                        "authentication": {
                            "config": {
                                "authentication-method": [
                                    "{{authentication_method}}"
                                ]
                            }
                        }
                    }
                }
            ]
        },
        "frinx-huawei-aaa-extension:accounting-schemes": {
            "account": [
                {
                    "name": "{{accounting_name}}",
                    "config": {
                        "fail-policy": "{{fail_policy_type}}",
                        "fail-policy-mode": "{{fail_policy_mode}}",
                        "accounting": {
                            "config": {
                                "accounting-method": [
                                    "{{accounting-method}}"
                                ]
                            }
                        }
                    }
                }
            ]
        }
    }
}
```

## OS Configuration Commands

### Huawei NE5000E (V800R009C10SPC310)

#### CLI

<pre> 
aaa                                        
 authentication-scheme {{authentication_name}}             
  authentication-mode {{authentication_method}} 

 accounting-scheme {{accounting_name}}
  accounting-mode {{accounting_method}}                  
  accounting {{fail_policy_type}} {{fail_policy_mode}}  

 domain {{domain_name}}                           
  authentication-scheme {{authentication_name}}        
  accounting-scheme {{accounting_name}}         
  radius-server {{radius_name}}                  
 
 local-user lab password irreversible-cipher {{user_hashed_password}}
 local-user lab privilege level {{user_privilege_level}}       
 local-user lab service-type {{user_service_types}}

radius 
 radius-server template {{radius_name}}
 radius-server shared-key cipher {{radius_hashed_secret_key}}
 radius-server authentication {{source_ip_address}} 1812 vpn-instance {{vrf_name}} source LoopBack 0 weight 80
 radius-server authentication {{source_ip_address}} 1812 source LoopBack 0 weight 80
 radius-server retransmit {{radius_retransmit_attempts}}
</pre>

*local, radius* is conversions of {{authentication_method}} set to "authentication-method"  
*local, radius* is conversions of {{accounting_method}} set to "accounting-method"  
*start-fail* is conversion of {{fail_policy_type}} set to "fail-policy"  
*online* is conversion of {{fail_policy_mode}} set to "fail-policy-mode"
*telnet, terminal, ssh, ftp* is conversions of {{user_service_types}} set to "frinx-huawei-aaa-extension:service-type"  
*1-15* is conversion of {{user_privilege_level}} set to "frinx-huawei-aaa-extension:privilege-level"

##### Unit

Link to github : [huawei-unit](https://github.com/FRINXio/cli-units/tree/master/huawei/aaa)