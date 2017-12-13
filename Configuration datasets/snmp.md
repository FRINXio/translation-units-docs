# Simple Network Management Protocol (SNMP)

## URL

```
frinx-snmp:snmp/interfaces/interface/<intf-id>
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/snmp/src/main/yang)

```javascript
{
    "interface": [
        {
            "interface-id": "<intf-id>",
            "config": {
                "interface-id": "<intf-id>",
                "enabled-trap-for-event": [
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
snmp-server interface &lt;intf-id&gt; notification linkupdown
</pre>

Does work only for subinterfaces.

##### Unit

Unit version range: 3.1.1.rc5

Link to github : [xr-unit]()

### Junos 15.1F-6.9

#### CLI

<pre>
set interfaces &lt;intf-id&gt; traps
</pre>

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit]()
