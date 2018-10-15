# Link Aggregation Group (bundle) interface

## URL (Interface/lag)

```
frinx-openconfig-interfaces:interfaces/interface/Bundle-Ether{{lag_intf_id}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/interfaces/src/main/yang)

```javascript
{
    "interface": [
        {
            "name": "Bundle-Ether{{lag_intf_id}}",
            "frinx-openconfig-if-aggregate:aggregation": {
                "state": {
                    "frinx-if-aggregate-extension:bundle-state": {{bundle_state}},
                    "frinx-if-aggregate-extension:active-member-count": {{active_count}},
                    "frinx-if-aggregate-extension:standby-member-count": {{standby_count}},
                    "frinx-if-aggregate-extension:configured-member-count": {{configured_count}}
                }
            }
        }
    ]
}
```

## URL (Interface/ethernet)

```
frinx-openconfig-interfaces:interfaces/interface/{{eth_intf_name}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/interfaces/src/main/yang)

```javascript
{
    "interface": [
        {
            "name": "{{eth_intf_name}}",
            "frinx-openconfig-if-ethernet:ethernet": {
                "config": {
                    "frinx-openconfig-if-aggregate:aggregate-id": "Bundle-Ether{{lag_intf_id}}"
                },
                "state": {
                    "frinx-if-aggregate-extension:member-state": {{member_state}}
                }
            }
        ]
    }
}
```

## URL (lacp)

```
frinx-openconfig-lacp:lacp/interfaces/interface/Bundle-Ether{{lag_intf_id}}
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/lacp/src/main/yang)

```javascript
{
    "interface": [
        {
            "name": "Bundle-Ether{{lag_intf_id}}",
            "state": {
                "name": "Bundle-Ether{{lag_intf_id}}",
                "frinx-lacp-extension:lacp-state": "{{lacp_state}}"
            }
        }
    ]
}
```

## OS Configuration Commands

### Cisco IOS XR 7.0.1

<pre>
RP/0/RP0/CPU0:MG-04#show bundle Bundle-Ether{{lag_intf_id}}

Bundle-Ether{{lag_intf_id}}
  Status:                                    {{bundle_state}}
  Local links <active/standby/configured>:   {{active_count}} / {{standby_count}} / {{configured_count}}
  Local bandwidth <effective/available>:     100000000 (100000000) kbps
  MAC address (source):                      008a.96cc.6cda (Chassis pool)
  Inter-chassis link:                        No
  Minimum active links / bandwidth:          1 / 1 kbps
  Maximum active links:                      64
  Wait while timer:                          2000 ms
  Load balancing:
    Link order signaling:                    Not configured
    Hash type:                               Default
    Locality threshold:                      None
  LACP:                                      {{lacp_state}}
    Flap suppression timer:                  Off
    Cisco extensions:                        Disabled
    Non-revertive:                           Disabled
  mLACP:                                     Not configured
  IPv4 BFD:                                  Not configured
  IPv6 BFD:                                  Not configured

  Port                  Device           State        Port ID         B/W, kbps
  --------------------  ---------------  -----------  --------------  ----------
  Hu0/0/0/1             Local            {{member_state}}       0x8000, 0x0001   100000000
      Link is Active
</pre>


##### Unit

Link to github : [xr-interface-unit](https://github.com/FRINXio/unitopo-units/tree/master/xr/xr-7-interface-unit)
[xr-lacp-unit](https://github.com/FRINXio/unitopo-units/tree/master/xr/xr-7-lacp-unit)
