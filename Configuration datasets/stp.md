# Configure STP interfaces

## URL

```
stp:stp
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/cdp/src/main/yang)

```javascript
{
    "stp": {
        "interfaces": {
            "interface": [
                {
                    "name": "{{intf-id}}",
                }
            ]
        }
    }
}
```


## OS Commands

### Brocade (V5.6.0fT163)

#### CLI

If /stp/interfaces/interface/{{intf-id}} exists 
<pre>
interface {{intf-id}}
 spanning-tree
</pre>

If /interfaces/interface/{{intf-id}} exists and /stp/interfaces/interface/{{intf-id}} does not exist
<pre>
interface {{intf-id}}
 no spanning-tree
</pre>

##### Unit

NOT IMPLEMENTED

Link to github : [brocade-unit]()
