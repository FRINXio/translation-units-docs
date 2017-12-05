# Multiprotocol Label Switching - Traffic Engineering (MPLS-TE)

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance/<ni-name>/mpls/te-interface-attributes/interface/<intf-id>
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/mpls/src/main/yang)

[extensions to MPLS YANG model](https://github.com/FRINXio/openconfig/tree/master/network-instance/src/main/yang)

```javascript
{
    "interface": [
        {
            "interface-id": "<intf-id>",
            "config": {
                "interface-id": <intf-id>
            }
        }
    ]
}
```

## OS Configuration Commands

### Cisco IOS XR 5.3.4

#### CLI

<pre>
mpls traffic-eng
 interface &lt;intf-id&gt;
</pre>

##### Unit

Unit version range: 3.1.1.rc4

Link to github : [xr-unit]()

### Junos 15.1F-6.9

#### CLI

<pre>
set interfaces &lt;intf-id&gt; unit 0 family mpls
</pre>

##### Unit

Unit version range: NOT IMPLEMENTED

Link to github : [junos-unit]()

