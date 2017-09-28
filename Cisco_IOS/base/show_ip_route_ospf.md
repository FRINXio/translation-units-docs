# show ip route ospf

## REST call

```



```

## REST response body

```
 


```


---

<pre>
R121#sh ip route ospf
Codes: L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area 
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2
       i - IS-IS, su - IS-IS summary, L1 - IS-IS level-1, L2 - IS-IS level-2
       ia - IS-IS inter area, * - candidate default, U - per-user static route
       o - ODR, P - periodic downloaded static route, H - NHRP, l - LISP
       + - replicated route, % - next hop override

Gateway of last resort is not set

      6.0.0.0/32 is subnetted, 1 subnets
O        <b><mark>6.6.6.6</b></mark> [<b><mark>110</b></mark>/<b><mark>101</b></mark>] via <b><mark>8.8.8.2</b></mark>, 01:06:47, <b><mark>GigabitEthernet3/0</b></mark>
      10.0.0.0/8 is variably subnetted, 3 subnets, 2 masks
O        <b><mark>10.7.7.0/24</b></mark> [<b><mark>110</b></mark>/<b><mark>101</b></mark>] via <b><mark>8.8.8.2</b></mark>, 01:02:03, <b><mark>GigabitEthernet3/0</b></mark>
R121#
</pre>



