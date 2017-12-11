# IETF L2VPN YANG 

##Scenario

###L2P2P/VPWS 
l2vpn-instance/type == vpws-instance-type
only two endpoints

###Local-Local
connection between two local ports on a host (pe-node-id`s of endpoints match)

## IETF  YANG
```javascript
{  
  "l2vpn-instance":[  
    {  
      "name":"<ni-name>",
      "type":"vpws-instance-type",
      "service-type":"Ethernet",
      "signaling-type":"ldp-signaling",
      "tenant-id":"frinx",
      "pw":[
        {
          "name":"<connection_point1_id>",
          "request-vlanid":"<endpoint1_vlanid>",
          "vlan-tpid":"<endpoint1_vlan-tpid>"
        },
        {
          "name":"<connection_point2_id>",
          "request-vlanid":"<endpoint2_vlanid>",
          "vlan-tpid":"<endpoint2_vlan-tpid>"
        }
      ],
      "endpoint":[
        {
          "name":"<endpoint1_name>",
          "pe-node-id":"pe01",
          "pe-2-ce-tp-id":"<endpoint1_interface_id>",
          "pw":[
            {
              "name":"<connection_point1_id>"
            }
          ]
        },
        {
          "name":"<endpoint2_name>",
          "pe-node-id":"pe01",
          "pe-2-ce-tp-id":"<endpoint2_interface_id>",
          "pw":[
            {
              "name":"<connection_point2_id>"
            }
          ]
        }
      ]
    }
  ]
}
```

## OPENCONFIG YANG

### pe01

```javascript
{
    "network-instance": [
        {
            "config": {
                "name": "<ni-name>"
                "type": "L2P2P" //matches vpws-instance-type in ietf
                "enabled": true
            }
            "connection-points": {
                "connection-point": [
                    {
                        "config": {
                            "connection-point-id": "<connection_point1_id>"
                        }
                        "endpoints": {
                            "endpoint": [
                                {
                                    "config": {
                                        "endpoint-id": "<endpoint1_name>"
                                        "type": "LOCAL"
                                        "local": {
                                            "config": {
                                                "interface": "<endpoint1_interface_id>"
                                                "subinterface": "<endpoint1_vlanid>"
                                            }
                                        }
                                    }
                                }
                            ]
                        }
                    }
                    {
                        "config": {
                            "connection-point-id": "<connection_point2_id>"
                        }
                        "endpoints": {
                            "endpoint": [
                                {
                                    "config": {
                                        "endpoint-id": "<endpoint2_name>"
                                        "type": "LOCAL"
                                        "local": {
                                            "config": {
                                                "interface": "<endpoint2_interface_id>"
                                                "subinterface": "<endpoint2_vlanid>"
                                            }
                                        }
                                    }
                                }
                            ]
                        }
                    }
                ]
            }
        }
    ]
}
```