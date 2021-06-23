# Privilege

## URL

```
frinx-privilege:privilege
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/evc/src/main/yang)

```javascript
{
    "frinx-privilege:privilege": {
        "levels": {
            "level": [
                {
                    "id": {{privilege_level}},
                    "config": {
                        "id": {{privilege_level}},
                        "commands": [
                            "{{privilege_command}}"
                        ]
                    }
                }
            ]
        }
    }
}
```

## OS Configuration Commands

### Cisco IOS 12, 15, 16 / IOS XE 15, 16, 17

#### CLI

<pre>
privilege exec level {{privilege_level}} {{privilege_command}}
</pre>

#### Unit

Link to github : [ios-privilege-unit](https://github.com/FRINXio/cli-units/tree/master/ios/privilege)