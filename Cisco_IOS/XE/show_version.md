# show version

## REST call

```
http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/IOS1/yang-ext:mount/ios-essential:version
```

## REST response body

```
{
    "version": {
        "conf-reg": "0x2102",
        "os-family": "Cisco IOS",
        "platform": "CSR1000V",
        "os-version": "15.3(3)S2, RELEASE SOFTWARE (fc3)",
        "serial-id": "9GHUYVY8CTT",
        "sys-memory": "2187404K/6147K",
        "sys-image": "bootflash:csr1000v-universalk9.03.10.02.S.153-3.S2-ext.SPA.bin"
    }
}
```


---

<pre>
Router#show version
<b><mark>Cisco IOS XE Software</b></mark>, Version 03.10.02.S - Extended Support Release
Cisco IOS Software, <b><mark>CSR1000V</b></mark> Software (X86_64_LINUX_IOSD-UNIVERSALK9-M), Version <b><mark>15.3(3)S2, RELEASE SOFTWARE (fc3)</b></mark>
Technical Support: http://www.cisco.com/techsupport
Copyright (c) 1986-2014 by Cisco Systems, Inc.
Compiled Fri 31-Jan-14 20:10 by mcpre


Cisco IOS-XE software, Copyright (c) 2005-2014 by cisco Systems, Inc.
All rights reserved.  Certain components of Cisco IOS-XE software are
licensed under the GNU General Public License ("GPL") Version 2.0.  The
software code licensed under GPL Version 2.0 is free software that comes
with ABSOLUTELY NO WARRANTY.  You can redistribute and/or modify such
GPL code under the terms of GPL Version 2.0.  For more details, see the
documentation or "License Notice" file accompanying the IOS-XE software,
or the applicable URL provided on the flyer accompanying the IOS-XE
software.


ROM: IOS-XE ROMMON

Router uptime is 39 minutes
Uptime for this control processor is 40 minutes
System returned to ROM by reload
System image file is "<b><mark>bootflash:csr1000v-universalk9.03.10.02.S.153-3.S2-ext.SPA.bin</b></mark>"
Last reload reason: <NULL>



This product contains cryptographic features and is subject to United
States and local country laws governing import, export, transfer and
use. Delivery of Cisco cryptographic products does not imply
third-party authority to import, export, distribute or use encryption.
Importers, exporters, distributors and users are responsible for
compliance with U.S. and local country laws. By using this product you
agree to comply with applicable laws and regulations. If you are unable
to comply with U.S. and local laws, return this product immediately.

A summary of U.S. laws governing Cisco cryptographic products may be found at:
http://www.cisco.com/wwl/export/crypto/tool/stqrg.html

If you require further assistance please contact us by sending email to
export@cisco.com.
          
License Level: limited
License Type: Default. No valid license found.
Next reload license Level: limited

cisco CSR1000V (VXE) processor with <b><mark>2187404K/6147K</b></mark> bytes of memory.
Processor board ID <b><mark>9GHUYVY8CTT</b></mark>
32768K bytes of non-volatile configuration memory.
4194304K bytes of physical memory.
7774207K bytes of virtual hard disk at bootflash:.

Configuration register is 0x2102

</pre>


