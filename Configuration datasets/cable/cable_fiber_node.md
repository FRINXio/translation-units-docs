# cable FIBER-NODE

## URL

```
frinx-openconfig-cable:cable/fiber-nodes/fiber-node={{fiber_node_id}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/cable/src/main/yang)

```javascript
{
    "fiber-node": [
        {
            "id": "{{fiber_node_id}}",
            "config": {
                "id": "{{fiber_node_id}}",
            },
            "cable-channels": {
                "cable-channel": [
                    {
                        "type": "{{cable_channel_type}}",
                        "config": {
                            "name": "{{downstream_cable_channel_name}}"
                        }
                    },
                    {
                        "type": "{{cable_channel_type}}",
                        "config": {
                            "name": "{{upstream_cable_channel_name}}"
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
cable fiber-node {{fiber_node_id}}
  {{cable_channel_type}} {{downstream_cable_channel_name}}
  {{cable_channel_type}} {{upstream_cable_channel_name}}
</pre>

{{upstream_cable_channel_name}} and {{upstream_cable_channel_name}} are in commands input with whitespace dividing name and number (Downstream-Cable 1/0/16)

##### Unit

Link to github : [ios-xe-unit](https://github.com/FRINXio/cli-units/tree/master/cable/fiber-node)