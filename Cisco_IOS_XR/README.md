# Cisco IOS XR translation units

## Show commands for IOS xr 6

### Interface

| Translation unit  | YANG model |  Command  | Status | 
| ----------------- |------------| --------- | ------ |
| [Translate-unit-xr6-interface-Openconfig](https://NNN) | [openconfig-interfaces.yang](https://github.com/FRINXio/openconfig/tree/master/interfaces) | [show ip interface brief](base/show_ip_interface_brief.md) | completed |
|  | | [show run interface &lt;intf id&gt;](base/show_run_interface.md) | completed |
|  | | [show interface &lt;intf id&gt;](base/show_interface.md) | completed |


### IP information

| Translation unit  | YANG model |  Command  | Status | 
| ----------------- |------------| --------- | ------ |
| [Translate-unit-xr6-interface-Openconfig](https://NNN) | [openconfig-if-ip.yang](https://github.com/FRINXio/openconfig/tree/master/interfaces) | [show ip interface](base/show_ip_interface.md) | completed |
|  | | [show ipv6 interface](base/show_ipv6_interface.md) | completed |

### Local Routing

| Translation unit  | YANG model |  Command  | Status |
| ----------------- |------------| --------- | ------ |
| xr-6-lr-unit | [openconfig-local-routing.yang](https://github.com/FRINXio/openconfig/tree/master/local-routing) | [show static routes](base/show_static_routes.md) | draft |


### PROTOCOLS

| Translation unit  | YANG model |  Command  | Status |
| ----------------- |------------| --------- | ------ |
| xr-6-bgp-unit | [openconfig-bgp.yang](https://github.com/FRINXio/openconfig/tree/master/bgp) | [show router bgp](base/show_router_bgp.md) | completed |
| xr-6-ospf-unit | [openconfig-ospf.yang](https://github.com/FRINXio/openconfig/tree/master/ospf) | [show router ospf](base/show_router_ospf.md) | completed |


### Platform

| Translation unit  | YANG model |  Command  | Status |
| ----------------  |------------| --------- | ------ |
| xr-6-platform-unit | [openconfig-platform.yang](https://github.com/FRINXio/openconig/tree/master/platform) | [show_inventory](base/show_inventory.md) | draft |

---

## Configuration commands for IOS xr v5.3.4

### Interfaces

| Translation unit  | YANG model |  Command  | Status | 
| ----------------- |------------| --------- | ------ |
| Translate-unit-ios-xr-interfaces-Openconfig | [openconfig-interfaces.yang](https://github.com/FRINXio/openconfig/tree/master/interfaces) | [enable interface](base/enable_interface.md) | draft |
|  | | [configure bundle](base/configure_bundle.md) | draft
|  | | [configure bundle member](base/configure_bundle_member.md) | draft |
|  | | [configure autoroute](base/configure_autoroute.md) | needs augment |

### Network Instances

#### PROTOCOLS

| Translation unit  | YANG model |  Command  | Status | 
| ----------------- |------------| --------- | ------ |
| Translate-unit-ios-xr-bgp-Openconfig | [openconfig-bgp.yang](https://github.com/FRINXio/openconfig/tree/master/bgp) | [configure bgp neighbor](base/configure_bgp_neighbor.md) | draft |
| Translate-unit-ios-xr-ospf-Openconfig | [openconfig-ospf.yang](https://github.com/FRINXio/openconfig/tree/master/ospf) | [configure ospf interface cost](base/configure_ospf_interface_cost.md) | draft |
| | | [configure ospf](base/configure_ospf.md) | draft |

#### MPLS

| Translation unit  | YANG model |  Command  | Status |
| ----------------- |------------| --------- | ------ |
| Translate-unit-ios-xr-mpls-Openconfig | openconfig-mpls.yang | [configure load share](../base/configure_load_share.md) | draft |
| | | [configure rsvp](base/configure_rsvp.md) | draft |


