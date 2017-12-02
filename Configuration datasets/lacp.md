# Link Aggregation Control Protocol (LACP)

## URL

```
openconfig-lacp:lacp/lacp-lag-member:lag-member-interfaces/lag-member-interface/<intf-id>
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/snmp/src/main/yang)

```javascript
{
    "lag-member-interface": [
        {
            "name": <intf-id>
            "interval": "openconfig-lacp:<FAST|SLOW>"
            "lacp-mode": "openconfig-lacp:<ACTIVE|PASSIVE>"
        }
    ]
}

```

## OS Configuration Commands

### Cisco IOS XR 5.3.4

#### CLI

<pre>
interface bundle-ether &lt;intf-id&gt;
 bundle id <bundle_id> mode <active|passive>
 lacp period short
</pre>

*<bundle_id>* is not defined by user but is found automatically based
on interface reference
*lacp persiod short* is conversion of *"lacp-mode": "openconfig-lacp:ACTIVE"*
*no lacp persiod short* is conversion of *"lacp-mode": "openconfig-lacp:PASSIVE"*

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [xr-unit]()

### Junos 15.1F-6.9

#### CLI

<pre>
set interfaces <bundle_id> aggregated-ether-options lacp <active|passive>
set interfaces <bundle_id> aggregated-ether-options lacp periodic <fast|slow>
</pre>

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit]()
