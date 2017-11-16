# Simple Network Management Protocol (SNMP)

## URL

```
snmp:snmp/interfaces/interface/<intf-id>
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/snmp/src/main/yang)

```javascript
{
    "interface": [
        {
            "id": <intf-id>
            "config": {
                "id": <intf-id>
                "enabled-trap-for-event": [
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
snmp-server interface &lt;intf-id&gt; notification linkupdown
</pre>

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [xr-unit]()

### Junos 15.1F-6.9

#### CLI

<pre>
set interfaces &lt;intf-id&gt; traps
</pre>

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit]()
