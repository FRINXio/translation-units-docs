# Multiprotocol Label Switching - Tunnel

## URL

```
openconfig-network-instance:network-instances/network-instance/<ni-name>/openconfig-mpls:mpls/lsps/constrained-path/tunnels/tunnel/<tunnel-id>
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/mpls/src/main/yang)

[extensions to MPLS YANG model](https://github.com/FRINXio/openconfig/tree/master/network-instance/src/main/yang)

```javascript
{
    "tunnel": [
         {
             "name": <tunnel-id>
             "config": {
                 "name": <tunnel-id>
                 "shortcut-eligible": <true|false>
                 "metric-type": "openconfig-mpls-types:LSP_METRIC_ABSOLUTE"
                 "metric": <metric>
             }
             "cisco-mpls-te-extension:cisco-mpls-te-extension": {
                "config": {
                    "load-share": <load-share>
                }
             }
         }
    ]
}
```

## OS Configuration Commands

### Cisco IOS XR 5.3.4

#### CLI

<pre>
interface tunnel-te &lt;tunnel-id&gt;
 load-share &lt;load-share&gt;
 autoroute announce
 metric absolute &lt;metric&gt;
</pre>

*autoroute announce* is conversion of *"shortcut-eligible": true*  
*no autoroute announce* is conversion of *"shortcut-eligible": false*  

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [xr-unit]()

### Junos 15.1F-6.9

#### CLI

<pre>
set protocols mpls label-switched-path &lt;tunnel-id&gt;
set protocols mpls label-switched-path &lt;tunnel-id&gt; metric &lt;metric&gt;
</pre>

*set protocols mpls label-switched-path &lt;tunnel-id&gt;* is conversion of *"shortcut-eligible": true*  

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit]()

