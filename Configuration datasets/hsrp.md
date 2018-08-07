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
                ]
            },
            "subinterfaces": {
                "subinterface": [
                    {
                        "index": 0,
                        "config": {
                            "index": 0
                        }
                    }
                ]
            },
            "delay": {
                "config": {
                    "minimum-delay": {{hsrp_minimum_delay}},
                    "reload-delay": {{hsrp_reload_delay}}
                }
            },
            "afi-safis": {
                "afi-safi": [
                    "config": {
                        "afi-safi-name": {{hsrp_afi_safi_name}} //ipv4 | ipv6
                    }
                     "ipv4|ipv6": {
                        "groups": {
                            "group": [
                                {
                                     "group-number": {{hsrp_group_number}},
                                     "config": {
                                         "group-number": {{hsrp_group_number}},
                                         "version": {{hsrp_version}},
                                         "priority": {{hsrp_priority}}
                                     }
                                }
                            ]
                        }
                    }
                ]
            }
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
  address-family ipv4/ipv6
   hsrp {{hsrp_group_number}} version {{hsrp_version}}
    priority {{hsrp_priority}}
</pre>

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/hsrp)

