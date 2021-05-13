# Ethernet Virtual Circuit (EVC)

## URL

```
frinx-openconfig-evc:evcs
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/evc/src/main/yang)

```javascript
{
    "frinx-openconfig-evc:evcs": {
        "evc": [
            {
                "name": {{evc_name}},
                "config": {
                    "name": {{evc_name}}
                }
            }
        ]
    }
}

```

## OS Configuration Commands

### Cisco IOS XE 16.*

#### CLI

<pre>
ethernet evc {{evc_name}}
</pre>

*ethernet evc {{evc_name}}* is creating evc configuration with name {{evc_name}}  
*no ethernet evc {{evc_name}}* is deleting evc configuration with name {{evc_name}}

#### Unit

Link to github : [ios-xe-evc-unit](https://github.com/FRINXio/cli-units/tree/master/ios-xe/evc)


