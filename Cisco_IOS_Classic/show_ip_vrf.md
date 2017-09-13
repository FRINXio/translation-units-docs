# show ip vrf

## REST call

```
GET
http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/IOS1/yang-ext:mount/openconfig-interfaces:interfaces
```

## REST response body

```
{
    "vrfs": {
        "vrf": [
            {
                "id": "bambi"
            }
        ]
    }
}
```


---

<pre>
R121#sh ip vrf              
  Name                             Default RD          Interfaces
  <b><mark>bambi</b></mark>                           <b><mark>65000:1</b></mark>             <b><mark>Lo99</b></mark>


R121#sh ip vrf detail bambi 
VRF bambi (VRF Id = 1); default RD 65000:1; default VPNID &lt;not set&gt;
  Interfaces:
    Lo99                    
VRF Table ID = 1
  Export VPN route-target communities
    RT:<b><mark>65000:2</b></mark>            
  Import VPN route-target communities
    RT:<b><mark>65000:2</b></mark>            
  No import route-map
  No global export route-map
  No export route-map
  VRF label distribution protocol: not configured
  VRF label allocation mode: per-prefix

R121#
</pre>



