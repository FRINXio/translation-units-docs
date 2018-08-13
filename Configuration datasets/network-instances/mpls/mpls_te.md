# Multiprotocol Label Switching - Traffic Engineering (MPLS-TE)

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance/default/mpls
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/mpls/src/main/yang)

[extensions to MPLS YANG model](https://github.com/FRINXio/openconfig/tree/master/network-instance/src/main/yang)

```javascript
{
    "mpls" {
        "te-global-attributes:" {
            "frinx-cisco-mpls-te-extension": {
                "config" {
                    "enabled" : true
                }
            }
        },
        "te-interface-attributes": {
            "interface": [
                {
                    "interface-id": "{{mpls_intf_id}}",
                    "config": {
                        "interface-id": "{{mpls_intf_id}}"
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
mpls traffic-eng
 interface {{mpls_intf_id}}
</pre>

- "enabled" MUST be set to true when any te-configuration is pushed
- "enabled" set to false, will ignore any additional configuration in the PUT request and will result in 'no mpls traffic-eng'

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/mpls)

### Junos 17.3R1.10

#### CLI

<pre>
set interfaces {{mpls_intf_id}} unit 0 family mpls
</pre>

##### Unit

Link to github : [junos-unit](https://github.com/FRINXio/unitopo-units/tree/master/junos/junos-17-mpls-unit)
