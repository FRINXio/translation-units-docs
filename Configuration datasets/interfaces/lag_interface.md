# Link Aggregation Group (bundle) interface

## URL

```
openconfig-interfaces:interfaces/interface/<intf-id>
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/interfaces/src/main/yang)

```javascript
{
    "interface": [
        {
            "name": "<intf-id>"
            "config": {
                "type": "iana-if-type:ieee8023adLag"
                "enabled": <true/false>
                "mtu": <mtu>
                "description": <desc>
                "name": <intf-id>
            }
            "subinterfaces": {
                "subinterface": [
                    {
                        "index": 0
                        "config": {
                            "index": 0
                        }
                        "openconfig-if-ip:ipv4": {
                            "addresses": {
                                "address": [
                                    {
                                        "ip": <ip>
                                        "config": {
                                            "ip": <ip>
                                            "prefix-length": <prefix>
                                        }
                                    }
                                ]
                            }
                        }
                    }
                ]
            }
            "damping:damping": {
                "config": {
                    "enabled": <true/false>,
                    "half-life": <half-life>,
                    "reuse": <reuse>,
                    "suppress": <suppres>,
                    "max-supress": <max-supress>
                }
            }
            "cisco-if-extension:statistics": {
                "load-interval": <load-interval>
            }
            "openconfig-if-aggregate:aggregation": {
                "config": {
                    "min-links": <min-links>
                    "juniper-if-aggregate-extension:link-speed": <link_speed>
                }
                "bfd:bfd": {
                    "config": {
                        "local-address": <local_ip>
                        "destination-address": <destination_ip>
                        "multiplier": <multiplier>
                        "min-interval": <min-int>
                    }
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
 description &lt;desc&gt;
 mtu &lt;mtu&gt;
 ipv4 address &lt;ip&gt; &lt;subnet&gt;
 dampening
  dampening &lt;half-life&gt; &lt;reuse&gt; &lt;supress&gt; &lt;max-supress&gt;
 load-interval &lt;load-interval&gt;
 bundle minimum-active links &lt;min-links&gt;
 bfd mode ietf
 bfd address-family ipv4 destination &lt;destination_ip&gt;
 bfd address-family ipv4 fast-detect
 bfd address-family ipv4 minimum-interval &lt;min-int&gt;
 bfd address-family ipv4 multiplier &lt;multiplier&gt;
 no shutdown
</pre>

&lt;subnet&gt; is conversion of &lt;prefix&gt;  
*no shutdown* is conversion of *"enabled": true*  
*shutdown* is conversion of *"enabled": false*

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [xr-unit]()

### Junos 15.1F-6.9

#### CLI

<pre>
set interfaces &lt;intf-id&gt; description &lt;desc&gt;
set interfaces &lt;intf-id&gt; mtu &lt;mtu&gt;
set interfaces &lt;intf-id&gt; unit 0 family inet address &lt;ip&gt/&lt;prefix&gt;
set interfaces &lt;intf-id&gt; aggregated-ether-options minimum-links &lt;min-links&gt;
set interfaces &lt;intf-id&gt; aggregated-ether-options bfd-liveness-detection neighbor &lt;destination_ip&gt;
set interfaces &lt;intf-id&gt; aggregated-ether-options bfd-liveness-detection local-address &lt;local_ip&gt;
set interfaces &lt;intf-id&gt; aggregated-ether-options bfd-liveness-detection minimum-interval &lt;min-int&gt;
set interfaces &lt;intf-id&gt; aggregated-ether-options bfd-liveness-detection multiplier &lt;multiplier&gt;
set interfaces &lt;intf-id&gt; aggregated-ether-options link-speed &lt;link_speed&gt;
delete interface &lt;intf-id&gt; disable
</pre>

*delete interface &lt;intf-id&gt; disable* is conversion of *"enabled": true*  
*set interface &lt;intf-id&gt; disable* is conversion of *"enabled": false*

**Device does not support damping on LAG interface.**

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit]()

