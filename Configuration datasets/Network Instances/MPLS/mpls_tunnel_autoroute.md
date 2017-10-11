# Autoroute configuration

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
             "auto-route": {
                 "config": {
                    "set": true
                 }
             }
         }
    ]
}

TODO: auto-route not implemented, need to augment
```

## OS Configuration Commands

#### Cisco IOS XR 5.4.3

---
<pre>
interface tunnel-te &lt;tunnel-id&gt;
  autoroute announce
</pre>
---

#### Junos

---
<pre>
set protocols mpls label-switched-path &lt;tunnel-id&gt; metric &lt;metric&gt;
</pre>
---
