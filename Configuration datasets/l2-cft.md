# L2-Cft (Layer 2 Control Frame Forwarding)

## URL

```
frinx-openconfig-l2-cft:l2-cft
```

## OPENCONFIG YANG

```javascript
{
    "frinx-openconfig-l2-cft:l2-cft": {
        "profiles": {
            "profile": [
                {
                    "name": "{{cft_profile_name}}",              
                    "protocols": {
                        "protocol": [
                            {
                                "name": "{{ctrl_protocol_name}}",
                                "config": {
                                    "name": "{{ctrl_protocol_name}}",
                                    "disposition": "{{disposition}}"
                                }
                            }
                        ]
                    },
                    "config": {
                        "name": "{{cft_profile_name}}"
                    }
                }
            ]
        },
        "config": {
            "mode": "{{cft_mode}}"
        }
    }
}
```
## OS Configuration Commands

### Ciena SAOS 6.14

#### CLI

<pre>
l2-cft set mode {{cft_mode}}
l2-cft create profile {{cft_profile_name}}
l2-cft protocol add profile {{cft_profile_name}} ctrl-protocol {{ctrl_protocol_name}} untagged-disposition {{disposition}}
</pre>

{{cft_mode}} can be <mef-ce1|mef-ce2>  
{{ctrl_protocol_name}} can be <802.1x | all-bridges-block | cisco-cdp | 
cisco-dtp | cisco-pagp | cisco-pvst | cisco-stp-uplink-fast |cisco-udld | 
cisco-vtp | elmi | esmc | garp-block | gmrp | gvrp | lacp | lacp-marker | 
lldp | oam | ptp-peer-delay | vlan-bridge | xstp>  
if {{cft_mode}} ==  mef-ce1 -> {{ctrl_protocol_name}} can be also bridge-block  
if {{cft_mode}} ==  mef-ce2 -> {{ctrl_protocol_name}} can be also <bridge-rsvd-0B0F |
bridge-rsvd-0C0D | mef-ce2-bridge-block>  
{{disposition}} can be <discard | forward>  


##### Unit