<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**

- [Configuration datasets](#configuration-datasets)
    - [Interfaces](#interfaces)
        - [enable interface](#enable-interface)
    - [LAG interface](#lag-interface)
        - [bundle](#bundle)
    - [LAG member interface](#lag-member-interface)
        - [bundle member](#bundle-member)
  - [Network Instances (VRFs)](#network-instances-vrfs)
    - [PROTOCOLS](#protocols)
        - [bgp neighbor](#bgp-neighbor)
        - [ospf interface cost](#ospf-interface-cost)
        - [max metric](#max-metric)
    - [MPLS](#mpls)
        - [tunnel load share](#tunnel-load-share)
        - [tunnel autoroute](#tunnel-autoroute)
        - [rsvp bandwidth](#rsvp-bandwidth)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Configuration datasets

All URLs start with:

<pre>http://localhost:8181/restconf/config/network-topology:network-topology/topology/&lt;topo-name&gt;/node/&lt;node-id&gt;/yang-ext:mount/</pre>

- &lt;topo-name&gt; can be either <b>cli</b> or <b>unified</b>
- &lt;node-id&gt; mountpoint name

### Interfaces

##### [interface](Interfaces/interface_common.md)

### LAG interface

##### [bundle](Interfaces/bundle_common.md)

### LAG member interface

##### [bundle member](Interfaces/bundle_member_common.md)

## Network Instances (VRFs)

### PROTOCOLS

##### [bgp neighbor](Network%20Instances/Protocols/bgp_neighbor.md)

##### [ospf interface cost](Network%20Instances/Protocols/ospf_interface_cost.md)

##### [max metric](Network%20Instances/Protocols/ospf_metric.md)

### MPLS

##### [tunnel load share](Network%20Instances/MPLS/mpls_tunnel_load_share.md)
##### [tunnel autoroute](Network%20Instances/MPLS/mpls_tunnel_autoroute.md)
##### [rsvp bandwidth](Network%20Instances/MPLS/rsvp_bandwidth.md)


