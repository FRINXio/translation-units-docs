# show ip bgp

## REST call

```
GET
http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-rib-bgp:bgp-rib

```

## REST response body

```
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
                                        "prefix": "10.5.5.0/24",
                                        "origin": "i",
                                        "path-id": "0",
                                        "state": {
                                            "prefix": "10.5.5.0/24",
                                            "valid-route": true
                                        }
                                    },
                                    {
                                        "prefix": "10.7.7.0/24",
                                        "origin": "i",
                                        "path-id": "0",
                                        "state": {
                                            "prefix": "10.7.7.0/24",
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
 *>  <b><mark>10.5.5.0/24</b></mark>      <b><mark>0.0.0.0</b></mark>                   0         <b><mark>32768</b></mark>  <b><mark>i</b></mark> 
 *>  <b><mark>10.7.7.0/24</b></mark>      <b><mark>192.168.56.122</b></mark>           0             <b><mark>0</b></mark>  <b><mark>65777 i</b></mark> 
R121#
</pre>

   