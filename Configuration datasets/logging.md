# Logging (syslog)

## URL

```
logging:logging/interfaces/interface/<intf-id>
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/logging/src/main/yang)

```javascript
{
    "interface": [
        {
            "id": <intf-id>
            "config": {
                "id": <intf-id>
                "enabled-logging-for-event": [
                    {
                        "event-name": "event-types:LINK_UP_DOWN"
                    }
                ]
            }
            "interface-ref": {
                "config": {
                    "interface": <intf-id>
                }
            }
        }
    ]
}

```

## OS Configuration Commands

### Cisco IOS XR 5.3.4

#### CLI

<pre>
interface bundle-ether &lt;intf-id&gt;
 logging events link-status
</pre>

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [xr-unit]()