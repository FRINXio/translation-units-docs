# Tunnel load-share configuration

## URL

```
openconfig-network-instance:network-instances/network-instance/<ni-name>/openconfig-mpls:mpls/lsps/constrained-path/tunnels/tunnel/<tunnel-id>
```

## OPENCONFIG YANG

```json
{
    "tunnel": [
         {
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

### Cisco IOS XR (note:range 5.4.3 )

---
<pre>
interface tunnel-te &lt;tunnel-id&gt;
 load-share &lt;bandwidth&gt;
</pre>
---

### Junos

---
<pre>
set protocols mpls label-switched-path &lt;tunnel-id&gt;
</pre>
---

