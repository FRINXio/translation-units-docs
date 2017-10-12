# Configuration datasets

All URLs start with:

<pre>http://localhost:8181/restconf/config/network-topology:network-topology/topology/&lt;topo-name&gt;/node/&lt;node-id&gt;/yang-ext:mount/</pre>

- &lt;topo-name&gt; can be either <b>cli</b> or <b>unified</b>
- &lt;node-id&gt; mountpoint name

## Interfaces

##### [sub-interface](Interfaces/subinterface_common.md)

##### [interface](Interfaces/interface_common.md)

##### [interface policy](Interfaces/interface_policy.md)

##### [interface LACP](Interfaces/interface_lacp.md)

##### [interface ACL](Interfaces/interface_acl.md)

### LAG interface

##### [bundle](Interfaces/LAG%20interfaces/bundle_common.md)
##### [bundle BFD](Interfaces/LAG%20interfaces/bundle_bfd.md)

### LAG member interface

##### [bundle member](Interfaces/LAG%20member%20interfaces/bundle_member_common.md)

## Network Instances (VRFs)

### PROTOCOLS

##### [bgp neighbor](Network%20Instances/Protocols/bgp_neighbor.md)

##### [ospf interface cost](Network%20Instances/Protocols/ospf_interface_cost.md)

##### [max metric](Network%20Instances/Protocols/ospf_metric.md)

### MPLS

##### [tunnel load share](Network%20Instances/MPLS/mpls_tunnel_load_share.md)

##### [tunnel autoroute](Network%20Instances/MPLS/mpls_tunnel_autoroute.md)

##### [rsvp bandwidth](Network%20Instances/MPLS/rsvp_bandwidth.md)
