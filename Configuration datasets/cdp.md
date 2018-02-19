# Configure CDP interfaces

## URL

```
frinx-cdp:cdp
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/cdp/src/main/yang)

```javascript
{
    "cdp": {
        "interfaces": {
            "interface": [
                {
                    "name": "{{cdp_lldp_test_interface}}",
                    "config": {
                        "name": "{{cdp_lldp_test_interface}}",
                        "enabled": true
                    }
                }
            ]
        }
    }
}
```


## OS Commands

### Cisco IOS Classic (15.2(4)S5) / XE (15.3(3)S2)

#### CLI

<pre>
interface {{cdp_lldp_test_interface}}
 cdp enable | no cdp enable
</pre>

*cdp enable* is conversion of *"enabled": true*  
*no cdp enable* is conversion of *"enabled": false*

##### Unit

Link to github : [ios-unit](https://github.com/FRINXio/cli-units/tree/master/ios/cdp)

### Cisco IOS XR (XRv 5.1.3 and XRv 6.1.2 tested)

#### CLI

<pre>
interface {{cdp_lldp_test_interface}}
 cdp | no cdp
</pre>

*cdp* is conversion of *"enabled": true*  
*no cdp* is conversion of *"enabled": false*

##### Unit

Link to github : [xr-unit](https://github.com/FRINXio/unitopo-units/tree/master/xr-6-cdp-unit)

### Brocade (V5.6.0fT163)

#### CLI

<pre>
interface {{cdp_lldp_test_interface}}
 cdp enable | no cdp enable
</pre>

*cdp enable* is conversion of *"enabled": true*  
*no cdp enable* is conversion of *"enabled": false*

##### Unit

Link to github : [brocade-unit](https://github.com/FRINXio/cli-units/tree/master/brocade/cdp)
