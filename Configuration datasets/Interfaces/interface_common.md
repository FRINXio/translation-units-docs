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
                "type": "iana-if-type:<interface-type>"
                "enabled": <true/false>
                "mtu": <mtu>
                "description": <desc>
                "name": <intf-id>
                "cisco-if-extension:statistics": {
                    "load-interval": <load-interval>
                }
                "interfaces-damp:damp": {
                    "enabled": <true/false>,
                    "half-life": <half-life>,
                    "reuse": <reuse>,
                    "suppress": <suppres>,
                    "max-supress": <max-supress>
                }
            }
            "hold-time": {
                "config": {
                    "up": <up>
                    "down": <down>
                }
            }
            "logging": {
                "config": {
                    "link-status": {}
                }
            }
            "subinterfaces": {
                "subinterface": [
                    {
                        "index": 0
                        "config": {
                            "index": 0
                        }
                        "ipv4": {
                            "addresses": {
                                "address": [
                                    {
                                        "ip":
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

// TODO: SNMP traps not supported in OpenConfig
```

## OS Configuration Commands

### Cisco IOS Classic (15.2(4)S5) / XE (15.3(3)S2)

---
<pre>
interface &lt;intf-id&gt;
 description &lt;descr&gt;
 mtu &lt;mtu&gt;
 ip address &lt;ip&gt; &lt;subnet&gt;
 logging events link-status
 dampening
  dampening &lt;half-life&gt; &lt;reuse&gt; &lt;supress&gt; &lt;max-supress&gt;
 no shutdown
</pre>

&lt;subnet&gt; is conversion of &lt;prefix&gt;  
*no shutdown* is conversion of *"enabled": true*  
*shutdown* is conversion of *"enabled": false*
*no dampening* is conversion of *"enabled": false*
*dampening* is conversion od *"enabled": true*

---

##### Unit

Unit version range: 3.1.1.rc1-frinx

Link to github : [ios-unit](https://github.com/FRINXio/cli-units/tree/master/ios/interface)

### Cisco IOS XR 5.3.4

#### CLI

---
<pre>
interface &lt;intf-id&gt;
 description &lt;desc&gt;
 mtu &lt;mtu&gt;
 carrier-delay up &lt;up&gt; down &lt;down&gt;
 ipv4 address &lt;ip&gt; &lt;subnet&gt;
 logging &lt;events&gt; &lt;link-status&gt;
 load-interval &lt;load-interval&gt;
 no shutdown
 snmp-server traps snmp linkup
</pre>

&lt;subnet&gt; is conversion of &lt;prefix&gt;  
*no shutdown* is conversion of *"enabled": true*  
*shutdown* is conversion of *"enabled": false*

---

##### Unit

Unit version range: 3.1.1.rc1-frinx

Link to github : [xr-unit](https://github.com/FRINXio/unitopo-units/tree/master/xr-6-interface-unit)

### Junos 15.1F5

#### CLI

---
<pre>
set interfaces &lt;intf-id&gt; description &lt;desc&gt;
set interfaces &lt;intf-id&gt; mtu &lt;mtu&gt;
set interfaces &lt;intf-id&gt; hold-time up &lt;up&gt; down &lt;down&gt;
set interfaces &lt;intf-id&gt; unit 0 family inet address &lt;ip&gt/&lt;prefix&gt;
set event-options policy log-on-snmp-trap-link-up events snmp_trap_link_up
set interfaces &lt;intf-id&gt; damping enable
set interfaces &lt;intf-id&gt; damping half-life &lt;half-life&gt;
set interfaces &lt;intf-id&gt; damping max-suppress &lt;max-supress&gt;
set interfaces &lt;intf-id&gt; damping reuse &lt;reuse&gt;
set interfaces &lt;intf-id&gt; damping suppress &lt;supress&gt;
delete interface &lt;intf-id&gt; disable
set interfaces &lt;intf-id&gt; traps
</pre>

*delete interface &lt;intf-id&gt; disable* is conversion of *"enabled": true*  
*set interface &lt;intf-id&gt; disable* is conversion of *"enabled": false*

---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit]()
