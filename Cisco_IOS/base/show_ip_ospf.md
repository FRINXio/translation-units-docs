# show ip ospf

## REST call

```

http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/IOS1/yang-ext:mount/openconfig-ospfv2:ospfv2

```

## REST response body

```
 
"ospfs": {
	"ospf": [
		"global": {
			"config": {
				"router-id": "9.9.9.9"
			}
		}
		"areas": {
			"area": {
				"area-key": 70
			}
			"area": {
				"area-key": 90
			}
		}
	]
	"ospf": [
		"global": {
			"config": {
				"router-id": "192.168.56.121"
			}
		}
		"areas": {
			"area": {
				"area-key": 20
			}
		}
	]
}

```


---

<pre>
R121#sh ip ospf
 Routing Process "<b><mark>ospf 200</b></mark>" with ID <b><mark>9.9.9.9</b></mark>
 Start time: 01:59:55.128, Time elapsed: 00:01:26.652
 Supports only single TOS(TOS0) routes
 Supports opaque LSA
 Supports Link-local Signaling (LLS)
 Supports area transit capability
 Supports NSSA (compatible with RFC 3101)
 Event-log enabled, Maximum number of events: 1000, Mode: cyclic
 Router is not originating router-LSAs with maximum metric
 Initial SPF schedule delay 5000 msecs
 Minimum hold time between two consecutive SPFs 10000 msecs
 Maximum wait time between two consecutive SPFs 10000 msecs
 Incremental-SPF disabled
 Minimum LSA interval 5 secs
 Minimum LSA arrival 1000 msecs
 LSA group pacing timer 240 secs
 Interface flood pacing timer 33 msecs
 Retransmission pacing timer 66 msecs
 Number of external LSA 0. Checksum Sum 0x000000
 Number of opaque AS LSA 0. Checksum Sum 0x000000
 Number of DCbitless external and opaque AS LSA 0
 Number of DoNotAge external and opaque AS LSA 0
 Number of areas in this router is 1. 1 normal 0 stub 0 nssa
 Number of areas transit capable is 0
 External flood list length 0
 IETF NSF helper support enabled
 Cisco NSF helper support enabled
 Reference bandwidth unit is 100 mbps
    Area <b><mark>70</b></mark>
        Number of interfaces in this area is 1 (1 loopback)
	Area has no authentication
	SPF algorithm last executed 00:00:50.840 ago
	SPF algorithm executed 1 times
	Area ranges are
	Number of LSA 1. Checksum Sum 0x007F46
	Number of opaque link LSA 0. Checksum Sum 0x000000
	Number of DCbitless LSA 0
	Number of indication LSA 0
	Number of DoNotAge LSA 0
	Flood list length 0
    Area <b><mark>90</b></mark>
        Number of interfaces in this area is 1 (1 loopback)
	Area has no authentication
	SPF algorithm last executed 00:00:31.564 ago
	SPF algorithm executed 1 times
	Area ranges are
        Number of LSA 1. Checksum Sum 0x00C3F9
	Number of opaque link LSA 0. Checksum Sum 0x000000
	Number of DCbitless LSA 0
	Number of indication LSA 0
	Number of DoNotAge LSA 0
	Flood list length 0
	
 Routing Process "<b><mark>ospf 100</b></mark>" with ID <b><mark>192.168.56.121</b></mark>
 Start time: 00:26:19.132, Time elapsed: 01:35:02.676
 Supports only single TOS(TOS0) routes
 Supports opaque LSA
 Supports Link-local Signaling (LLS)
 Supports area transit capability
 Supports NSSA (compatible with RFC 3101)
 Event-log enabled, Maximum number of events: 1000, Mode: cyclic
 Router is not originating router-LSAs with maximum metric
 Initial SPF schedule delay 5000 msecs
 Minimum hold time between two consecutive SPFs 10000 msecs
 Maximum wait time between two consecutive SPFs 10000 msecs
 Incremental-SPF disabled
 Minimum LSA interval 5 secs
 Minimum LSA arrival 1000 msecs
 LSA group pacing timer 240 secs
 Interface flood pacing timer 33 msecs
 Retransmission pacing timer 66 msecs
 Number of external LSA 0. Checksum Sum 0x000000
 Number of opaque AS LSA 0. Checksum Sum 0x000000
 Number of DCbitless external and opaque AS LSA 0
 Number of DoNotAge external and opaque AS LSA 0
 Number of areas in this router is 1. 1 normal 0 stub 0 nssa
 Number of areas transit capable is 0
 External flood list length 0
 IETF NSF helper support enabled
 Cisco NSF helper support enabled
 Reference bandwidth unit is 100 mbps
    Area <b><mark>20</b></mark>
        Number of interfaces in this area is 3 (1 loopback)
	Area has no authentication
	SPF algorithm last executed 01:11:09.108 ago
	SPF algorithm executed 7 times
	Area ranges are
	Number of LSA 3. Checksum Sum 0x01FFE3
	Number of opaque link LSA 0. Checksum Sum 0x000000
	Number of DCbitless LSA 0
	Number of indication LSA 0
	Number of DoNotAge LSA 0
	Flood list length 0
</pre>


