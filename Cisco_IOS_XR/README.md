# Cisco IOS XR translation units

[Link to Postman collection](https://github.com/FRINXio/postman-collections)

## Configuration commands

### Interfaces

| Translation unit  | YANG model |  Command  | Status | 
| ----------------- |------------| --------- | ------ |
| Translate-unit-ios-xr-interfaces-Openconfig | [openconfig-interfaces.yang](https://github.com/FRINXio/openconfig/tree/master/interfaces) | [enable interface](enable_interface.md) | draft |
|  | | [configure bundle](configure_bundle.md) | draft
|  | | [configure bundle member](configure_bundle_member.md) | draft |
|  | | [configure autoroute](configure_autoroute.md) | needs augment |

### Network Instances

#### PROTOCOLS

| Translation unit  | YANG model |  Command  | Status | 
| ----------------- |------------| --------- | ------ |
| Translate-unit-ios-xr-bgp-Openconfig | [openconfig-bgp.yang](https://github.com/FRINXio/openconfig/tree/master/bgp) | [configure bgp neighbor](configure_bgp_neighbor.md) | draft |
| Translate-unit-ios-xr-ospf-Openconfig | [openconfig-ospf.yang](https://github.com/FRINXio/openconfig/tree/master/ospf) | [configure ospf interface cost](configure_ospf_interface_cost.md) | draft |
| | | [configure ospf](configure_ospf.md) | draft |

#### MPLS

| Translation unit  | YANG model |  Command  | Status |
| ----------------- |------------| --------- | ------ |
| Translate-unit-ios-xr-mpls-Openconfig | openconfig-mpls.yang | [configure load share](configure_load_share.md) | draft |
| | | [configure rsvp](configure_rsvp.md) | draft |
