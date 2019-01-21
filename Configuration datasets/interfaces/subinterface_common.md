# Subinterface common configuration

## URL

```
frinx-openconfig-interfaces:interfaces/interface/{{eth_url_intf-id}}/subinterfaces
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/interfaces/src/main/yang)

```javascript
{
    "subinterfaces": {
        "subinterface": [
            {
                "index": 0,
                "config": {
                    "index": 0,
                    "juniper-if-ext:rpm-type": {{rpm_type}}
                },
                "frinx-openconfig-if-ip:ipv4": {
                    "addresses": {
                        "address": [
                            {
                                "ip": "{{eth_ifc_ip}}",
                                "config": {
                                    "ip": "{{eth_ifc_ip}}",
                                    "prefix-length": {{eth_ifc_pref_length}}
                                }
                            }
                        ]
                    }
                }
            },
            {
                "index": {{sub_ifc_index}},
                "config": {
                    "index": {{sub_ifc_index}},
                    "juniper-if-ext:rpm-type": {{rpm_type}},
                    "description": "{{sub_ifc_description}}"
                },
                "frinx-openconfig-if-ip:ipv4": {
                    "addresses": {
                        "address": [
                            {
                                "ip": "{{eth_ifc_ip}}",
                                "config": {
                                    "ip": "{{eth_ifc_ip}}",
                                    "prefix-length": {{eth_ifc_pref_length}}
                                }
                            }
                        ]
                    }
                },
                "frinx-openconfig-vlan:vlan": {
                    "config": {
                        "vlan-id": "{{l3_vlan_id}}"
                    }
                }
            }
        ]
    }
}
```

## OS Configuration Commands

### Cisco IOS Classic (15.2(4)S5) / XE (15.3(3)S2)

---
<pre>
interface {{eth_url_intf-id}}
 ip address {{eth_ifc_ip}} {{subnet}}
</pre>

{{subnet}} is conversion of {{eth_ifc_pref_length}}

---

##### Unit

Link to github : [ios-unit](https://github.com/FRINXio/cli-units/tree/master/ios/interface)

### Cisco IOS XR 5.3.4

#### CLI

---
<pre>
interface {{eth_url_intf-id}}.0
 ipv4 address {{eth_ifc_ip}} {{subnet}}
</pre>

{{subnet}} is conversion of {{eth_ifc_pref_length}}

---


##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/interface)

### Cisco IOS XR 6.2.3

#### CLI

---
<pre>
interface {{eth_url_intf-id}}.{{sub_ifc_index}}
 description {{sub_ifc_description}}
 ipv4 address {{eth_ifc_ip}} {{subnet}}
 encapsulation dot1q {{l3_vlan_id}}
</pre>

{{subnet}} is conversion of {{eth_ifc_pref_length}}

---

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xr/interface)

### Cisco IOS XR 7.0.1

#### CLI

---
<pre>
interface {{eth_url_intf-id}}.0
 ipv4 address {{eth_ifc_ip}} {{subnet}}
interface {{eth_url_intf-id}}.{{sub_ifc_index}}
 ipv4 address {{eth_ifc_ip}} {{subnet}}
 encapsulation dot1q {{l3_vlan_id}}
</pre>

{{subnet}} is conversion of {{eth_ifc_pref_length}}

---

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/unitopo-units/tree/master/xr/xr-7-interface-unit)

### Junos 17.3R1.10

#### CLI

---
<pre>
set interfaces {{eth_url_intf-id}} unit 0 family inet address {{eth_ifc_ip}}/{{eth_ifc_pref_length}}
</pre>
---

##### Unit

Link to github : [junos-unit](https://github.com/FRINXio/unitopo-units/tree/master/junos/junos-17/junos-17-interface-unit)

### Junos 18.2R2

#### CLI

---
<pre>
set interfaces {{rpm_intf_index}} unit {{rpm_subintf_index}} rpm {{rpm_type}}
</pre>
---

rpm_intf_index , rpm_subintf_index is a conversion of {{rpm_intf_id}} set {{rpm_intf_index}}.{{rpm_subintf_index}}  

##### Unit

Link to github : [junos-unit](https://github.com/FRINXio/unitopo-units/tree/master/junos/junos-18/junos-18-interface-unit)

### Huawei NE5000E (V800R009C10SPC310)

#### CLI

---
<pre>
interface {{eth_url_intf-id}}.0
 ipv4 address {{eth_ifc_ip}} {{subnet}}
</pre>

{{subnet}} is conversion of {{eth_ifc_pref_length}}

---

##### Unit

Link to github : [huawei-unit](https://github.com/FRINXio/cli-units/tree/master/huawei/interface)

