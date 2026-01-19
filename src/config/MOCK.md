# CNI-MOCK-EXAM
>Mock exam commands and configurations

## Topology
![Topology](../pics/IMG_0936.jpeg)
## Part 2: Basic connectivity
### Switch
- Create Vlan A, B
```
int vlan 195, 149
ip add ... ...
exit

int E0/1 - E0/2
no shut
switchport mode access
switchport access vlan 195, 149
```
- Create Trunk link
```
int E0/0
no shut
switchport trunk encapsulation dot1q
switch port mode trunk
```

### Router1
- Add static ip
```
int e0/0
ip add ... ...
no shut
```
- DHCP
```
ip dhcp pool VLANB_POOL
network ... ...
default-router ... ...
dns-server .. ...
exit

ip dhcp excluded-address ... ...
```

- NAT
```
----- Define inside and outside -----
int e0/0
ip nat inside
no shut
exit

int e0/1
ip add dhcp
no shut
ip nat outside

----- Create rule -----
access-list 10 permit any

----- Create NAT by using an interface to the clould -----
ip nat inside source list 10 interface Ethernet0/1 overload
```

### Router2
- Create sub-interface 
```
int e0/0.195 - .149
no shut
encapsulation dot1q <vlan id>
ip add ... ...
ip helper-address ... --> For DHCP relay
```
- Add ip add to another interfaces
```
int e0/1
ip add ... ...
no shut
```

- Do ip route to Internet
```
ip route 0.0.0.0 0.0.0.0 192.168.1.1
```

## Part3: Services
