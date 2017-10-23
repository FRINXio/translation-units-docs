# Show inventory

## URL

```
openconfig-platform:components
```

## OPENCONFIG YANG

```javascript
{
    "components": {
        "component": [
            {
                "name": "module 0/0/CPU0",
                "config": {
                    "name": "module 0/0/CPU0"
                },
                "state": {
                    "mfg-name": "Cisco Systems Inc.",
                    "part-no": "ASR9001-LC",
                    "version": "V01",
                    "serial-no": "FOC2025NGA1",
                    "id": "module 0/0/CPU0",
                    "description": "ASR 9001, Modular Line Card",
                    "type": "openconfig-platform-types:LINECARD"
                }
            }
        ]
    }
}
```

## OS Commands

### Cisco ASR9K

#### CLI
---
<pre>
RP/0/RSP0/CPU0:ios#admin
Wed Oct 18 07:47:29.184 UTC
RP/0/RSP0/CPU0:ios(admin)#sh inventory
Wed Oct 18 07:47:38.990 UTC
NAME: "module 0/RSP0/CPU0", DESCR: "ASR 9001, Route Switch Processor with 8GB memory"
PID: ASR9001-RP, VID: V01 , SN: FOC2025NFZL

NAME: "fantray 0/FT0/SP", DESCR: "ASR-9001 Fan Tray"
PID: ASR-9001-FAN, VID: V04 , SN: FOC2003NHY3

NAME: "fan0 0/FT0/SP", DESCR: "ASR9K Generic Fan"
PID:    , VID: N/A, SN: 

NAME: "fan1 0/FT0/SP", DESCR: "ASR9K Generic Fan"
PID:    , VID: N/A, SN: 

NAME: "fan2 0/FT0/SP", DESCR: "ASR9K Generic Fan"
PID:    , VID: N/A, SN: 

NAME: "fan3 0/FT0/SP", DESCR: "ASR9K Generic Fan"
PID:    , VID: N/A, SN: 

NAME: "fan4 0/FT0/SP", DESCR: "ASR9K Generic Fan"
PID:    , VID: N/A, SN: 

NAME: "fan5 0/FT0/SP", DESCR: "ASR9K Generic Fan"
PID:    , VID: N/A, SN: 

NAME: "fan6 0/FT0/SP", DESCR: "ASR9K Generic Fan"
PID:    , VID: N/A, SN: 

NAME: "fan7 0/FT0/SP", DESCR: "ASR9K Generic Fan"
PID:    , VID: N/A, SN: 

NAME: "fan8 0/FT0/SP", DESCR: "ASR9K Generic Fan"
PID:    , VID: N/A, SN: 

NAME: "fan9 0/FT0/SP", DESCR: "ASR9K Generic Fan"
PID:    , VID: N/A, SN: 

NAME: "fan10 0/FT0/SP", DESCR: "ASR9K Generic Fan"
PID:    , VID: N/A, SN: 

NAME: "fan11 0/FT0/SP", DESCR: "ASR9K Generic Fan"
PID:    , VID: N/A, SN: 

NAME: "fan12 0/FT0/SP", DESCR: "ASR9K Generic Fan"
PID:    , VID: N/A, SN: 

NAME: "fan13 0/FT0/SP", DESCR: "ASR9K Generic Fan"
PID:    , VID: N/A, SN: 

<b><mark>
NAME: "module 0/0/CPU0", DESCR: "ASR 9001, Modular Line Card"
PID: ASR9001-LC, VID: V01 , SN: FOC2025NGA1
</b></mark>

NAME: "module 0/0/0", DESCR: "ASR 9000 8-port 10GE Modular Port Adapter"
PID: N/A, VID: N/A, SN: 

NAME: "module 0/0/2", DESCR: "ASR 9000 Virtual Module"
PID: A9K-MODULEv, VID: N/A, SN: N/A

NAME: "power-module 0/PS0/M0/SP", DESCR: "ASR-9001 AC Power Supply"
PID: A9K-750W-AC, VID: V01 , SN: ART2017X0ZT

NAME: "power-module 0/PS0/M1/SP", DESCR: "ASR-9001 AC Power Supply"
PID: A9K-750W-AC, VID: V01 , SN: ART2017X10J

NAME: "chassis ASR-9001", DESCR: "ASR-9001 Chassis"
PID: ASR-9001, VID: V06 , SN: FOC2026N2TR
</pre>
---

#### DEVICE YANG

##### Unit

Unit version range: 3.1.1.rc1-frinx

Link to github : [xr-unit][]

