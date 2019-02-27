# Logging (syslog)

## URL

```
frinx-logging:logging/interfaces/interface/{{intf_id}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/logging/src/main/yang)

```javascript
{
    "interface": [
        {
            "interface-id": "{{intf_id}}",
            "config": {
                "interface-id": "{{intf_id}}",
                "enabled-logging-for-event": [
                    {
                        "event-name": "frinx-event-types:LINK_UP_DOWN"
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
interface {{intf_id}}
 logging events link-status
</pre>

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/logging)

### Cisco IOS XR 6.6.1

#### CLI

<pre>
interface {{intf_id}}
 logging events link-status
</pre>

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/unitopo-units/tree/master/xr/xr-7-logging)
