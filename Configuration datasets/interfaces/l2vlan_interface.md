# L2VLAN interface

## URL

```
frinx-openconfig-interfaces:interfaces/interface={{l2vlan_if_name}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/interfaces/src/main/yang)

```javascript
{
    "interface": [
        {
            "name": "{{l2vlan_if_name}}",
            "config": {
                "type": "iana-if-type:l2vlan",
                "name": "{{l2vlan_if_name}}"
            }
        }
    ]
}
```

## OS Configuration Commands

### Ciena SAOS8

#### CLI

<pre>
cpu-interface sub-interface create cpu-subinterface {{l2vlan_if_name}}
</pre>

##### Unit

Link to github : [saos-unit](https://github.com/FRINXio/cli-units/tree/master/saos/saos8/saos-8-interface)
