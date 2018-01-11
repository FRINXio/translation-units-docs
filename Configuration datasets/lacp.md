# Link Aggregation Control Protocol (LACP)

## URL

```
frinx-openconfig-interfaces:interfaces/interface/{{lacp_intf_id}}/frinx-openconfig-if-ethernet:ethernet
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/lacp/src/main/yang)

```javascript
{
    "frinx-openconfig-if-ethernet:ethernet": {
        "config": {
            "frinx-openconfig-if-aggregate:aggregate-id": "{{lacp_bundle_id}}",
            "lacp-mode": "{{lacp_mode}}",
            "interval": "{{lacp_interval}}"
	}
    }
}
```

## OS Configuration Commands

### Cisco IOS XR 5.3.4

#### CLI

<pre>
interface {{lacp_intf_id}}
 bundle id {{lacp_bundle_id}} mode {{lacp_mode}}
 lacp period short | no lacp period short
</pre>

*lacp persiod short* is a conversion of {{lacp_interval}} set to *frinx-openconfig-lacp:FAST*  
*no lacp persiod short* is a conversion of {{lacp_interval}} set to *frinx-openconfig-lacp:SLOW* 

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/interface)

### Junos 17.3R1.10

#### CLI

<pre>
set interfaces {{lacp_bundle_id}} aggregated-ether-options lacp {{lacp_mode}}
set interfaces &lt;bundle_id&gt; aggregated-ether-options lacp periodic {{lacp_interva}}
</pre>

##### Unit

NOT IMPLEMENTED

Link to github : [junos-unit]()
