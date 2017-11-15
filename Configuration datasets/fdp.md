# Configure FDP interfaces

## URL

```
fdp:fdp
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/fdp/src/main/yang)

```javascript
{
    "fdp": {
        "interfaces": {
            "interface": [
                {
                    "name": "<intf-id>",
                    "config": {
                        "name": "<intf-id>",
                        "enabled": true
                }
            ]
        }
    }
}
```


### Brocade (V5.6.0fT163)

#### CLI

<pre>
interface &lt;intf-id&gt;
 fdp enable | no fdp enable
</pre>

*fdp enable* is conversion of *"enabled": true*  
*no fdp enable* is conversion of *"enabled": false*
##### Unit