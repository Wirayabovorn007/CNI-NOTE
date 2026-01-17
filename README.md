# CNI-CMDs-NOTE

This is for me na krub no share

### Subnet calculation
![Subnet Calculation](./src/IMG_0933.PNG)

### Basic commands for Router & Switch configuration
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

### VLAN configuration
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