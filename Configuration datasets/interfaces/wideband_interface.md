# WIDEBAND interface

## URL

```
frinx-openconfig-interfaces:interfaces/interface={{wideband_ifc_name}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/interfaces/src/main/yang)

```javascript
{
    "interface": [
       {
            "name": "{{wideband_ifc_name}}",
            "config": {
                "name": "{{wideband_ifc_name}}"
            },
            "frinx-cisco-if-extension:statistics": {
                "config": {
                    "load-interval": "{{load_interval}}"
                }
            },
            "frinx-rphy-if-extension:cable": {
                "rf-channels": {
                    "channel-list": "{{rf_channels_list}}",
                    "bandwidth-percent": "{{rf_channels_bw}}"
                },
                "config": {
                    "bundle": "{{cable_bundle}}"
                }
            }
        }
    ]
}
```

## OS Configuration Commands

### IOS XE 16

#### CLI

<pre>
interface {{wideband_ifc_name}}
  cable bundle {{cable_bundle}}
  load-interval {{load_interval}}
  cable rf-channels channel-list {{rf_channels_list}}
  bandwidth-percent {{rf_channels_bw}}
</pre>

##### Unit

Link to github : [ios-xe-unit](https://github.com/FRINXio/cli-units/tree/master/ios/interface)