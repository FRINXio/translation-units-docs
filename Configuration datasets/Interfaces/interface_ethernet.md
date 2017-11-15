# Common interface configuration

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
                "type": "iana-if-type:ethernetCsmacd"
                "enabled": <true/false>
                "mtu": <mtu>
                "description": <desc>
                "name": <intf-id>
                "cisco-if-extension:statistics": {
                    "load-interval": <load-interval>
                }
            }
            "hold-time": {
                "config": {
                    "up": <up>
                    "down": <down>
                }
            }
            "ethernet": {
                "config": {
                    "openconfig-if-aggregate:aggregate-id": <bundle-id>
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
                    "config": {
                        "load-interval": <load_interval>
                    }
                }
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
        }
    ]
}
```

## OS Configuration Commands

### Cisco IOS Classic (15.2(4)S5) / XE (15.3(3)S2)

<pre>
interface &lt;intf-id&gt;
 description &lt;descr&gt;
 mtu &lt;mtu&gt;
 ip address &lt;ip&gt; &lt;subnet&gt;
 dampening
  dampening &lt;half-life&gt; &lt;reuse&gt; &lt;supress&gt; &lt;max-supress&gt;
 no shutdown
</pre>

&lt;subnet&gt; is conversion of &lt;prefix&gt;  
*no shutdown* is conversion of *"enabled": true*  
*shutdown* is conversion of *"enabled": false*  
*no dampening* is conversion of *"enabled": false*  
*dampening* is conversion od *"enabled": true*


##### Unit

Unit version range: 3.1.1.rc1-frinx

Link to github : [ios-unit](https://github.com/FRINXio/cli-units/tree/master/ios/interface)

### Cisco IOS XR 5.3.4

#### CLI

<pre>
interface &lt;intf-id&gt;
 description &lt;desc&gt;
 mtu &lt;mtu&gt;
 ipv4 address &lt;ip&gt; &lt;subnet&gt;
 dampening
  dampening &lt;half-life&gt; &lt;reuse&gt; &lt;supress&gt; &lt;max-supress&gt;
 carrier-delay up &lt;up&gt; down &lt;down&gt;
 load-interval &lt;load-interval&gt;
 bundle-id &lt;bundle-id&gt; mode on
 no shutdown
</pre>

&lt;subnet&gt; is conversion of &lt;prefix&gt;  
*no shutdown* is conversion of *"enabled": true*  
*shutdown* is conversion of *"enabled": false*

##### Unit

Unit version range: 3.1.1.rc1-frinx

Link to github : [xr-unit]()

### Junos 15.1F-6.9

#### CLI

<pre>
set interfaces &lt;intf-id&gt; description &lt;desc&gt;
set interfaces &lt;intf-id&gt; mtu &lt;mtu&gt;
set interfaces &lt;intf-id&gt; unit 0 family inet address &lt;ip&gt/&lt;prefix&gt;
set interfaces &lt;intf-id&gt; damping enable
set interfaces &lt;intf-id&gt; damping half-life &lt;half-life&gt;
set interfaces &lt;intf-id&gt; damping max-suppress &lt;max-supress&gt;
set interfaces &lt;intf-id&gt; damping reuse &lt;reuse&gt;
set interfaces &lt;intf-id&gt; damping suppress &lt;supress&gt;
set interfaces &lt;intf-id&gt; hold-time up &lt;up&gt; down &lt;down&gt;
set interfaces &lt;intf-id&gt; gigether-options 802.3ad &lt;bundle-id&gt;
delete interface &lt;intf-id&gt; disable
</pre>

*delete interface &lt;intf-id&gt; disable* is conversion of *"enabled": true*  
*set interface &lt;intf-id&gt; disable* is conversion of *"enabled": false*

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit]()

### Brocade (V5.6.0fT163)

#### CLI

<pre>
interface &lt;intf-id&gt;
  port-name &lt;desc&gt;
  enable | disable
</pre>

*enable* is conversion of *"enabled": true*  
*disable* is conversion of *"enabled": false*

