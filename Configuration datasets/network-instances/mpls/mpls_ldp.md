# Multiprotocol Label Switching - Label Distribution Protocol (MPLS LDP)

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance/default/mpls/signaling-protocols/ldp
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/mpls/src/main/yang)

[extensions to MPLS YANG model](https://github.com/FRINXio/openconfig/tree/master/network-instance/src/main/yang)

```javascript
{
    "ldp": {
        "global": {
            "config": {
                "frinx-mpls-ldp-extension:enabled": true|false
            }
        },
        "interface-attributes": {
            "interface": [
                {
                    "interface-id": "{{ldp_intf_id}}",
                    "config": {
                        "interface-id": "{{ldp_intf_id}}"
                    }
                }
            ]
        }
    }
}

```

## OS Configuration Commands

### Cisco IOS XR 5.3.4

#### CLI

<pre>
mpls ldp
 interface {{ldp_intf_id}}
</pre>

- "enabled" MUST be set to true when any ldp-configuration is pushed
- "enabled" set to false, will ignore any additional configuration in the PUT request and will result in 'no mpls ldp'

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/mpls)
