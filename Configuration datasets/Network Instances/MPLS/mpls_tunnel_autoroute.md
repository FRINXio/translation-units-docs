# Autoroute configuration

## URL

```
openconfig-network-instance:network-instances/network-instance/<ni-name>/openconfig-mpls:mpls/lsps/constrained-path/tunnels/tunnel/<tunnel-id>
```

## OPENCONFIG YANG

```javascript
{
    "tunnel": [
         {
             "config": {
                 "name": <tunnel-id>
             }
             "auto-route": {
                 "config": {
                    "set": <true/false>
                    "metric": <metric>
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
  autoroute announce
   metric absolute &lt;metric&gt;
</pre>
---

*autoroute announce* is conversion of *"enabled": true*
*no autoroute announce* is conversion of *"enabled": false*

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [xr-unit]()

### Junos 15.1F5

#### CLI


---
<pre>
set protocols mpls label-switched-path &lt;tunnel-id&gt; metric &lt;metric&gt;
</pre>
---

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit]()
