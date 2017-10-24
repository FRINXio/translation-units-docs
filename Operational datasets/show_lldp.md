# show lldp
  
## REST call

```
http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/<node-id>/yang-ext:mount/openconfig-lldp:lldp

```

## REST response body

```
{
    "interfaces": {
	"interface": [
	    "name": "Et0/0"
            "config": {
		"name": "Et0/0"
	    }
  	    "state": {
	        "name": "Et0/0"
	    }
	    "neighbors": {
	        "neighbor": [
		    "id": "Router2"
       		    "state": {
			"id": "Router2"
			"port-id": "Et0/1"				
  		    }
		 ]
	     }
	]
    }
}
```

---

<pre>
R121# show lldp neighbors


Capability codes:

    (R) Router, (B) Bridge, (T) Telephone, (C) DOCSIS Cable Device

    (W) WLAN Access Point, (P) Repeater, (S) Station, (O) Other


Device ID           Local Intf     Hold-time  Capability      Port ID

<b><mark>Router2</b></mark>            <b><mark>Et0/0</b></mark>           150        R              <b><mark>Et0/1</b></mark> 


Total entries displayed: 1


</pre>



