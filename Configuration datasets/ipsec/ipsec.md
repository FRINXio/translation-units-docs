# Internet Protocol Security (IPsec)

## URL

```
frinx-ipsec:ipsec/client-groups/client-group/{{group_name}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/ipsec/src/main/yang)

```javascript
{
    "client-group": [
        {
            "group-name": "{{group_name}}",
            "config": {
                "group-name": "{{group_name}}"
            },
            "clients": {
                "client": [
                    {
                        "client-id": "{{client_id}}",
                        "config": {
                            "client-id": "{{client_id}}",
                            "enabled": {{client_enabled}}
                        },
                        "client-identification": {
                            "config": {
                                "idi-host": "{{idi_fqdn}}",
                                "peer-prefix": "{{peer_prefix}}"
                            }
                        },
                        "security-association": {
                            "tunneling": {
                                "config": {
                                    "private-interface-name": "{{private_interface_name}}",
                                    "private-service-id": {{private_service_id}},
                                    "tunnel-template-id": {{tunnel_template_id}}
                                }
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
### NOKIA SROS 16.0

#### CLI

<pre>
/configure
  ipsec
    client-db "{{group_name}}" create
      client {{client_id}} create
        private-interface "{{private_interface_name}}"
        private-service {{private_service_id}}
        tunnel-template {{tunnel_template_id}}
        client-identification
          idi string-type fqdn string-value "{{idi_fqdn}}"
          peer-ip-prefix {{peer_prefix}}
        no shutdown | shutdown
</pre>

*no shutdown* is a conversion of {{client_enabled}} set to true  
*shutdown* is a conversion of {{client_enabled}} set to false  
