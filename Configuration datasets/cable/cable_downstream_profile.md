# cable DOWNSTREAM CONTROLLER-PROFILE

## URL

```
frinx-openconfig-cable:cable/downstreams/downstream-cable-profile={{controller_profile_id}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/cable/src/main/yang)

```javascript
{
    "downstream-cable-profile": [
        {
            "id": "{{controller_profile_id}}",
            "config": {
                "max-carrier": "{{controller_profile_max_carrier}}",
                "max-ofdm-spectrum": "{{controller_profile_spectrum}}"
            },
            "rf-channels": {
                "rf-channel": [
                    {
                        "id": "{{rf_channel_id}}",
                        "rf-chan-type": {
                            "config": {
                                "rf-type": "{{rf_channel_type}}"
                            }
                        },
                        "config": {
                            "frequency": "{{rf_channel_frequency}}",
                            "docsis-channel-id": "{{rf_channel_docsis}}",
                            "rf-output": "{{rf_channel_output}}",
                            "qam-profile": "{{rf_channel_qam}}"
                        }
                    },
                    {
                        "id": "{{rf_channel_id}}",
                        "config": {
                            "docsis-channel-id": "{{rf_channel_docsis}}"
                        },
                        "ofdm": {
                            "config": {
                                "channel-profile": "{{ofdm_channel}}",
                                "width": "{{ofdm_width}}",
                                "start-frequency": "{{ofdm_start_frequency}}",
                                "plc": "{{ofdm_plc}}"
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

### IOS XE 16

#### CLI

<pre>
cable downstream controller-profile {{controller_profile_id}}
 max-carrier {{controller_profile_max_carrier}}
 max-ofdm-spectrum {{controller_profile_spectrum}}
 rf-chan {{rf_channel_id}}
  type {{rf_channel_type}}
  qam-profile {{rf_channel_qam}}
  frequency {{rf_channel_frequency}}
  rf-output {{rf_channel_output}}
  docsis-channel-id {{rf_channel_docsis}}
 rf-chan {{rf_channel_id}}
  docsis-channel-id {{rf_channel_docsis}}
  ofdm channel-profile {{ofdm_channel}} start-frequency {{ofdm_start_frequency}} width {{ofdm_width}} plc {{ofdm_plc}}
</pre>

{{rf_channel_id}} can be either a single number or a list of numbers (0 31 which represents all the values from 0 to 31)

##### Unit

Link to github : [ios-xe-unit](https://github.com/FRINXio/cli-units/tree/master/cable/downstream)