# Open Shortest Path First v3 (OSPFv3)

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance=default/protocols/protocol=frinx%2Dopenconfig%2Dpolicy%2Dtypes%3AOSPFv3,{{ospfv3}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/ospf/src/main/yang)

```javascript
{
   "protocol": [
        {
            "identifier": "frinx-openconfig-policy-types:OSPFv3",
            "name": {{ospfv3}}
            "config": {
                "identifier": "frinx-openconfig-policy-types:OSPFv3",
                "name": {{ospfv3}}
            },
            "ospfv3": {
                "global": {
                    "stub-router": {
                        "config": {
                            "set": true,
                            "advertise-lsas-types": "STUB_ROUTER_MAX_METRIC",
                            "always": true
                        }
                    }
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
router ospfv3 {{ospfv3}}
 stub-router router-lsa max-metric
  always
</pre>

{{advertise-lsas-types}} value STUB_ROUTER_MAX_METRIC is to be converted to *max-metric*  
{{advertise-lsas-types}} value STUB_ROUTER_R_BIT is to be converted to *r-bit*  
{{advertise-lsas-types}} value STUB_ROUTER_V6_BIT is to be converted to *v6-bit*  

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/ospf)

