# Multiprotocol Label Switching - Traffic Engineering (MPLS-TE)

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance/default/mpls/te-interface-attributes/interface/{{mpls_intf_id}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/mpls/src/main/yang)

[extensions to MPLS YANG model](https://github.com/FRINXio/openconfig/tree/master/network-instance/src/main/yang)

```javascript
{
    "interface": [
        {
            "interface-id": "{{mpls_intf_id}}",
            "config": {
                "interface-id": "{{mpls_intf_id}}"
            }
        }
    ]
}
```

## OS Configuration Commands

### Cisco IOS XR 5.3.4

#### CLI

<pre>
mpls traffic-eng
 interface {{mpls_intf_id}}
</pre>

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/mpls)

### Junos 17.3R1.10

#### CLI

<pre>
set interfaces {{mpls_intf_id}} unit 0 family mpls
</pre>

##### Unit

Link to github : [junos-unit](https://github.com/FRINXio/unitopo-units/tree/master/junos/junos-17-mpls-unit)
