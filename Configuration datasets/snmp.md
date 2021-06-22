# Simple Network Management Protocol (SNMP)

## URL

```
frinx-snmp:snmp/interfaces/interface={{snmp_intf_if}}
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

## URL

```
frinx-snmp:snmp/views/view={{view_name}}
```

## OPENCONFIG YANG

```javascript
{
    "frinx-snmp:view": [
        {
            "name": "{{view_name}}",
            "config": {
                "name": "{{view_name}}",
                "mib": [
                    {
                        "name": "{{mib_name}}",
                        "inclusion": "included|excluded"
                    }
                ]
            }
        }
    ]
}
```

## URL

```
frinx-snmp:snmp/communities/community={{community_name}}
```

## OPENCONFIG YANG

```javascript
{
    "frinx-snmp:community": [
        {
            "name": "{{community_name}}",
            "config": {
                "name": "{{community_name}}",
                "access-list": "{{access_list_number}}",
                "access": "ro|rw",
                "view": "{{view_name}}"
            }
        }
    ]
}
```

## OS Configuration Commands

### Cisco IOS Classic (15.2(4)S5) / XE (15.3(3)S2)

#### CLI

<pre>
snmp-server view {{view_name}} {{mib_name}} {{inclusion}}
snmp-server community {{community_name}} view {{view_name}} {{access}} {{access_list_number}}
</pre>

##### Unit

Link to github : [ios-unit](https://github.com/FRINXio/cli-units/tree/master/ios/snmp)

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


*enabled:true* is a conversion of snmp set *enabled*

*enabled:false* is a conversion of snmp set *disabled*

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/snmp)

### Junos 17.3R1.10

#### CLI

<pre>
set interfaces {{snmp_intf_if}} traps
</pre>

##### Unit

Link to github : [junos-unit](https://github.com/FRINXio/unitopo-units/tree/master/junos/junos-17/junos-17-snmp-unit)
