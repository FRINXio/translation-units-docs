# Translation Units for the FRINX ODL CLI service module

This repository contains documentation for all available translation units for the FRINX ODL CLI service module. A translation unit is a piece of code that includes handlers to read from or write to a specific device (e.g. Cisco IOS classic router) and facilitates the translation in OpenConfig models. 
The purpose of this documentation is to see which commands can be read and set and how they map to the respective YANG models.
Every section has a README file that provides an overview of all show and configuration commands that are supported.
Multiple translation units are finally packaged together and made available as a karaf feature that can be installed at runtime. 

Table of Contents
=================

   * [URL](#url)
     * [URL Operations](#url-operations)
        * [GET](#get)
        * [PUT](#put)
        * [DELETE](#delete)
   * [OPERATIONAL datasets](#operational-datasets)
     * [URL](#url-1)
     * [OPENCONFIG YANG](#openconfig-yang)
     * [OS COMMANDS](#os-commands)
     * [DEVICE YANG](#device-yang)
     * [UNIT](#unit)
   * [CONFIGURATION datasets](#configuration-datasets)
     * [URL](#url-2)
     * [OPENCONFIG YANG](#openconfig-yang-1)
     * [OS COMMANDS](#os-commands-1)
     * [DEVICE YANG](#device-yang-1)
     * [UNIT](#unit-1)

# URL

Each URL has a base format:

```
http://localhost:8181/rests/data/network-topology:network-topology/topology={{topo-name}}/node={{node-id}}/yang-ext:mount
```

- {{topo-name}} can be either cli or unified
- {{node-id}} mountpoint name


The URL will always point to either <b>operational</b> or <b>config</b> datastore and to the node we want to get the information from.
You can always check if the particular device is registered by issuing GET on :

```
http://localhost:8181/rests/data/network-topology:network-topology
```
Simplified example:

```json
{
    "network-topology": {
        "topology": [
            {
                "topology-id": "cli",
                "node": [
                    {
                        "node-id": "xe",
                        "cli-topology:connection-status": "connected",
                        "cli-topology:connected-message": "Success"
                    }
                ]
            },
            {
                "topology-id": "uniconfig",
            },
            {
                "topology-id": "unified",
                "node": [
                    {
                        "node-id": "xe",
                        "unified-topology:connection-status": "connected",
                    }
                ]
            }
        ]
    }
}
```

URLs are modular. By changing the URL you can move along the YANG data tree.

<strong>Example:</strong>

```
http://localhost:8181/rests/data/network-topology:network-topology/topology={{topo-name}}/node={{node-id}}/yang-ext:mount
```/frinx-openconfig-network-instance:network-instances/network-instance={{VRF-id}}/protocols/protocol=frinx-openconfig-policy-types:OSPF={{OSPF-process-id}}/ospfv2/areas/area={{area-id}}/interfaces
```

- very specific URL listing interfaces under one specific area in OSPF under specific VRF

Let's say you want to list all areas in a specific OSPF. To obtain this data, you can trim the part: '/area=&lt;area-id&gt;/interfaces' from the URL.

Let's say you want to be even more specific and list details just about one particular interface. You can view the data by adding 'interface=&lt;interface-id&gt;' to the URL.

The general steps in creating the URL are following:

1. for each container or list in YANG model, there MUST be an argument in the URL
2. each list item argument MUST be followed by list key. Usually the key is mapped to just one leaf (identifier, name, etc.), but in some cases, the key is created using more leafs. In this case, in the URL, the keys follow each other in order specified by YANG.
3. the top level argument must contain the name of the model. The name of the model must also be specified for YANG identities.
4. if the URL is tied with a body, the top-level element in the body must be the last element in the URL

<strong>Example:</strong>
```
http://localhost:8181/rests/data/network-topology:network-topology/topology=cli/node={{node-id}}/yang-ext:mount/frinx-openconfig-network-instance:network-instances/network-instance={{VRF-id}}/protocols/protocol=frinx-openconfig-policy-types:OSPF,{{OSPF-process-id}}/ospfv2/areas/area={{area-id}}/interfaces
```

- top-level argument contains also YANG model name: ‘frinx-openconfig-network-instance’
- network-instances argument is a list. We want to specify one item from that list (specific network instance), therefore the URL continues with ‘network-instance'. The key in network-instance is the identifier '{{VRF-id}}' (e.g. vrf1) which follows the list item argument. Complex key is needed for protocol argument. The key is protocol-type followed by process-id. (frinx-openconfig-policy-types:OSPF,{{OSPF-process-id}} )
- same for 'area={{area-id}}'
- the URL contains an identity which is a part of a key for protocol list. This identity is prefixed by model name: ‘frinx-openconfig-policy-types:OSPF’

You can create a minimalistic YANG tree out of the URL:

```javascript
frinx-openconfig-network-instances: {                 // top-level container
    network-instance: [                               // list
        {                                             // list-item start
            key: {{VRF-id}}                           // list key
            protocols: {
                protocol: [
                    {
                        key: "frinx-openconfig-policy-types:OSPF {{OSPF-process-id}}"
                        ospfv2: {
                            areas: {
                                area: [
                                    {
                                        key: {{area-id}}
                                        interfaces {
                                           ...
                                        }
                                    }
                                ]
                            }
                        }
                    }                                 // list-item end
                ]
            }
        }
    ]
}
```

### URL Operations

Each show command supports only one http operation: GET .

#### GET

GET operation can be issued on both config/operational datastore. Config datastore reflects how the device is configured. Operational datastore reflects the state of the device. In most cases the information is the same.

Example of a case where the information is not the same (the only difference in requests is config vs operational):

```
GET http://{{odl_ip}}:8181/rests/data/network-topology:network-topology/topology=cli/node={{node_id}}/yang-ext:mount/frinx-openconfig-network-instance:network-instances/network-instance=default/protocols/protocol=frinx-openconfig-policy-types:STATIC,default/static-routes/static=10.255.1.0%2F24?content=config
```
```json
{
    "static": [
        {
            "prefix": "10.255.1.0/24",
            "config": {
                "prefix": "10.255.1.0/24"
            },
            "next-hops": {
                "next-hop": [
                    {
                        "index": "192.168.1.5",
                        "config": {
                            "index": "192.168.1.5"
                        }
                    }
                ]
            }
        }
    ]
}
```

```
GET http://{{odl_ip}}:8181/rests/data/network-topology:network-topology/topology=cli/node={{node_id}}/yang-ext:mount/frinx-openconfig-network-instance:network-instances/network-instance=default/protocols/protocol=frinx-openconfig-policy-types:STATIC,default/static-routes/static=10.255.1.0%2F24?content=nonconfig
```

```json
{
    "static": [
        {
            "prefix": "10.255.1.0/24",
            "config": {
                "prefix": "10.255.1.0/24"
            },
            "state": {
                "prefix": "10.255.1.0/24"
            },
            "next-hops": {
                "next-hop": [
                    {
                        "index": "192.168.1.5",
                        "config": {
                            "index": "192.168.1.5"
                        },
                        "state": {
                            "metric": 1,
                            "index": "192.168.1.5"
                        }
                    }
                ]
            }
        }
    ]
}
```


Configuration commands support PUT for create/replace data. This operation requires HTTP body, which contains openconfig YANG model of the configuration you want to send to the router. Another operation supported by configuration commands is DELETE, which removes data from the device. Both operations need to be issued on config datastore.

For modifications of the data, you can use also PATCH method, that does not replace the entire data structure, only the parts that are different.

<strong>Example:</strong>

We want to create a new BGP neighbor:

The IOS command is:

<pre>
router bgp &lt;as&gt;
 neighbor &lt;neighbor-address&gt;
   no shutdown
</pre>

#### PUT

```
http://localhost:8181/rests/data/network-topology:network-topology/topology=cli/node={{node-id}}/yang-ext:mount/frinx-openconfig-network-instance:network-instances/network-instance={{ni-name}}/protocols/protocol=frinx-openconfig-bgp:bgp
```

BODY:
```javascript
{
    "bgp": {
        "global": {
            "config": {
                "as": {{as}}
            }
        }
        "neighbors": {
            "neighbor": [
                {
                    "config": {
                        "neighbor-address": {{neighbor-address}}
                        "enabled": true
                    }
                }
            ]
        }
    }
}
```

WARNING: PUT operation does not merge data. In this example if you have already configured some BGP neighbors, this request will REMOVE
all of them and create just the one described in the PUT body. The solution is to first issue GET, copy existing configuration and add/change items there, or use PATCH method.

If we want to DELETE a BGP neighbor, the body is not needed, the URL needs to be specific to the neighbor we want to delete:

#### DELETE

```
http://localhost:8181/rests/data/network-topology:network-topology/topology=cli/node={{node-id}}/yang-ext:mount/frinx-openconfig-network-instance:network-instances/network-instance={{ni-name}}/protocols/protocol=frinx-openconfig-bgp:bgp/neighbors/neighbor={{neighbor-address}}
```

This operation will issue following command:

<pre>
router bgp &lt;as&gt;
 no neighbor &lt;neighbor-address&gt;
</pre>

DELETE operation always removes the last argument of the URL.

# OPERATIONAL datasets

<a href="Operational%20datasets/README.md">go to operational datasets</a>

Show commands are commands that usually on Cisco device start with 'show'. The aim is to obtain data from the router.

### URL
GET operation issued on operational datastore

### OPENCONFIG YANG
In case of show commands this section is a sample output of a particular show command.

### OS COMMANDS
In this section we list the actual router commands with sample outputs, where the data obtained and transformed into Openconfig YANG is marked as bold. We list show commands and outputs for each supported device OS.

IOS XR | IOS Classic/XE | Junos | SAOS 

### DEVICE YANG

In case of CLI units, the unit parses the output of the CLI command directly into OC YANG. In case of Netconf units, the output is mapped to OC YANG through Device YANG (YANG model supported by the device). In case of Netconf units, the YANG is also written in documentation.
This section is a link to XML unit test input testing this operation.

### UNIT

Link to github code where this show commmand is implemented along with unit version range.

# CONFIGURATION datasets

<a href="Configuration%20datasets/README.md">go to configuration datasets</a>

### URL
PUT operation with given URL will result in creating of data in config datastore
DELETE operation with given URL will result in removing data in config datastore

### OPENCONFIG YANG

In case of configuration commands, this section represents the HTTP body in PUT operation

### OS COMMANDS
In this section we list the actual router commands that are mapped to the Openconfig YANG model. Data transformed into Openconfig YANG is marked as bold. We list commands for each supported device OS.

IOS XR | IOS Classic/XE | Junos

### DEVICE YANG
In case od Netconf units, the device yang represents command sent to the device in device YANG model.
This section is a link to XML unit test input testing this configuration.

### UNIT

Link to github code where this config commmand is implemented along with unit version range.
