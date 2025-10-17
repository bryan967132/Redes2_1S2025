*Universidad de San Carlos de Guatemala*  
*Facultad de Ingenieria*  
*Escuela de Ciencias y Sistemas*  
*Redes De Computadoras 2*  
*Primer Semestre 2025*  
___
**202200048 - Christian Samuel Brán Mazariegos**  
**201908355 - Danny Hugo Bryan Tejaxún Pichiyá**  
**201612218 - Susan Pamela Herrera Monzón**  
___
## **Proyecto 1**

### Edificio Izquierdo
#### Subnetting
|VLAN|Hosts|ID|Primera IP Utilizable|Última IP Utilizable|Broadcast|Máscara de Subred|
|-|-|-|-|-|-|-|
|Naranja|30|`192.168.5.0`|`192.168.5.1`|`192.168.5.30`|`192.168.5.31`|`255.255.255.224` `/27`|
|Verde|30|`192.168.5.32`|`192.168.5.33`|`192.168.5.62`|`192.168.5.63`|`255.255.255.224` `/27`|

#### LACP
* SW1, SW2, SW3, SW4
```sh
enable
configure terminal
interface range Fa0/1-3
channel-protocol lacp
channel-group 2 mode active
exit
interface Port-channel2
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan all
no shutdown
exit
exit
wr
```

#### VTP
##### Servidor
* SW1
```sh
enable
configure terminal
vtp mode server
vtp domain proyecto1g5
vtp password sisale
vtp version 2
exit
wr
```

##### Cliente
* S1, S2, SW2, SW3, SW4
```sh
enable
configure terminal
vtp mode client
vtp domain proyecto1g5
vtp password sisale
exit
wr
```

#### Modo Troncal
* SW1
```sh
enable
configure terminal
ip routing
interface range Fa0/4-6
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan all
exit
exit
wr
```

* SW3
```sh
enable
configure terminal
ip routing
interface Fa0/4
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan all
exit
exit
wr
```

#### VLAN
* SW1
```sh
enable
configure terminal
vlan 10
name VLAN_Naranja_EdificioIZQ_5
exit
vlan 20
name VLAN_Verde_EdificioIZQ_5
exit
exit
wr
```

* SW4
```sh
enable
configure terminal
interface vlan 10
ip address 192.168.5.1 255.255.255.224
ip helper-address 10.0.5.30
ip access-group 110 in
no shutdown
exit
interface vlan 20
ip address 192.168.5.33 255.255.255.224
ip helper-address 10.0.5.30
ip access-group 112 in
no shutdown
exit
exit
wr
```

#### Modo Acceso
* S1
```sh
enable
configure terminal
interface range Fa0/11-12
switchport mode access
switchport access vlan 10
exit
exit
wr
```

* S2
```sh
enable
configure terminal
interface range Fa0/11-12
switchport mode access
switchport access vlan 20
exit
exit
wr
```

#### ACL
* SW4
```sh
enable
configure terminal
access-list 110 permit ip 192.168.5.0 0.0.0.31 192.168.5.96 0.0.0.31
access-list 112 permit ip 192.168.5.32 0.0.0.31 192.168.5.64 0.0.0.31
access-list 110 deny ip any any
access-list 112 deny ip any any
exit
wr
```

### Edificio Derecho
#### Subnetting
|VLAN|Hosts|ID|Primera IP Utilizable|Última IP Utilizable|Broadcast|Máscara de Subred|
|-|-|-|-|-|-|-|
|Verde|30|`192.168.5.64`|`192.168.5.65`|`192.168.5.94`|`192.168.5.95`|`255.255.255.224` `/27`|
|Naranja|30|`192.168.5.96`|`192.168.5.97`|`192.168.5.126`|`192.168.5.127`|`255.255.255.224` `/27`|


#### PAGP
* SW5, SW6, SW7, SW8
```sh
enable
configure terminal
interface range Fa0/1-3
channel-protocol pagp
channel-group 2 mode desirable
exit
interface Port-channel2
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan all
no shutdown
exit
exit
wr
```

#### VTP
##### Servidor
* SW5
```sh
enable
configure terminal
vtp mode server
vtp domain proyecto1g5
vtp password sisale
vtp version 2
exit
wr
```

##### Cliente
* S3, S4, SW6, SW7, SW8
```sh
enable
configure terminal
vtp mode client
vtp domain proyecto1g5
vtp password sisale
exit
wr
```

#### Modo Troncal
* SW5
```sh
enable
configure terminal
ip routing
interface range Fa0/4-6
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan all
exit
exit
wr
```

* SW6
```sh
enable
configure terminal
ip routing
interface Fa0/4
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan all
exit
exit
wr
```

#### VLAN
* SW5
```sh
enable
configure terminal
vlan 10
name VLAN_Naranja_EdificioDER_5
exit
vlan 20
name VLAN_Verde_EdificioDER_5
exit
exit
wr
```

* SW8
```sh
enable
configure terminal
interface vlan 10
ip address 192.168.5.97 255.255.255.224
ip helper-address 10.0.5.34
ip access-group 111 in
no shutdown
exit
interface vlan 20
ip address 192.168.5.65 255.255.255.224
ip helper-address 10.0.5.34
ip access-group 113 in
no shutdown
exit
exit
wr
```

#### Modo Acceso
* S3
```sh
enable
configure terminal
interface range Fa0/11-12
switchport mode access
switchport access vlan 20
exit
exit
wr
```

* S4
```sh
enable
configure terminal
interface range Fa0/11-12
switchport mode access
switchport access vlan 10
exit
exit
wr
```

#### ACL
* SW8
```sh
enable
configure terminal
access-list 111 permit ip 192.168.5.96 0.0.0.31 192.168.5.0 0.0.0.31
access-list 113 permit ip 192.168.5.64 0.0.0.31 192.168.5.32 0.0.0.31
access-list 111 deny ip any any
access-list 113 deny ip any any
exit
wr
```

### Edificio Administración
#### Subnetting
|VLAN|Hosts|ID|Primera IP Utilizable|Última IP Utilizable|Broadcast|Máscara de Subred|
|-|-|-|-|-|-|-|
|ADMIN|30|`192.168.5.128`|`192.168.5.129`|`192.168.5.158`|`192.168.5.159`|`255.255.255.224` `/27`|

#### VLAN
* SW9
```sh
enable
configure terminal
vlan 30
name VLAN_Azul_EdificioADMIN_5
exit
exit
wr
```

* SW9
```sh
enable
configure terminal
interface vlan 30
ip address 192.168.5.129 255.255.255.224
ip access-group 114 in
no shutdown
exit
exit
wr
```

#### Modo Acceso
* SW9
```sh
enable
configure terminal
interface Gi1/0/1
switchport mode access
switchport access vlan 30
exit
exit
wr
```

#### ACL
* SW9
```sh
enable
configure terminal
access-list 114 permit ip 192.168.5.128 0.0.0.31 192.168.5.0 0.0.0.31
access-list 114 permit ip 192.168.5.128 0.0.0.31 192.168.5.96 0.0.0.31
access-list 114 permit ip 192.168.5.128 0.0.0.31 192.168.5.32 0.0.0.31
access-list 114 permit ip 192.168.5.128 0.0.0.31 192.168.5.64 0.0.0.31
access-list 114 deny ip any any
exit
wr
```

### Data Center
#### Subnetting
|Hosts|ID|Primera IP Utilizable|Última IP Utilizable|Broadcast|Máscara de Subred|
|-|-|-|-|-|-|
|2|`10.0.5.28`|`10.0.5.29`|`10.0.5.30`|`10.0.5.31`|`255.255.255.252` `/30`|
|2|`10.0.5.32`|`10.0.5.33`|`10.0.5.34`|`10.0.5.35`|`255.255.255.252` `/30`|

#### DHCP1: Edificio Izquierdo
|Dispositivo|Gateway|Primera IP|Máscara de Subred|Máximo de Usuarios|
|-|-|-|-|-|
|Naranja|`192.168.5.1`|`192.168.5.2`|`255.255.255.224` `/27`|30|
|Verde|`192.168.5.33`|`192.168.5.34`|`255.255.255.224` `/27`|30|

#### DHCP2: Edificio Derecho
|Dispositivo|Gateway|Primera IP|Máscara de Subred|Máximo de Usuarios|
|-|-|-|-|-|
|Verde|`192.168.5.65`|`192.168.5.66`|`255.255.255.224` `/27`|30|
|Naranja|`192.168.5.97`|`192.168.5.98`|`255.255.255.224` `/27`|30|

### Core
#### Subnetting
|Hosts|ID|Primera IP Utilizable|Última IP Utilizable|Broadcast|Máscara de Subred|
|-|-|-|-|-|-|
|2|`10.0.5.0`|`10.0.5.1`|`10.0.5.2`|`10.0.5.3`|`255.255.255.252` `/30`|
|2|`10.0.5.4`|`10.0.5.5`|`10.0.5.6`|`10.0.5.7`|`255.255.255.252` `/30`|
|2|`10.0.5.8`|`10.0.5.9`|`10.0.5.10`|`10.0.5.11`|`255.255.255.252` `/30`|
|2|`10.0.5.12`|`10.0.5.13`|`10.0.5.14`|`10.0.5.15`|`255.255.255.252` `/30`|
|2|`10.0.5.16`|`10.0.5.17`|`10.0.5.18`|`10.0.5.19`|`255.255.255.252` `/30`|
|2|`10.0.5.20`|`10.0.5.21`|`10.0.5.22`|`10.0.5.23`|`255.255.255.252` `/30`|
|2|`10.0.5.24`|`10.0.5.25`|`10.0.5.26`|`10.0.5.27`|`255.255.255.252` `/30`|

#### Enrutamiento
##### Interfaces
* SW4
    - LACP: `Fa0/5-7` - `Port-Channel1`

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Fa0/5`|`10.0.5.22`|`255.255.255.252` `/30`|
|`Fa0/6`|||
|`Fa0/7`|||

* SW8
    - PAGP: `Fa0/5-7` - `Port-Channel1`

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Fa0/5`|`10.0.5.26`|`255.255.255.252` `/30`|
|`Fa0/6`|||
|`Fa0/7`|||

* SW9

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Gi1/1/1`|`10.0.5.14`|`255.255.255.252` `/30`|
|`Gi1/1/2`|`10.0.5.18`|`255.255.255.252` `/30`|

* SW10
    - LACP: `Gi1/0/1-3` - `Port-Channel1`

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Gi1/1/1`|`10.0.5.1`|`255.255.255.252` `/30`|
|`Gi1/1/2`|`10.0.5.9`|`255.255.255.252` `/30`|
|`Gi1/1/3`|`10.0.5.13`|`255.255.255.252` `/30`|
|`Gi1/0/1`|`10.0.5.21`|`255.255.255.252` `/30`|
|`Gi1/0/2`|||
|`Gi1/0/3`|||

* SW11
    - PAGP: `Gi1/0/1-3` - `Port-Channel1`

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Gi1/1/1`|`10.0.5.5`|`255.255.255.252` `/30`|
|`Gi1/1/2`|`10.0.5.10`|`255.255.255.252` `/30`|
|`Gi1/1/3`|`10.0.5.17`|`255.255.255.252` `/30`|
|`Gi1/0/1`|`10.0.5.25`|`255.255.255.252` `/30`|
|`Gi1/0/2`|||
|`Gi1/0/3`|||

* SW12

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Gi1/1/1`|`10.0.5.2`|`255.255.255.252` `/30`|
|`Gi1/1/2`|`10.0.5.6`|`255.255.255.252` `/30`|
|`Gi1/0/1`|`10.0.5.29`|`255.255.255.252` `/30`|
|`Gi1/0/2`|`10.0.5.33`|`255.255.255.252` `/30`|

#### LACP
* SW4
```sh
enable
configure terminal
ip routing
interface range Fa0/5-7
channel-protocol lacp
channel-group 1 mode active
exit
interface Port-channel1
no switchport
ip address 10.0.5.22 255.255.255.252
no shutdown
exit
exit
wr
```

* SW10
```sh
enable
configure terminal
ip routing
interface range Gi1/0/1-3
channel-protocol lacp
channel-group 1 mode active
exit
interface Port-channel1
no switchport
ip address 10.0.5.21 255.255.255.252
no shutdown
exit
exit
wr
```

#### PAGP
* SW8
```sh
enable
configure terminal
ip routing
interface range Fa0/5-7
channel-protocol pagp
channel-group 1 mode desirable
exit
interface Port-channel1
no switchport
ip address 10.0.5.26 255.255.255.252
no shutdown
exit
exit
wr
```

* SW11
```sh
enable
configure terminal
ip routing
interface range Gi1/0/1-3
channel-protocol pagp
channel-group 1 mode desirable
exit
interface Port-channel1
no switchport
ip address 10.0.5.25 255.255.255.252
no shutdown
exit
exit
wr
```

#### IP's
* SW9
```sh
enable
configure terminal
ip routing
interface Gi1/1/1
no switchport
ip address 10.0.5.14 255.255.255.252
no shutdown
exit
interface Gi1/1/2
no switchport
ip address 10.0.5.18 255.255.255.252
no shutdown
exit
exit
wr
```

* SW10
```sh
enable
configure terminal
ip routing
interface Gi1/1/1
no switchport
ip address 10.0.5.1 255.255.255.252
no shutdown
exit
interface Gi1/1/2
no switchport
ip address 10.0.5.9 255.255.255.252
no shutdown
exit
interface Gi1/1/3
no switchport
ip address 10.0.5.13 255.255.255.252
no shutdown
exit
exit
wr
```

* SW11
```sh
enable
configure terminal
ip routing
interface Gi1/1/1
no switchport
ip address 10.0.5.5 255.255.255.252
no shutdown
exit
interface Gi1/1/2
no switchport
ip address 10.0.5.10 255.255.255.252
no shutdown
exit
interface Gi1/1/3
no switchport
ip address 10.0.5.17 255.255.255.252
no shutdown
exit
exit
wr
```

* SW12
```sh
enable
configure terminal
ip routing
interface Gi1/1/1
no switchport
ip address 10.0.5.2 255.255.255.252
no shutdown
exit
interface Gi1/1/2
no switchport
ip address 10.0.5.6 255.255.255.252
no shutdown
exit
interface Gi1/0/1
no switchport
ip address 10.0.5.29 255.255.255.252
no shutdown
exit
interface Gi1/0/2
no switchport
ip address 10.0.5.33 255.255.255.252
no shutdown
exit
exit
wr
```

#### EIGRP
* SW9
```sh
enable
configure terminal
ip routing
router eigrp 10
network 10.0.5.12 0.0.0.3
network 10.0.5.16 0.0.0.3
network 192.168.5.128 0.0.0.31
exit
exit
wr
```

* SW10
```sh
enable
configure terminal
ip routing
router eigrp 10
network 10.0.5.0 0.0.0.3
network 10.0.5.8 0.0.0.3
network 10.0.5.12 0.0.0.3
no auto-summary
exit
exit
wr
```

* SW11
```sh
enable
configure terminal
ip routing
router eigrp 10
network 10.0.5.4 0.0.0.3
network 10.0.5.8 0.0.0.3
network 10.0.5.16 0.0.0.3
no auto-summary
exit
exit
wr
```

* SW12
```sh
enable
configure terminal
ip routing
router eigrp 10
network 10.0.5.0 0.0.0.3
network 10.0.5.4 0.0.0.3
network 10.0.5.28 0.0.0.3
network 10.0.5.32 0.0.0.3
exit
exit
wr
```

#### OSPF
* SW4
```sh
enable
configure terminal
ip routing
router ospf 10
network 10.0.5.20 0.0.0.3 area 1
network 192.168.5.0 0.0.0.31 area 1
network 192.168.5.32 0.0.0.31 area 1
exit
exit
wr
```

* SW8
```sh
enable
configure terminal
ip routing
router ospf 10
network 10.0.5.24 0.0.0.3 area 1
network 192.168.5.64 0.0.0.31 area 1
network 192.168.5.96 0.0.0.31 area 1
exit
exit
wr
```

* SW10
```sh
enable
configure terminal
ip routing
router ospf 10
network 10.0.5.20 0.0.0.3 area 1
exit
exit
wr
```

* SW11
```sh
enable
configure terminal
ip routing
router ospf 10
network 10.0.5.24 0.0.0.3 area 1
exit
exit
wr
```

### Redistribución
* SW10, SW11
```sh
enable
configure terminal
ip routing
router ospf 10
redistribute eigrp 10 metric 2 subnets
exit
router eigrp 10
redistribute ospf 10 metric 100000 10 255 1 1500
exit
exit
wr
```