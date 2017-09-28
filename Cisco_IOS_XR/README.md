# Cisco IOS XR translation units

[Link to Postman collection](https://github.com/FRINXio/postman-collections)

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

#### Local Routing

| Translation unit  | YANG model |  Command  | Status |
| ----------------- |------------| --------- | ------ |
| Translate-unit-ios-xr-lr-Openconfig | [openconfig-local-routing.yang](https://github.com/FRINXio/openconfig/tree/master/local-routing) | [show static routes](base/show_static_routes.md) | draft |

