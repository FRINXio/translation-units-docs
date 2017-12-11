# IETF L2VPN YANG 

##Scenario

###L2P2P/VPLS
l2vpn-instance/type == vpls-instance-type
Two or more endpoints


## IETF  YANG
```javascript
{  
  "l2vpn-instance":[  
    {  
      "name":"<ni-name>",
      "type":"vpls-instance-type",
      "service-type":"Ethernet",
      "signaling-type":"ldp-signaling",
      "tenant-id":"frinx",
      "pw":[
        {
          "name":"<connection_point1_id>",
          "template":"PW1",
          "pw-id":"<vpn_vccid>",
          "request-vlanid":<endpoint1_vlanid>"
        },
        {
          "name":"<connection_point2_id>",
          "template":"PW1",
          "pw-id":"<vpn_vccid>",
          "request-vlanid":"<endpoint2_vlanid>"
        }
        {
          "name":"<connection_point3_id>",
          "template":"PW1",
          "pw-id":"<vpn_vccid>",
          "request-vlanid":"<endpoint3_vlanid>"
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
          "pe-node-id":"pe02",
          "pe-2-ce-tp-id":"<endpoint2_interface_id>",
          "pw":[
            {
              "name":"<connection_point2_id>"
            }
          ]
        },
        {
          "name":"<endpoint3_name>",
          "pe-node-id":"pe03",
          "pe-2-ce-tp-id":"<endpoint3_interface_id>",
          "pw":[
            {
              "name":"<connection_point3_id>"
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
                "type": "L2VSI" //matches vpls-instance-type in ietf
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
                            "connection-point-id": "autodiscovery"
                        }
                        "endpoints": {
                            "endpoint": [
                                {
                                    "config": {
                                        "endpoint-id": "autodiscovery"
                                        "type": "REMOTE"
                                        "remote": {
                                            "config": {
                                                "virtual-circuit-identifier": "<vpn_vccid>"
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

### pe02

```javascript
{
    "network-instance": [
        {
            "config": {
                "name": "<ni-name>"
                "type": "L2VSI" //matches vpls-instance-type in ietf
                "enabled": true
            }
            "connection-points": {
                "connection-point": [
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
                    {
                        "config": {
                            "connection-point-id": "autodiscovery"
                        }
                        "endpoints": {
                            "endpoint": [
                                {
                                    "config": {
                                        "endpoint-id": "autodiscovery"
                                        "type": "REMOTE"
                                        "remote": {
                                            "config": {
                                                "virtual-circuit-identifier": "<vpn_vccid>"
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

### pe03

```javascript
{
    "network-instance": [
        {
            "config": {
                "name": "<ni-name>"
                "type": "L2VSI" //matches vpls-instance-type in ietf
                "enabled": true
            }
            "connection-points": {
                "connection-point": [
                    {
                        "config": {
                            "connection-point-id": "<connection_point3_id>"
                        }
                        "endpoints": {
                            "endpoint": [
                                {
                                    "config": {
                                        "endpoint-id": "<endpoint3_name>"
                                        "type": "LOCAL"
                                        "local": {
                                            "config": {
                                                "interface": "<endpoint3_interface_id>"
                                                "subinterface": "<endpoint3_vlanid>"
                                            }
                                        }
                                    }
                                }
                            ]
                        }
                    }
                    {
                        "config": {
                            "connection-point-id": "autodiscovery"
                        }
                        "endpoints": {
                            "endpoint": [
                                {
                                    "config": {
                                        "endpoint-id": "autodiscovery"
                                        "type": "REMOTE"
                                        "remote": {
                                            "config": {
                                                "virtual-circuit-identifier": "<vpn_vccid>"
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