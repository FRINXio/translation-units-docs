# Simple Network Management Protocol (SNMP)

## URL

```
frinx-snmp:snmp/interfaces/interface/{{snmp_intf_if}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/snmp/src/main/yang)

```javascript
{
    "interface": [
        {
            "interface-id": "{{snmp_intf_if}}",
            "config": {
                "interface-id": "{{snmp_intf_if}}",
                "enabled-trap-for-event": [
                    {
                        "event-name": "frinx-event-types:LINK_UP_DOWN"
                        "enabled": true/false            
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

By default enabled on all interfaces. To disable, use:

<pre>
snmp-server interface {{snmp_intf_if}} 
 notification linkupdown disable
</pre>

To enable disabled interfaces use:

<pre>
snmp-server interface {{snmp_intf_if}} 
 no notification linkupdown disable
</pre>

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/snmp)

### Junos 17.3R1.10

#### CLI

<pre>
set interfaces {{snmp_intf_if}} traps
</pre>

##### Unit

Link to github : [junos-unit](https://github.com/FRINXio/unitopo-units/tree/master/junos/junos-17-snmp-unit)
