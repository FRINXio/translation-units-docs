# Hot Standby Router Protocol (HSRP)

## URL

```
frinx-openconfig-hsrp:hsrp/interfaces/interface/{{hsrp_intf_id}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/hsrp/src/main/yang)

```javascript
{
    "interface": [
        {
            "interface-id": "{{hsrp_intf_id}}",
            "config": {
                "interface-id": "{{hsrp_intf_id}}"
                "minimum-delay": {{hsrp_minimum_delay}},
                "reload-delay": {{hsrp_reload_delay}}
            },
            "hsrp-group": [
                "address-family": "ipv4",
                "virtual-router-id":{{hsrp_group_number}},
                "config": {
                    "address-family": "ipv4",
                    "virtual-router-id": {{hsrp_group_number}},
                    "version": {{hsrp_version}},
                    "priority": {{hsrp_priority}}
                }
            ]
        }
    ]
}
```

## OS Configuration Commands

### Cisco IOS XR 5.3.4

#### CLI

<pre>
router hsrp
 interface {{hsrp_intf_id}}
  hsrp delay minimum {{hsrp_minimum_delay}} reload {{hsrp_reload_delay}}
  address-family ipv4
   hsrp {{hsrp_group_number}} version {{hsrp_version}}
    priority {{hsrp_priority}}
</pre>

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/hsrp)

