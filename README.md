# isten-terve-kis_i_vel

## bocsánat Nagy __I__ vel az Isten 🙏🙏🙏 in nomine patris et fili 🙏🙏🙏


<img src="2omb-prayge.gif">
*in nomine oatris et fili <br>
cuius regio eius religio <br>
in medius res deus ex machine <br>
nomen est omen carpe diem <br>
divida et impara <br>
Ervin atyánk mindörökké ámen* 🙏 <br>

### interfészek beáll.
```bash

en
conf t

int serial0/0/0
ip add 192.168.10.2 255.255.255.252
ipv6 add 2001:db8:acad:3::2/64
no sh

int serial0/0/1
ip add 192.168.10.5 255.255.255.252
no sh


int g0/0
ip add 192.168.30.1 255.255.255.0
ipv6 add 2001:db8:acad:2::1/64

ipv6 add FE80::1 link-local
no sh
```




### alap konfig ssh meg miegymás
```bash


hostname BS3
ipv6 unicast-routing 

username admin privilege 15 secret wmtech2025

line vty 0 15
login local
password wmtech2025
transport input ssh
exit

line console 0
password wmtech2025
login local
exit


enable secret wmtech2025


no ip domain-lookup
service password-encryption 

banner motd #Unauthorised access is prohibited!#

banner login #megbukunk geci xd#

ip domain-name wmtech.hu

crypto key generate rsa 

1024

ip ssh version 2
```

## bolondos forrgalomiráynitás *ospfv2*
```bash
router ospf 10
passive-interface g0/0
network 192.168.20.0 0.0.0.255 area 0
etwork 192.168.20.0 0.0.0.255 area  0
network 192.168.10.0 0.0.0.3 area  0
router-id 1.1.1.1
do clear ip ospf process
yes

ip route 0.0.0.0 0.0.0.0 serial 0/0/0

do wr
```
## klasszicista dinamikus gránát AKA *dhcpv4*

```bash
ip dhcp pool STUDENT
dns-server 209.165.201.10
default-router 192.168.10.6
network 192.168.30.0 255.255.255.0 
exit
ip dhcp excluded-address 192.168.30.1 192.168.30.5
do wr
```


## reneszánsz dinyamikus forgalomiráynitás AKA *ospfv3*
```bash
ipv6 unicast-routing

ipv6 router ospf  10
passive-interface g0/0
router-id 1.1.1.1
ex

int serial 0/0/0
ipv6 ospf 10 area 0 
ex

int g0/0
ipv6 ospf 10 area 0 
ex

do wr
```
__UWU__
