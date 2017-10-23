# Configure network instance (VRF)

## URL

```
ios-essential:vrfs/vrf/<vrf>
```

## OPENCONFIG YANG

```javascript
{
	"vrf": {
    	"id": <vrf>
    	"description": <desc>
	}
}
```

## OS Commands

### Cisco IOS Classic (15.2(4)S5) / XE (15.3(3)S2)

#### CLI

---
<pre>
configure terminal
 ip vrf &lt;vrf&gt;
 description &lt;desc&gt;
exit
exit
</pre>
---

##### Unit

Unit version range: 3.1.1.rc1-frinx

Link to github : [ios-unit](https://github.com/FRINXio/cli-units/tree/master/ios/essential)

