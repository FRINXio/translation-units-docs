# show ip ospf rib

## REST call

```



```

## REST response body

```
 


```


---

<pre>
R122#show ip ospf rib

            OSPF Router with ID (192.168.56.122) (Process ID 100)


		Base Topology (MTID 0)

OSPF local RIB
Codes: * - Best, > - Installed in global RIB

*   <b><mark>6.6.6.6/32</b></mark>, <b><mark>Intra</b></mark>, cost <b><mark>1</b></mark>, <b><mark>area 20</b></mark>, <b><mark>Connected</b></mark>
      via <b><mark>6.6.6.6</b></mark>, <b><mark>Loopback1</b></mark>
*>  7.7.7.7/32, Intra, cost 101, area 20
      via 8.8.8.1, GigabitEthernet3/0
*   <b><mark>8.8.8.0/24</b></mark>, <b><mark>Intra</b></mark>, cost <b><mark>100</b></mark>, <b><mark>area 20</b></mark>, <b><mark>Connected</b></mark>
      via <b><mark>8.8.8.2</b></mark>, <b><mark>GigabitEthernet3/0</b></mark>
*>  10.5.5.0/24, Intra, cost 101, area 20
      via 8.8.8.1, GigabitEthernet3/0
*   <b><mark>10.7.7.0/24</b></mark>, <b><mark>Intra</b></mark>, cost <b><mark>1</b></mark>, <b><mark>area 20</b></mark>, <b><mark>Connected</b></mark>
      via <b><mark>10.7.7.1</b></mark>, <b><mark>GigabitEthernet1/0</b></mark>
R122#
</pre>



