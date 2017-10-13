# Bundle interface BFD configuration

## URL

```
openconfig-interfaces/interfaces/interface/<intf-id>
```

## OPENCONFIG YANG

```javascript
{
    "interface": [
        {
            "config": {
                "type": "iana-if-type:ieee8023adLag",
                "enabled": true,
                "name": "<intf-id>"
            }
            "aggregation": {
                "config": {
                }
            }
        }
    ]
}

//TODO: bfd configuration not available in openconfig

```

## OS Configuration Commands

### Cisco IOS XR 5.3.4

#### CLI

---
<pre>
interface &lt;intf-id&gt;
  bfd mode ietf
  bfd address-family ipv4 destination &lt;ip&gt;
  bfd address-family ipv4 fast-detect
  bfd address-family ipv4 minimum-interval &lt;min-int&gt;
  bfd address-family ipv4 multiplier &lt;multiplier&gt;
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [xr-unit][]

### Junos 15.1F5

#### CLI

---
<pre>
set interfaces &lt;intf-id&gt; aggregated-ether-options bfd-liveness-detection neighbor &lt;ip&gt;
set interfaces &lt;intf-id&gt; aggregated-ether-options bfd-liveness-detection local-address &lt;ip&gt;
set interfaces &lt;intf-id&gt; aggregated-ether-options bfd-liveness-detection minimum-interval &lt;min-int&gt;
set interfaces &lt;intf-id&gt; aggregated-ether-options bfd-liveness-detection multiplier &lt;multiplier&gt;
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit][]
