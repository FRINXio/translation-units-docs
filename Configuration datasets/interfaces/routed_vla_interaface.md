# ROUTED VLAN interface

## URL

```
frinx-openconfig-interfaces:interfaces/interface/{{routed_ifc_name}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/interfaces/src/main/yang)

```javascript
{
    "interface": [
        {
            "name": "{{routed_ifc_name}}",
            "config": {
                "type": "IF_ROUTED_VLAN",
                "name": "{{routed_ifc_name}}"
            }
        }
    ]
}
```

## OS Configuration Commands

### Ciena SAOS8

#### CLI

<pre>
cpu-interface sub-interface create cpu-subinterface {{routed_ifc_name}}
</pre>

##### Unit

Link to github : [saos-unit](https://github.com/FRINXio/cli-units/tree/master/saos/saos8/saos-8-interface)
