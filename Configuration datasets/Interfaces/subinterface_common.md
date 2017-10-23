# Subinterface common configuration

## URL

```
openconfig-interfaces:interfaces/interface/<intf-id>/subinterfaces/subinterface/0
```

## OPENCONFIG YANG

```javascript
{
    "subinterface": [
        {
            "index": 0
            "config": {
                "index": 0
            }
            "ipv4": {
                "addresses": {
                    "address": {
                        "ip":
                        "config": {
                            "ip": <ip>
                            "prefix-length": <prefix>
                        }
                    }
                }
            }
        }
    ]
}
```

## OS Configuration Commands

### Cisco IOS Classic (15.2(4)S5) / XE (15.3(3)S2)

---
<pre>
configure terminal
interface &lt;intf-id&gt;
ip address &lt;ip&gt; &lt;subnet&gt;
exit
exit
</pre>
---

##### Unit

Unit version range: 3.1.1.rc1-frinx

Link to github : [ios-unit](https://github.com/FRINXio/cli-units/tree/master/ios/interface)

### Cisco IOS XR 5.3.4

#### CLI

---
<pre>
interface &lt;intf-id&gt;
 ipv4 address &lt;ip&gt; &lt;subnet&gt;
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [xr-unit][]

### Junos 15.1F5

#### CLI

---
<pre>
set interfaces &lt;intf-id&gt;
set interfaces &lt;intf-id&gt; unit 0 family inet address &lt;ip&gt/&lt;prefix&gt;l
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit][]
