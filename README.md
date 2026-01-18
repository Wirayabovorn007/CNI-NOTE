# CNI-CMDs-NOTE

This is for me na krub no share

## Subnet calculation
![Subnet Calculation](./src/IMG_0933.PNG)

## Basic commands for Router & Switch configuration
```
conf t
enable secret class
line console 0
exec-timeout 0 0 
logging synchronous 
exit
ip domain-name itkmitl.lab 
ip ssh version 2 
crypto key generate rsa modulus 2048
username admin privilege 15 secret cisco
line vty 0 15
login local
transport input telnet ssh
exec-timeout 0 0 
logging synchronous
exit
do wr
```

## VLAN configuration
```
en
conf t
int vlan 8
ip add 10.x.x.x 255.255.255.0
no shut
exit
int Gi0/1
switchport mode access
switchport access vlan 8
no shutdown
```

## Inter VLAN 
### Trunk port
After create VLANs first link to router
```
interface Gi0/0
 description UPLINK_TO_ROUTER
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 8,9
 no shutdown
 exit
```
Second, do configure between switch
```
interface range Gi0/3 - 4
 description LINK_TO_SWITCH2
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 8,9
 no shutdown
 end
```
### Router (The Stick)
Prepare the Physical Interface 
```
interface Gi0/0
 no shutdown
 no ip address
 exit
```
Create Sub-Interface for VLAN 8, 9 
```
interface Gi0/0.8-Gi0.9
 encapsulation dot1q 8-9    <-- This number '8' MUST match the VLAN ID
 ip address 192.168.10.1 255.255.255.0
 exit
```

## Static Routing
```
ip route <dest network> <dest subnet>
```

## DHCP
Create Pool for each network
```
ip dhcp pool LEFT_NET
 network 192.168.10.0 255.255.255.0
 default-router 192.168.10.1
 dns-server 8.8.8.8
 exit
```
Exclude the Gateway IPs so they aren't given to PCs
```
ip dhcp excluded-address 192.168.10.1
```
