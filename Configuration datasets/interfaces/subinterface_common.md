# Subinterface common configuration

## URL

```
frinx-openconfig-interfaces:interfaces/interface/<intf-id>/subinterfaces/subinterface/<index>
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/interfaces/src/main/yang)

```javascript
{
    "subinterface": [
        {
            "index": <index>
            "config": {
                "index": <index>
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
interface &lt;intf-id&gt;.&lt;index&gt;
 ip address &lt;ip&gt; &lt;subnet&gt;
</pre>

&lt;subnet&gt; is conversion of &lt;prefix&gt;

---

##### Unit

Unit version range: 3.1.1.rc1-frinx

Link to github : [ios-unit](https://github.com/FRINXio/cli-units/tree/master/ios/interface)

### Cisco IOS XR 5.3.4

#### CLI

---
<pre>
interface &lt;intf-id&gt;.&lt;index&gt;
 ipv4 address &lt;ip&gt; &lt;subnet&gt;
</pre>

&lt;subnet&gt; is conversion of &lt;prefix&gt;

---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [xr-unit]()

### Junos 15.1F5

#### CLI

---
<pre>
set interfaces &lt;intf-id&gt; unit &lt;index&gt; family inet address &lt;ip&gt/&lt;prefix&gt;
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit]()
