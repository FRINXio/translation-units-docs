# BGP RIB

## URL

```
openconfig-rib-bgp:bgp-rib
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/rib/src/main/yang)

```javascript
{
    "bgp-rib": {
        "afi-safis": {
            "afi-safi": [
                {
                    "afi-safi-name": "openconfig-bgp-types:IPV4_UNICAST",
                    "ipv4-unicast": {
                        "loc-rib": {
                            "routes": {
                                "route": [
                                    {
                                        "prefix": "<prefix1>",
                                        "origin": "i",
                                        "path-id": "0",
                                        "state": {
                                            "prefix": "<prefix1>",
                                            "valid-route": true
                                        }
                                    },
                                    {
                                        "prefix": "<prefix2>",
                                        "origin": "i",
                                        "path-id": "0",
                                        "state": {
                                            "prefix": "<prefix2>",
                                            "valid-route": true
                                        }
                                    }
                                ]
                            }
                        }
                    }
                }
            ]
        }
    }
}
```


## OS Commands

### Cisco IOS Classic (15.2(4)S5) / XE (15.3(3)S2)

#### CLI

---
<pre>
R121#sh ip bgp
BGP table version is 3, local router ID is 9.9.9.9
Status codes: s suppressed, d damped, h history, * valid, > best, i - internal,
              r RIB-failure, S Stale, m multipath, b backup-path, f RT-Filter,
              x best-external, a additional-path, c RIB-compressed,
Origin codes: i - IGP, e - EGP, ? - incomplete
RPKI validation codes: V valid, I invalid, N Not found

     Network          Next Hop            Metric LocPrf Weight Path
 *>  <b><mark>&lt;prefix1&gt;</b></mark>      <b><mark>0.0.0.0</b></mark>                   0         <b><mark>32768</b></mark>  <b><mark>i</b></mark>
 *>  <b><mark>&lt;prefix2&gt;</b></mark>      <b><mark>192.168.56.122</b></mark>           0             <b><mark>0</b></mark>  <b><mark>65777 i</b></mark>

R121#sh ip bgp | section &lt;prefix1&gt;
 *>  <b><mark>&lt;prefix1&gt;</b></mark>      <b><mark>0.0.0.0</b></mark>                   0         <b><mark>32768</b></mark>  <b><mark>i</b></mark>
</pre>
---

'*' (valid route) translates to <b>"valid-route" : true</b>  
'i' (internal) translates to <b>"origin": "i"</be>

##### Unit

Unit version range: 3.1.1.rc1-frinx

Link to github : [ios-unit](https://github.com/FRINXio/cli-units/tree/master/ios/rib)
