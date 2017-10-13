# Configuration datasets

All URLs start with:

<pre>http://localhost:8181/restconf/config/network-topology:network-topology/topology/&lt;topo-name&gt;/node/&lt;node-id&gt;/yang-ext:mount/</pre>

- &lt;topo-name&gt; can be either <b>cli</b> or <b>unified</b>
- &lt;node-id&gt; mountpoint name

* [Configuration datasets](#configuration-datasets)
  * [Interfaces](#interfaces)
       * [<a href="Interfaces/subinterface_common.md">sub-interface</a>](#sub-interface)
       * [<a href="Interfaces/interface_common.md">interface</a>](#interface)
       * [<a href="Interfaces/interface_policy.md">interface policy</a>](#interface-policy)
       * [<a href="Interfaces/interface_acl.md">interface ACL</a>](#interface-acl)
     * [LAG interface](#lag-interface)
       * [<a href="Interfaces/LAG interfaces/bundle_common.md">bundle</a>](#bundle)
       * [<a href="Interfaces/LAG interfaces/bundle_bfd.md">bundle BFD</a>](#bundle-bfd)
       * [<a href="Interfaces/LAG interfaces/bundle_dampening.md">bundle damp</a>](#bundle-dampening)
     * [LAG member interface](#lag-member-interface)
       * [<a href="Interfaces/LAG member interfaces/bundle_member_common.md">bundle member</a>](#bundle-member)
       * [<a href="Interfaces/LAG member interfaces/interface_lacp.md">interface LACP</a>](#interface-lacp)
  * [Network Instances (VRFs)](#network-instances-vrfs)
     * [PROTOCOLS](#protocols)
       * [<a href="Network Instances/Protocols/bgp_neighbor.md">bgp neighbor</a>](#bgp-neighbor)
       * [<a href="Network Instances/Protocols/ospf_interface_cost.md">ospf interface cost</a>](#ospf-interface-cost)
       * [<a href="Network Instances/Protocols/ospf_metric.md">max metric</a>](#max-metric)
     * [MPLS](#mpls)
       * [<a href="Network Instances/MPLS/mpls_tunnel_load_share.md">tunnel load share</a>](#tunnel-load-share)
       * [<a href="Network Instances/MPLS/mpls_tunnel_autoroute.md">tunnel autoroute</a>](#tunnel-autoroute)
       * [<a href="Network Instances/MPLS/rsvp_bandwidth.md">rsvp bandwidth</a>](#rsvp-bandwidth)


## Interfaces

#### [sub-interface](Interfaces/subinterface_common.md)

#### [interface](Interfaces/interface_common.md)

#### [interface policy](Interfaces/interface_policy.md)

#### [interface ACL](Interfaces/interface_acl.md)

### LAG interface

#### [bundle](Interfaces/LAG%20interfaces/bundle_common.md)

#### [bundle BFD](Interfaces/LAG%20interfaces/bundle_bfd.md)

#### [bundle damp](Interfaces/LAG%20interfaces/bundle_dampening.md)

### LAG member interface

#### [bundle member](Interfaces/LAG%20member%20interfaces/bundle_member_common.md)

#### [interface LACP](Interfaces/LAG%20member%20interfaces/interface_lacp.md)

## Network Instances (VRFs)

### PROTOCOLS

#### [bgp neighbor](Network%20Instances/Protocols/bgp_neighbor.md)

#### [ospf interface cost](Network%20Instances/Protocols/ospf_interface_cost.md)

#### [max metric](Network%20Instances/Protocols/ospf_metric.md)

### MPLS

#### [tunnel load share](Network%20Instances/MPLS/mpls_tunnel_load_share.md)

#### [tunnel autoroute](Network%20Instances/MPLS/mpls_tunnel_autoroute.md)

#### [rsvp bandwidth](Network%20Instances/MPLS/rsvp_bandwidth.md)
