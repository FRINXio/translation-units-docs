# Cisco IOS classic translation units

Translation units also apply to IOS XE unless otherwise noted.

## Show commands

### General Information

| Translation unit  | YANG model |  Command  | Status | 
| ----------------- |------------| --------- | ------ |
| [Translate-unit-ios-essentials](https://github.com/FRINXio/cli-units/tree/master/ios/essential)| [IOS essentials](https://github.com/FRINXio/cli-units/tree/master/ios/essential)| [show version](../base/show_version.md) | completed |
|  |  |line card status| [MU-23](https://frinxhelpdesk.atlassian.net/browse/MU-23)|


### Interface

| Translation unit  | YANG model |  Command  | Status | 
| ----------------- |------------| --------- | ------ |
| [Translate-unit-ios-interfaces-Openconfig](https://github.com/FRINXio/cli-units/tree/master/ios/interface) | [openconfig-interfaces.yang](https://github.com/FRINXio/openconfig/tree/master/interfaces) | [show ip interface brief](../base/show_ip_interface_brief.md) | completed |
|  | | [show run interface &lt;intf id&gt;](../base/show_run_interface.md) | completed |
|  | | [show interface &lt;intf id&gt;](../base/show_interface.md) | completed |



### IP 

| Translation unit  | YANG model |  Command  | Status | 
| ----------------- |------------| --------- | ------ |
| [Translate-unit-ios-interfaces-Openconfig](https://github.com/FRINXio/cli-units/tree/master/ios/interface) | [openconfig-if-ip.yang](https://github.com/FRINXio/openconfig/tree/master/interfaces) | [show ip interface](../base/show_ip_interface.md) | completed |
|  | | [show ipv6 interface](../base/show_ipv6_interface.md) | completed |



### Routing

| Translation unit  | YANG model |  Command  | Status | 
| ----------------- |------------| --------- | ------ |
| [Translate-unit-ios-ospf-Openconfig](https://github.com/frinxio/translation-units/code/) | [openconfig-ospfv2.yang](https://github.com/openconfig/public/blob/master/release/models/ospf/openconfig-ospfv2.yang) | [show ip ospf](../base/show_ip_ospf.md) | completed |
|  | | [show ip ospf interface brief](../base/show_ip_ospf_interface_brief.md) | completed |
| [Translate-unit-ios- ](https://github.com/frinxio/translation-units/code/) | [openconfig-local-routing.yang](https://github.com/openconfig/public/blob/master/release/models/local-routing/openconfig-local-routing.yang)| [show ip route static](../base/show_ip_route_static.md)| [MU-27](https://frinxhelpdesk.atlassian.net/browse/MU-27) |
| [Translate-unit-ios-networks-Openconfig](https://github.com/frinxio/translation-units/code/) | [openconfig-network-instance.yang](https://github.com/openconfig/public/blob/master/release/models/network-instance/openconfig-network-instance.yang) | [show ip vrf](../base/show_ip_vrf.md) | completed |
| [Translate-unit-ios-BGP-OpenConfig](https://github.com/FRINXio/cli-units/tree/master/ios/bgp) | [openconfig-bgp.yang](https://github.com/openconfig/public/blob/master/release/models/bgp/openconfig-bgp.yang) | [show ip bgp summary](../base/show_ip_bgp_summary.md) | completed |


### LLDP/CDP

| Translation unit  | YANG model |  Command  | Status | 
| ----------------- |------------| --------- | ------ |
| [Translate-unit-ios-cdplldp](https://github.com/frinxio/translation-units/code/) | [cdp](https://github.com/frinxio/translation-units/models/) | [show cdp neighbor](../base/show_cdp_neighbor.md) | assignment required |
| [Translate-unit-ios-cdplldp](https://github.com/frinxio/translation-units/code/) | [openconfig-lldp.yang](https://github.com/openconfig/public/blob/master/release/models/lldp/openconfig-lldp.yang) | [show lldp neighbor](../base/show_lldp_neighbor.md) | assignment required |


---

## Configuration commands

### Interface 

| Translation unit  | YANG model |  Command  | Status | 
| ----------------- |------------| --------- | ------ |
| [Translate-unit-ios-interfaces-Openconfig](https://github.com/FRINXio/cli-units/tree/master/ios/interface) | [openconfig-interfaces.yang](https://github.com/openconfig/public/blob/master/release/models/interfaces/openconfig-interfaces.yang) | [configure interface](../base/configure_interface.md) | completed |
|  | | [enable interface](../base/enable_interface.md) | completed |
|  | | [configure interface description](../base/configure_interface_description.md) | assignment required |
|  | | [configure interface mtu](../base/configure_interface_mtu.md) | assignment required |


### IP

| Translation unit  | YANG model |  Command  | Status | 
| ----------------- |------------| --------- | ------ |
| [Translate-unit-ios-interfaces-Openconfig](https://github.com/FRINXio/cli-units/tree/master/ios/interface) | [openconfig-if-ip.yang](https://github.com/openconfig/public/blob/master/release/models/interfaces/openconfig-if-ip.yang) | [configure ipv4 interface](../base/configure_ipv4_interface.md) | completed |
|  | | [configure ipv6 interface](../base/configure_ipv6_interface.md) | assignment required |


### Routing

| Translation unit  | YANG model |  Command  | Status | 
| ----------------- |------------| --------- | ------ |
|||||



### LLDP/CDP

| Translation unit  | YANG model |  Command  | Status | 
| ----------------- |------------| --------- | ------ |
| [Translate-unit-ios-cdplldp](https://github.com/frinxio/translation-units/code/) | [cdp](https://github.com/frinxio/translation-units/models/) | [configure cdp](../base/configure_cdp.md) | assignment required |
| [Translate-unit-ios-cdplldp](https://github.com/frinxio/translation-units/code/) | [openconfig-lldp.yang](https://github.com/openconfig/public/blob/master/release/models/lldp/openconfig-lldp.yang) | [configure lldp](../base/configure_lldp.md) | assignment required |

