# Cisco IOS classic translation units

[Link to Postman collection](https://github.com/FRINXio/postman-collections)

## Show commands

### General Information

| Translation unit  | YANG model |  Command  | Status | 
| ----------------- |------------| --------- | ------ |
| [Translate-unit-ios-essentials](https://github.com/frinxio/translation-units/code/)| [IOS essentials](https://github.com/frinxio/translation-units/models/)| [show version](show_version.md) | completed |
|  |  | serial number (Device and Module) | [MU-22](https://frinxhelpdesk.atlassian.net/browse/MU-22)|
|  |  |line card status| [MU-23](https://frinxhelpdesk.atlassian.net/browse/MU-23)|


### Interface

| Translation unit  | YANG model |  Command  | Status | 
| ----------------- |------------| --------- | ------ |
| [Translate-unit-ios-interfaces-Openconfig](https://github.com/frinxio/translation-units/code/) | [openconfig-interfaces.yang](https://github.com/frinxio/translation-units/models/interfaces/openconfig-interfaces.yang) | [show ip interface brief](show_ip_interface_brief.md) | completed |
|  | | [show run interface &lt;intf id&gt;](show_run_interface.md) | completed |
|  | | [show interface &lt;intf id&gt;](show_interface.md) | completed |



### IP information

| Translation unit  | YANG model |  Command  | Status | 
| ----------------- |------------| --------- | ------ |
| [Translate-unit-ios-interfaces-Openconfig](https://github.com/frinxio/translation-units/code/) | [openconfig-if-ip.yang](https://github.com/openconfig/public/blob/master/release/models/interfaces/openconfig-if-ip.yang) | [show ip interface](show_ip_interface.md) | completed |
|  | | [show ipv6 interface](show_ipv6_interface.md) | [MU-18](https://frinxhelpdesk.atlassian.net/browse/MU-18) |



### Routing Information

| Translation unit  | YANG model |  Command  | Status | 
| ----------------- |------------| --------- | ------ |
| [Translate-unit-ios-ospf-Openconfig](https://github.com/frinxio/translation-units/code/) | [openconfig-ospfv2.yang](https://github.com/openconfig/public/blob/master/release/models/ospf/openconfig-ospfv2.yang) | [show ip ospf](show_ip_ospf.md) | assignment required |
|  | | [show ip ospf neighbor](show_ip_ospf_neighbor.md) | assignment required |
|  | | [show ip ospf rib](show_ip_ospf_rib.md)| assignment required |
|  | | [show ip route ospf](show_ip_route_ospf.md) | assignment required |
| [Translate-unit-ios- ](https://github.com/frinxio/translation-units/code/) | [openconfig-local-routing.yang](https://github.com/openconfig/public/blob/master/release/models/local-routing/openconfig-local-routing.yang)| [show ip route static](show_ip_route_static.md)| assignment required |
| [Translate-unit-ios-networks-Openconfig](https://github.com/frinxio/translation-units/code/) | [openconfig-network-instance.yang](https://github.com/openconfig/public/blob/master/release/models/network-instance/openconfig-network-instance.yang) | [show ip vrf](show_ip_vrf.md) | [MU-4](https://frinxhelpdesk.atlassian.net/browse/MU-4) |
| [Translate-unit-ios-BGP-OpenConfig](https://github.com/frinxio/translation-units/code/) | [openconfig-bgp.yang](https://github.com/openconfig/public/blob/master/release/models/bgp/openconfig-bgp.yang) | [show ip bgp summary](show_ip_bgp_summary.md) | assignment required |
|  |  | [show ip bgp ](show_ip_bgp.md) | assignment required |
|  |  |Route process type: BGP/OSPF| [MU-24](https://frinxhelpdesk.atlassian.net/browse/MU-24)|
|  |  |Route process ID: BGP-AS 65000/ospf as 100| [MU-25](https://frinxhelpdesk.atlassian.net/browse/MU-25)|
|  |  |Interfaces/IP under each process [IGP]| [MU-26](https://frinxhelpdesk.atlassian.net/browse/MU-26)|
|  |  |Static routes configured| [MU-27](https://frinxhelpdesk.atlassian.net/browse/MU-27)|




### LLDP/CDP

| Translation unit  | YANG model |  Command  | Status | 
| ----------------- |------------| --------- | ------ |
| [Translate-unit-ios-cdplldp](https://github.com/frinxio/translation-units/code/) | [cdp](https://github.com/frinxio/translation-units/models/) | [show cdp neighbor](show_cdp_neighbor.md) | assignment required |
| [Translate-unit-ios-cdplldp](https://github.com/frinxio/translation-units/code/) | [openconfig-lldp.yang](https://github.com/openconfig/public/blob/master/release/models/lldp/openconfig-lldp.yang) | [show lldp neighbor](show_lldp_neighbor.md) | assignment required |
|  |  |LLDP Neighbor| assignment required |
|  |  |LLDP Local Interface| assignment required |
|  |  |LLDP Remote Interface| assignment required |
|  |  |CDP Neighbor| assignment required |
|  |  |CDP Local Interface| assignment required |
|  |  |CDP Remote Interface| assignment required |



---

## Configuration commands

### Interface 

| Translation unit  | YANG model |  Command  | Status | 
| ----------------- |------------| --------- | ------ |
| [Translate-unit-ios-interfaces-Openconfig](https://github.com/frinxio/translation-units/code/) | [openconfig-interfaces.yang](https://github.com/openconfig/public/blob/master/release/models/interfaces/openconfig-interfaces.yang) | [configure interface](configure_interface.md) | completed |
|  | | [enable interface](enable_interface.md) | completed |
|  | | [configure interface description](configure_interface_description.md) | assignment required |
|  | | [configure interface mtu](configure_interface_mtu.md) | assignment required |


### IP information

| Translation unit  | YANG model |  Command  | Status | 
| ----------------- |------------| --------- | ------ |
| [Translate-unit-ios-interfaces-Openconfig](https://github.com/frinxio/translation-units/code/) | [openconfig-if-ip.yang](https://github.com/openconfig/public/blob/master/release/models/interfaces/openconfig-if-ip.yang) | [configure ipv4 interface](configure_ipv4_interface.md) | completed |
|  | | [configure ipv6 interface](configure_ipv6_interface.md) | assignment required |


### Routing Information

| Translation unit  | YANG model |  Command  | Status | 
| ----------------- |------------| --------- | ------ |
|||||



### LLDP/CDP

| Translation unit  | YANG model |  Command  | Status | 
| ----------------- |------------| --------- | ------ |
| [Translate-unit-ios-cdplldp](https://github.com/frinxio/translation-units/code/) | [cdp](https://github.com/frinxio/translation-units/models/) | [configure cdp](configure_cdp.md) | assignment required |
| [Translate-unit-ios-cdplldp](https://github.com/frinxio/translation-units/code/) | [openconfig-lldp.yang](https://github.com/openconfig/public/blob/master/release/models/lldp/openconfig-lldp.yang) | [configure lldp](configure_lldp.md) | assignment required |

