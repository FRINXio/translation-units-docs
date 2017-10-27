# Tunnel load-share configuration

## URL

```
openconfig-network-instance:network-instances/network-instance/<ni-name>/openconfig-mpls:mpls/lsps/constrained-path/tunnels/tunnel/<tunnel-id>
```

## OPENCONFIG YANG

```javascript
{
    "tunnel": [
         {
             "name": <tunnel-id>
             "config": {
                 "name": <tunnel-id>
             }
             "bandwidth": {
                 "config": {
                    "set-bandwidth": <bandwidth>
                 }
             }
         }
    ]
}
```

## OS Configuration Commands

### Cisco IOS XR 5.3.4

#### CLI

---
<pre>
interface tunnel-te &lt;tunnel-id&gt;
 load-share &lt;bandwidth&gt;
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [xr-unit][]

### Junos 15.1F5

#### CLI

---
<pre>
UNSUPPORTED
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit][]
