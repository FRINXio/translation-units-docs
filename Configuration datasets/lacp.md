# Link Aggregation Control Protocol (LACP)

## URL

```
frinx-openconfig-lacp:lacp/lacp-lag-member:lag-member-interfaces/lag-member-interface/<intf-id>
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/snmp/src/main/yang)

```javascript
{
    "lag-member-interface": [
        {
            "name": <intf-id>
            "interval": "frinx-openconfig-lacp:<FAST|SLOW>"
            "lacp-mode": "frinx-openconfig-lacp:<ACTIVE|PASSIVE>"
        }
    ]
}

```

## OS Configuration Commands

### Cisco IOS XR 5.3.4

#### CLI

<pre>
interface &lt;intf-id&gt;
 bundle id &lt;bundle_id&gt; mode &lt;active|passive&gt;
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
set interfaces &lt;bundle_id&gt; aggregated-ether-options lacp &lt;active|passive&gt;
set interfaces &lt;bundle_id&gt; aggregated-ether-options lacp periodic &lt;fast|slow&gt;
</pre>

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit]()
