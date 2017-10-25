# List all network instances (VRFs)

## URL

```
openconfig-network-instance:network-instances
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/network-instance/src/main/yang)

```javascript
{
    "network-instances": {
        "network-instance": [
            {
                "name": "default",
                "config": {
                    "name": "default",
                    "type": "openconfig-network-instance-types:L3VRF"
                },
                "interfaces": {
                    "interface": [
                        {
                            "id": "FastEthernet0/0"
                        }
                    ]
                }
            },
            {
                "name": "DEP_1",
                "config": {
                    "name": "DEP_1",
                    "type": "openconfig-network-instance-types:L3VRF"
                },
                "interfaces": {
                    "interface": [
                        {
                            "id": "GigabitEthernet1/0"
                        },
                        {
                            "id": "GigabitEthernet2/0"
                        }
                    ]
                }
            },
            {
                "name": "DEP_2",
                "config": {
                    "name": "DEP_2",
                    "type": "openconfig-network-instance-types:L3VRF"
                },
                "interfaces": {
                    "interface": [
                        {
                            "id": "GigabitEthernet3/0"
                        }
                    ]
                }
            }
        ]
    }
}
```

## OS Commands

### Cisco IOS Classic (15.2(4)S5) / XE (15.3(3)S2)

#### CLI

---
<pre>
R121#sh ip vrf
  Name                             Default RD          Interfaces
  <b><mark>DEP_1</b></mark>                            <not set>           <b><mark>Gi1/0</b></mark>
  <b><mark>DEP_1</b></mark>                                                <b><mark>Gi2/0</b></mark>
  <b><mark>DEP_2</b></mark>                            <not set>           <b><mark>Gi3/0</b></mark>


R121#sh ip vrf interfaces 
Interface              IP-Address      VRF                              Protocol
<b><mark>Gi1/0</b></mark>                  unassigned      <b><mark>DEP_1</b></mark>                            down
<b><mark>Gi2/0</b></mark>                  unassigned      <b><mark>DEP_1</b></mark>                            down
<b><mark>Gi3/0</b></mark>                  unassigned      <b><mark>DEP_2</b></mark>                            down
</pre>
---

##### Unit

Unit version range: 3.1.1.rc1-frinx

Link to github : [ios-unit](https://github.com/FRINXio/cli-units/tree/master/ios/essential)
