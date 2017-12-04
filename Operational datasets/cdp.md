# Show CDP interfaces and neighbors

## URL

```
frinx-cdp:cdp
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/cdp/src/main/yang)

```javascript
{
    "cdp": {
        "interfaces": {
            "interface": [
                {
                    "name": "<intf-id>",
                    "state": {
                        "name": "<intf-id>",
                        "enabled": true
                    },
                    "config": {
                        "name": "<intf-id>",
                        "enabled": true
                    },
                    "neighbors": {
                        "neighbor": [
                            {
                                "id": "<nei-id>",
                                "state": {
                                    "port-id": "<port-id>"
                                }
                            }
                        ]
                    }
                }
            ]
        }
    }
}
```


## OS Commands

### Cisco IOS Classic (15.2(4)S5) / XE (15.3(3)S2)

#### CLI

---
<pre>
R121#show cdp interface
&lt;intf-id&gt; is up, line protocol is up
  Encapsulation ARPA
  Sending CDP packets every 60 seconds
  Holdtime is 180 seconds

R121#sh lldp neighbor &lt;intf-id&gt; detail | include System Name
Device ID: &lt;nei-id&gt;
Interface: FastEthernet0/0,  Port ID (outgoing port): &lt;port-id&gt;
</pre>
---

##### Unit

Unit version range: 3.1.1.rc1-frinx

Link to github : [ios-unit](https://github.com/FRINXio/cli-units/tree/master/ios/cdp)

### Cisco XR 6.1.2

#### Netconf

---
<pre>
RP/0/0/CPU0:PE1#show cdp neighbor
Tue Oct 31 13:05:52.238 UTC
Capability Codes: R - Router, T - Trans Bridge, B - Source Route Bridge
                  S - Switch, H - Host, I - IGMP, r - Repeater

Device ID       Local Intrfce    Holdtme Capability Platform  Port ID
&lt;nei-id&gt; Mg0/0/CPU0/0     160     R          Cisco 720 &lt;port-id&gt;
</pre>
---

#### Device YANG
Link to github : [xml-sample](https://github.com/FRINXio/unitopo-units/blob/master/xr-6-cdp-unit/src/test/resources/cdp-oper.xml)

##### Unit

Unit version range: 3.1.1.rc1-frinx

Link to github : [xr-unit](https://github.com/FRINXio/unitopo-units/tree/master/xr-6-cdp-unit)