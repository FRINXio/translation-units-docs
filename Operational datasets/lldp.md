# Show LLDP interfaces and neighbors

## URL

```
openconfig-lldp:lldp
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/lldp/src/main/yang)

```javascript
{
    "lldp": {
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
R121#sh lldp interface
&lt;intf-id&gt;
    Tx: enabled
    Rx: enabled
    Tx state: IDLE
    Rx state: WAIT FOR FRAME

R121#sh lldp neighbor &lt;intf-id&gt; detail | include System Name
System Name: &lt;nei-id&gt;
Port id: &lt;port-id&gt;
</pre>
---

##### Unit

Unit version range: 3.1.1.rc1-frinx

Link to github : [ios-unit](https://github.com/FRINXio/cli-units/tree/master/ios/lldp)

### Cisco XR 6.1.2

#### Netconf

---
<pre>
RP/0/0/CPU0:PE1#show lldp neighbor
Tue Oct 31 12:50:27.962 UTC
Capability codes:
        (R) Router, (B) Bridge, (T) Telephone, (C) DOCSIS Cable Device
        (W) WLAN Access Point, (P) Repeater, (S) Station, (O) Other

Device ID       Local Intf          Hold-time  Capability     Port ID
&lt;nei-id&gt; Gi0/0/0/3           120        R               &lt;port-id&gt;

Total entries displayed: 1
</pre>
---

#### Device YANG
Link to github : [xml-sample](https://github.com/FRINXio/unitopo-units/blob/master/xr-6-lldp-unit/src/test/resources/lldp-oper.xml)

##### Unit

Unit version range: 3.1.1.rc1-frinx

Link to github : [xr-unit](https://github.com/FRINXio/unitopo-units/tree/master/xr-6-lldp-unit)