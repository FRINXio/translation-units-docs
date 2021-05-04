# NetFlow

## URL

```
frinx-netflow:netflow/interfaces/interface={{netflow_intf_id}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/netflow/src/main/yang)

```javascript
{
    "interface": [
        {
            "id": "{{netflow_intf_id}}",
            "config": {
                "id": "{{netflow_intf_id}}"
            },
            "ingress-flows": {
                "ingress-flow": [
                    {
                        "netflow-type": "NETFLOW_IPV4|NETFLOW_IPV6|NETFLOW_MPLS",
                        "config": {
                            "netflow-type": "NETFLOW_IPV4|NETFLOW_IPV6|NETFLOW_MPLS",
                            "monitor-name": "{{i_netflow_monitor}}",
                            "sampler-name": "{{i_netflow_sampler}}"
                        }
                    }
                ]
            },
            "egress-flows": {
                "egress-flow": [
                    {
                        "netflow-type": "NETFLOW_IPV4|NETFLOW_IPV6|NETFLOW_MPLS",
                        "config": {
                            "netflow-type": "NETFLOW_IPV4|NETFLOW_IPV6|NETFLOW_MPLS",
                            "monitor-name": "{{e_netflow_monitor}}",
                            "sampler-name": "{{e_netflow_sampler}}"
                        }
                    }
                ]
            }
        }
    ]
}
```

## OS Configuration Commands

### Cisco IOS XR 5.3.4

#### CLI

<pre>
interface {{netflow_intf_id}}
  flow ipv4|ipv6|mpls monitor {{i_netflow_monitor}} sampler {{i_netflow_sampler}} ingress
  flow ipv4|ipv6|mpls monitor {{e_netflow_monitor}} sampler {{e_netflow_sampler}} egress
</pre>

Assumption is that monitor map and sampler map configuration already exist on a device.

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/netflow)