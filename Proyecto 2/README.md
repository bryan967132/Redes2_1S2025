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
## **Proyecto 2**

### ISP1: Telecom Uno
#### Subnetting
* Red Principal: `192.168.15.0/24`

|Nombre|Hosts|ID Red|Primera IP Utilizable|Última IP Utilizable|Broadcast|Máscara de Subred|
|-|-|-|-|-|-|-|
|Administración 1|14|`192.168.15.0`|`192.168.15.1`|`192.168.15.14`|`192.168.15.15`|`255.255.255.240` `/28`|
|Administración 2|14|`192.168.15.16`|`192.168.15.17`|`192.168.15.30`|`192.168.15.31`|`255.255.255.240` `/28`|
|Administración 3|14|`192.168.15.32`|`192.168.15.33`|`192.168.15.46`|`192.168.15.47`|`255.255.255.240` `/28`|
|Atención al Cliente 1|14|`192.168.15.48`|`192.168.15.49`|`192.168.15.62`|`192.168.15.63`|`255.255.255.240` `/28`|
|Atención al Cliente 2|14|`192.168.15.64`|`192.168.15.65`|`192.168.15.78`|`192.168.15.79`|`255.255.255.240` `/28`|
|Atención al Cliente 3|14|`192.168.15.80`|`192.168.15.81`|`192.168.15.94`|`192.168.15.95`|`255.255.255.240` `/28`|
|DHCP Servers|6|`192.168.15.96`|`192.168.15.97`|`192.168.15.102`|`192.168.15.103`|`255.255.255.248` `/29`|
|Enrutamiento|2|`192.168.15.104`|`192.168.15.105`|`192.168.15.106`|`192.168.15.107`|`255.255.255.252` `/30`|
||2|`192.168.15.108`|`192.168.15.109`|`192.168.15.110`|`192.168.15.111`|`255.255.255.252` `/30`|
||2|`192.168.15.112`|`192.168.15.113`|`192.168.15.114`|`192.168.15.115`|`255.255.255.252` `/30`|
||2|`192.168.15.116`|`192.168.15.117`|`192.168.15.118`|`192.168.15.119`|`255.255.255.252` `/30`|
||2|`192.168.15.120`|`192.168.15.121`|`192.168.15.122`|`192.168.15.123`|`255.255.255.252` `/30`|

#### Enrutamiento
##### Interfaces
* SW10:
    - LACP: `Fa0/1-2` - `Port-Channel1`
    - LACP: `Fa0/3-4` - `Port-Channel2`
    - LACP: `Fa0/5-6` - `Port-Channel3`
    - LACP: `Fa0/7-8` - `Port-Channel4`
    - LACP: `Fa0/9-11` - `Port-Channel5`

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Fa0/1`|`192.168.15.105`|`255.255.255.252` `/30`|
|`Fa0/2`|||
|`Fa0/3`|`192.168.15.109`|`255.255.255.252` `/30`|
|`Fa0/4`|||
|`Fa0/5`|`192.168.15.113`|`255.255.255.252` `/30`|
|`Fa0/6`|||
|`Fa0/7`|`192.168.15.117`|`255.255.255.252` `/30`|
|`Fa0/8`|||
|`Fa0/9`|`192.168.15.121`|`255.255.255.252` `/30`|
|`Fa0/10`|||
|`Fa0/11`|||

* SW11
    - LACP `Fa0/1-2` - `Port-Channel1`

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Fa0/1`|`192.168.15.106`|`255.255.255.252` `/30`|
|`Fa0/2`|||

* SW12
    - LACP `Fa0/1-2` - `Port-Channel2`

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Fa0/1`|`192.168.15.110`|`255.255.255.252` `/30`|
|`Fa0/2`|||

* SW13
    - LACP `Fa0/1-2` - `Port-Channel3`

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Fa0/1`|`192.168.15.114`|`255.255.255.252` `/30`|
|`Fa0/2`|||

* SW14
    - LACP `Fa0/1-2` - `Port-Channel4`

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Fa0/1`|`192.168.15.118`|`255.255.255.252` `/30`|
|`Fa0/2`|||

* SW1
    - LACP `Gi1/0/1-3` - `Port-Channel5`

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Gi1/0/1`|`192.168.15.122`|`255.255.255.252` `/30`|
|`Gi1/0/2`|||
|`Gi1/0/3`|||

#### LACP
* SW10
```sh
enable
configure terminal
ip routing
interface range Fa0/1-2
channel-group 1 mode active
exit
interface Port-channel1
no switchport
ip address 192.168.15.105 255.255.255.252
no shutdown
exit
interface range Fa0/3-4
channel-group 2 mode active
exit
interface Port-channel2
no switchport
ip address 192.168.15.109 255.255.255.252
no shutdown
exit
interface range Fa0/5-6
channel-group 3 mode active
exit
interface Port-channel3
no switchport
ip address 192.168.15.113 255.255.255.252
no shutdown
exit
interface range Fa0/7-8
channel-group 4 mode active
exit
interface Port-channel4
no switchport
ip address 192.168.15.117 255.255.255.252
no shutdown
exit
interface range Fa0/9-11
channel-group 5 mode active
exit
interface Port-channel5
no switchport
ip address 192.168.15.121 255.255.255.252
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
interface range Fa0/1-2
channel-group 1 mode active
exit
interface Port-channel1
no switchport
ip address 192.168.15.106 255.255.255.252
no shutdown
exit
interface range Fa0/4-6
channel-group 7 mode active
exit
interface Port-channel7
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan all
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
interface range Fa0/1-2
channel-group 2 mode active
exit
interface Port-channel2
no switchport
ip address 192.168.15.110 255.255.255.252
no shutdown
exit
interface range Fa0/4-6
channel-group 7 mode active
exit
interface Port-channel7
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan all
no shutdown
exit
exit
wr
```

* SW13
```sh
enable
configure terminal
ip routing
interface range Fa0/1-2
channel-group 3 mode active
exit
interface Port-channel3
no switchport
ip address 192.168.15.114 255.255.255.252
no shutdown
exit
interface range Fa0/4-6
channel-group 7 mode active
exit
interface Port-channel7
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan all
no shutdown
exit
exit
wr
```

* SW14
```sh
enable
configure terminal
ip routing
interface range Fa0/1-2
channel-group 4 mode active
exit
interface Port-channel4
no switchport
ip address 192.168.15.118 255.255.255.252
no shutdown
exit
interface range Fa0/4-6
channel-group 7 mode active
exit
interface Port-channel7
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan all
no shutdown
exit
exit
wr
```

* SW1
```sh
enable
configure terminal
ip routing
interface range Gi1/0/1-3
channel-group 5 mode active
exit
interface Port-channel5
no switchport
ip address 192.168.15.122 255.255.255.252
no shutdown
exit
exit
wr
```

* SW111, SW122, SW132, SW142
```sh
enable
configure terminal
interface range Fa0/1-3
channel-group 7 mode active
exit
interface Port-channel7
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan all
no shutdown
exit
exit
wr
```

#### EIGRP
* SW10
```sh
enable
configure terminal
ip routing
router eigrp 10
network 192.168.15.104 0.0.0.3
network 192.168.15.108 0.0.0.3
network 192.168.15.112 0.0.0.3
network 192.168.15.116 0.0.0.3
network 192.168.15.120 0.0.0.3
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
network 192.168.15.96 0.0.0.7
network 192.168.15.104 0.0.0.3
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
network 192.168.15.0 0.0.0.15
network 192.168.15.48 0.0.0.15
network 192.168.15.108 0.0.0.3
exit
exit
wr
```

* SW13
```sh
enable
configure terminal
ip routing
router eigrp 10
network 192.168.15.16 0.0.0.15
network 192.168.15.64 0.0.0.15
network 192.168.15.112 0.0.0.3
exit
exit
wr
```

* SW14
```sh
enable
configure terminal
ip routing
router eigrp 10
network 192.168.15.32 0.0.0.15
network 192.168.15.80 0.0.0.15
network 192.168.15.116 0.0.0.3
exit
exit
wr
```

* SW1
```sh
enable
configure terminal
ip routing
router eigrp 10
network 192.168.15.120 0.0.0.3
no auto-summary
exit
exit
wr
```

```sh
enable
configure terminal
ip routing
router eigrp 10
redistribute bgp 100 metric 100000 100 255 1 1500
exit
exit
wr
```

#### VLAN
|Área|Nombre|ID|
|-|-|-|
|Administración|`ADMINISTRACION`|115|
|Atención al Cliente|`ATENCION_AL_CLIENTE`|125|
|DHCP SERVERS|`DHCP_SERVERS`|135|

* SW11, SW111
```sh
enable
configure terminal
vlan 135
name DHCP_SERVERS
exit
exit
wr
```

* SW12, SW121, SW122, SW13, SW131, SW132, SW14, SW141, SW142
```sh
enable
configure terminal
vlan 115
name ADMINISTRACION
exit
vlan 125
name ATENCION_AL_CLIENTE
exit
exit
wr
```

* SW11
```sh
enable
configure terminal
interface vlan 135
ip address 192.168.15.97 255.255.255.248
no shutdown
exit
exit
wr
```

* SW111
```sh
enable
configure terminal
interface range Fa0/11-13
switchport access vlan 135
no shutdown
exit
exit
wr
```

* SW12
```sh
enable
configure terminal
interface vlan 115
ip address 192.168.15.1 255.255.255.240
ip helper-address 192.168.15.98
no shutdown
exit
interface vlan 125
ip address 192.168.15.49 255.255.255.240
ip helper-address 192.168.15.98
no shutdown
exit
interface Fa0/3
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan all
no shutdown
exit
exit
wr
```

* SW13
```sh
enable
configure terminal
interface vlan 115
ip address 192.168.15.17 255.255.255.240
ip helper-address 192.168.15.98
no shutdown
exit
interface vlan 125
ip address 192.168.15.65 255.255.255.240
ip helper-address 192.168.15.98
no shutdown
exit
interface Fa0/3
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan all
no shutdown
exit
exit
wr
```

* SW14
```sh
enable
configure terminal
interface vlan 115
ip address 192.168.15.33 255.255.255.240
ip helper-address 192.168.15.98
no shutdown
exit
interface vlan 125
ip address 192.168.15.81 255.255.255.240
ip helper-address 192.168.15.98
no shutdown
exit
interface Fa0/3
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan all
no shutdown
exit
exit
wr
```

* SW121, SW131, SW141
```sh
enable
configure terminal
interface Fa0/1
switchport mode trunk
switchport trunk allowed vlan all
no shutdown
exit
interface Fa0/11
switchport mode access
switchport access vlan 115
no shutdown
exit
interface Fa0/12
switchport mode access
switchport access vlan 125
no shutdown
exit
exit
wr
```

* SW122, SW142
```sh
enable
configure terminal
interface Fa0/11
switchport mode access
switchport access vlan 115
no shutdown
exit
exit
wr
```

* SW132
```sh
enable
configure terminal
interface Fa0/11
switchport mode access
switchport access vlan 125
no shutdown
exit
exit
wr
```

### ISP2: Redes Nacionales
#### Subnetting
* Red Principal: `192.168.25.0/24`

|Nombre|Hosts|ID Red|Primera IP Utilizable|Última IP Utilizable|Broadcast|Máscara de Subred|
|-|-|-|-|-|-|-|
|Ventas 1|14|`192.168.25.0`|`192.168.25.1`|`192.168.25.14`|`192.168.25.15`|`255.255.255.240` `/28`|
|Ventas 2|14|`192.168.25.16`|`192.168.25.17`|`192.168.25.30`|`192.168.25.31`|`255.255.255.240` `/28`|
|Ventas 3|14|`192.168.25.32`|`192.168.25.33`|`192.168.25.46`|`192.168.25.47`|`255.255.255.240` `/28`|
|Ventas 4|14|`192.168.25.48`|`192.168.25.49`|`192.168.25.62`|`192.168.25.63`|`255.255.255.240` `/28`|
|Facturación 1|14|`192.168.25.64`|`192.168.25.65`|`192.168.25.78`|`192.168.25.79`|`255.255.255.240` `/28`|
|Facturación 2|14|`192.168.25.80`|`192.168.25.81`|`192.168.25.94`|`192.168.25.95`|`255.255.255.240` `/28`|
|Facturación 3|14|`192.168.25.96`|`192.168.25.97`|`192.168.25.110`|`192.168.25.111`|`255.255.255.240` `/28`|
|Facturación 4|14|`192.168.25.112`|`192.168.25.113`|`192.168.25.126`|`192.168.25.127`|`255.255.255.240` `/28`|
|Wireless 1|14|`192.168.25.128`|`192.168.25.129`|`192.168.25.142`|`192.168.25.143`|`255.255.255.240` `/28`|
|Wireless 2|14|`192.168.25.144`|`192.168.25.145`|`192.168.25.158`|`192.168.25.159`|`255.255.255.240` `/28`|
|Enrutamiento|2|`192.168.25.160`|`192.168.25.161`|`192.168.25.162`|`192.168.25.163`|`255.255.255.252` `/30`|
||2|`192.168.25.164`|`192.168.25.165`|`192.168.25.166`|`192.168.25.167`|`255.255.255.252` `/30`|
||2|`192.168.25.168`|`192.168.25.169`|`192.168.25.170`|`192.168.25.171`|`255.255.255.252` `/30`|
||2|`192.168.25.172`|`192.168.25.173`|`192.168.25.174`|`192.168.25.175`|`255.255.255.252` `/30`|
||2|`192.168.25.176`|`192.168.25.177`|`192.168.25.178`|`192.168.25.179`|`255.255.255.252` `/30`|
||2|`192.168.25.180`|`192.168.25.181`|`192.168.25.182`|`192.168.25.183`|`255.255.255.252` `/30`|
||2|`192.168.25.184`|`192.168.25.185`|`192.168.25.186`|`192.168.25.187`|`255.255.255.252` `/30`|

#### Enrutamiento
##### Interfaces
* SW20:
    - LACP: `Fa0/1-2` - `Port-Channel1`
    - LACP: `Fa0/3-4` - `Port-Channel2`
    - LACP: `Fa0/5-6` - `Port-Channel3`
    - LACP: `Fa0/7-8` - `Port-Channel4`
    - LACP: `Fa0/9-11` - `Port-Channel5`

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Fa0/1`|`192.168.25.161`|`255.255.255.252` `/30`|
|`Fa0/2`|||
|`Fa0/3`|`192.168.25.165`|`255.255.255.252` `/30`|
|`Fa0/4`|||
|`Fa0/5`|`192.168.25.169`|`255.255.255.252` `/30`|
|`Fa0/6`|||
|`Fa0/7`|`192.168.25.173`|`255.255.255.252` `/30`|
|`Fa0/8`|||
|`Fa0/9`|`192.168.25.185`|`255.255.255.252` `/30`|
|`Fa0/10`|||
|`Fa0/11`|||
|`Fa0/12`|`192.168.25.177`|`255.255.255.252` `/30`|
|`Fa0/13`|`192.168.25.181`|`255.255.255.252` `/30`|

* SW21
    - LACP `Fa0/1-2` - `Port-Channel1`

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Fa0/1`|`192.168.15.162`|`255.255.255.252` `/30`|
|`Fa0/2`|||

* SW22
    - LACP `Fa0/1-2` - `Port-Channel2`

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Fa0/1`|`192.168.15.166`|`255.255.255.252` `/30`|
|`Fa0/2`|||

* SW23
    - LACP `Fa0/1-2` - `Port-Channel3`

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Fa0/1`|`192.168.15.170`|`255.255.255.252` `/30`|
|`Fa0/2`|||

* SW24
    - LACP `Fa0/1-2` - `Port-Channel4`

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Fa0/1`|`192.168.15.174`|`255.255.255.252` `/30`|
|`Fa0/2`|||

* SW2
    - LACP `Fa0/1-2` - `Port-Channel5`

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Gi1/0/1`|`192.168.25.186`|`255.255.255.252` `/30`|
|`Gi1/0/2`|||
|`Gi1/0/3`|||

#### LACP
* SW20
```sh
enable
configure terminal
ip routing
interface range Fa0/1-2
channel-group 1 mode active
exit
interface Port-channel1
no switchport
ip address 192.168.25.161 255.255.255.252
no shutdown
exit
interface range Fa0/3-4
channel-group 2 mode active
exit
interface Port-channel2
no switchport
ip address 192.168.25.165 255.255.255.252
no shutdown
exit
interface range Fa0/5-6
channel-group 3 mode active
exit
interface Port-channel3
no switchport
ip address 192.168.25.169 255.255.255.252
no shutdown
exit
interface range Fa0/7-8
channel-group 4 mode active
exit
interface Port-channel4
no switchport
ip address 192.168.25.173 255.255.255.252
no shutdown
exit
interface range Fa0/9-11
channel-group 5 mode active
exit
interface Port-channel5
no switchport
ip address 192.168.25.185 255.255.255.252
no shutdown
exit
interface Fa0/12
no switchport
ip address 192.168.25.177 255.255.255.252
no shutdown
exit
interface Fa0/13
no switchport
ip address 192.168.25.181 255.255.255.252
no shutdown
exit
exit
wr
```

* SW21
```sh
enable
configure terminal
ip routing
interface range Fa0/1-2
channel-group 1 mode active
exit
interface Port-channel1
no switchport
ip address 192.168.25.162 255.255.255.252
no shutdown
exit
exit
wr
```

* SW22
```sh
enable
configure terminal
ip routing
interface range Fa0/1-2
channel-group 2 mode active
exit
interface Port-channel2
no switchport
ip address 192.168.25.166 255.255.255.252
no shutdown
exit
exit
wr
```

* SW23
```sh
enable
configure terminal
ip routing
interface range Fa0/1-2
channel-group 3 mode active
exit
interface Port-channel3
no switchport
ip address 192.168.25.170 255.255.255.252
no shutdown
exit
exit
wr
```

* SW24
```sh
enable
configure terminal
ip routing
interface range Fa0/1-2
channel-group 4 mode active
exit
interface Port-channel4
no switchport
ip address 192.168.25.174 255.255.255.252
no shutdown
exit
exit
wr
```

* SW2
```sh
enable
configure terminal
ip routing
interface range Gi1/0/1-3
channel-group 5 mode active
exit
interface Port-channel5
no switchport
ip address 192.168.25.186 255.255.255.252
no shutdown
exit
exit
wr
```

#### EIGRP
* SW20
```sh
enable
configure terminal
ip routing
router eigrp 20
network 192.168.25.160 0.0.0.3
network 192.168.25.164 0.0.0.3
network 192.168.25.168 0.0.0.3
network 192.168.25.172 0.0.0.3
network 192.168.25.176 0.0.0.3
network 192.168.25.180 0.0.0.3
network 192.168.25.184 0.0.0.3
exit
exit
wr
```

* SW21
```sh
enable
configure terminal
ip routing
router eigrp 20
network 192.168.25.0 0.0.0.15
network 192.168.25.64 0.0.0.15
network 192.168.25.160 0.0.0.3
exit
exit
wr
```

* SW22
```sh
enable
configure terminal
ip routing
router eigrp 20
network 192.168.25.16 0.0.0.15
network 192.168.25.80 0.0.0.15
network 192.168.25.164 0.0.0.3
exit
exit
wr
```

* SW23
```sh
enable
configure terminal
ip routing
router eigrp 20
network 192.168.25.32 0.0.0.15
network 192.168.25.96 0.0.0.15
network 192.168.25.168 0.0.0.3
exit
exit
wr
```

* SW24
```sh
enable
configure terminal
ip routing
router eigrp 20
network 192.168.25.48 0.0.0.15
network 192.168.25.112 0.0.0.15
network 192.168.25.172 0.0.0.3
exit
exit
wr
```

* SW2
```sh
enable
configure terminal
ip routing
router eigrp 20
network 192.168.25.184 0.0.0.3
no auto-summary
exit
exit
wr
```

```sh
enable
configure terminal
ip routing
router eigrp 20
redistribute bgp 200 metric 100000 100 255 1 1500
exit
exit
wr
```

#### VTP
##### Servidores
* SW210, SW220, SW230, SW240
```sh
enable
configure terminal
vtp mode server
vtp domain Grupo5
vtp password 1S2025
vtp version 2
exit
wr
```

##### Clientes
* SW211, SW212, SW221, SW222, SW231, SW232, SW241, SW242
```sh
enable
configure terminal
vtp mode client
vtp domain Grupo5
vtp password 1S2025
exit
wr
```

#### VLAN
|Área|Nombre|ID|
|-|-|-|
|Ventas|`VENTAS`|215|
|Facturación|`FACTURACION`|225|

* SW21 - SW24
```sh
enable
configure terminal
interface Fa0/3
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan all
exit
exit
wr
```

* SW210, SW220, SW230, SW240
```sh
enable
configure terminal
interface range Fa0/1-3
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan all
exit
exit
wr
```

* SW211, SW212, SW221, SW222, SW231, SW232, SW241, SW242
```sh
enable
configure terminal
interface Fa0/1
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan all
exit
exit
wr
```

* SW21 - SW24, SW210, SW220, SW230, SW240
```sh
enable
configure terminal
vlan 215
name VENTAS
exit
vlan 225
name FACTURACION
exit
exit
wr
```

* SW211, SW221, SW231, SW241
```sh
enable
configure terminal
interface range Fa0/2-3
switchport access vlan 215
no shutdown
exit
exit
wr
```

* SW212, SW222, SW232, SW242
```sh
enable
configure terminal
interface range Fa0/2-3
switchport access vlan 225
no shutdown
exit
exit
wr
```

* SW21
```sh
enable
configure terminal
interface vlan 215
ip address 192.168.25.1 255.255.255.240
ip helper-address 192.168.15.99
no shutdown
exit
interface vlan 225
ip address 192.168.25.65 255.255.255.240
ip helper-address 192.168.15.99
no shutdown
exit
exit
wr
```

* SW22
```sh
enable
configure terminal
interface vlan 215
ip address 192.168.25.17 255.255.255.240
ip helper-address 192.168.15.99
no shutdown
exit
interface vlan 225
ip address 192.168.25.81 255.255.255.240
ip helper-address 192.168.15.99
no shutdown
exit
exit
wr
```

* SW23
```sh
enable
configure terminal
interface vlan 215
ip address 192.168.25.33 255.255.255.240
ip helper-address 192.168.15.99
no shutdown
exit
interface vlan 225
ip address 192.168.25.97 255.255.255.240
ip helper-address 192.168.15.99
no shutdown
exit
exit
wr
```

* SW24
```sh
enable
configure terminal
interface vlan 215
ip address 192.168.25.49 255.255.255.240
ip helper-address 192.168.15.99
no shutdown
exit
interface vlan 225
ip address 192.168.25.113 255.255.255.240
ip helper-address 192.168.15.99
no shutdown
exit
exit
wr
```

### ISP3: Conexiones Futuras
#### Subnetting
* Red Principal: `192.168.35.0/24`

|Nombre|Hosts|ID Red|Primera IP Utilizable|Última IP Utilizable|Broadcast|Máscara de Subred|
|-|-|-|-|-|-|-|
|Soporte 1|14|`192.168.35.0`|`192.168.35.1`|`192.168.35.14`|`192.168.35.15`|`255.255.255.240` `/28`|
|Soporte 2|14|`192.168.35.16`|`192.168.35.17`|`192.168.35.30`|`192.168.35.31`|`255.255.255.240` `/28`|
|Seguridad 1|14|`192.168.35.32`|`192.168.35.33`|`192.168.35.46`|`192.168.35.47`|`255.255.255.240` `/28`|
|Seguridad 2|14|`192.168.35.48`|`192.168.35.49`|`192.168.35.62`|`192.168.35.63`|`255.255.255.240` `/28`|
|Web Servers|6|`192.168.35.64`|`192.168.35.65`|`192.168.35.70`|`192.168.35.71`|`255.255.255.248` `/29`|
|Enrutamiento|2|`192.168.35.72`|`192.168.35.73`|`192.168.35.74`|`192.168.35.75`|`255.255.255.252` `/30`|
||2|`192.168.35.76`|`192.168.35.77`|`192.168.35.78`|`192.168.35.79`|`255.255.255.252` `/30`|
||2|`192.168.35.80`|`192.168.35.81`|`192.168.35.82`|`192.168.35.83`|`255.255.255.252` `/30`|
||2|`192.168.35.84`|`192.168.35.85`|`192.168.35.86`|`192.168.35.87`|`255.255.255.252` `/30`|
||2|`192.168.35.88`|`192.168.35.89`|`192.168.35.90`|`192.168.35.91`|`255.255.255.252` `/30`|
||2|`192.168.35.92`|`192.168.35.93`|`192.168.35.94`|`192.168.35.95`|`255.255.255.252` `/30`|
||2|`192.168.35.96`|`192.168.35.97`|`192.168.35.98`|`192.168.35.99`|`255.255.255.252` `/30`|
||2|`192.168.35.100`|`192.168.35.101`|`192.168.35.102`|`192.168.35.103`|`255.255.255.252` `/30`|
||2|`192.168.35.104`|`192.168.35.105`|`192.168.35.106`|`192.168.35.107`|`255.255.255.252` `/30`|
||2|`192.168.35.108`|`192.168.35.109`|`192.168.35.110`|`192.168.35.111`|`255.255.255.252` `/30`|
||2|`192.168.35.112`|`192.168.35.113`|`192.168.35.114`|`192.168.35.115`|`255.255.255.252` `/30`|
||2|`192.168.35.116`|`192.168.35.117`|`192.168.35.118`|`192.168.35.119`|`255.255.255.252` `/30`|
||2|`192.168.35.120`|`192.168.35.121`|`192.168.35.122`|`192.168.35.123`|`255.255.255.252` `/30`|
||2|`192.168.35.124`|`192.168.35.125`|`192.168.35.126`|`192.168.35.127`|`255.255.255.252` `/30`|
||2|`192.168.35.128`|`192.168.35.129`|`192.168.35.130`|`192.168.35.131`|`255.255.255.252` `/30`|

#### Enrutamiento
##### Interfaces
* SW3:
    - LACP: `Gi1/0/1-3` - `Port-Channel1`
    - LACP: `Gi1/0/4-6` - `Port-Channel2`

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Gi1/0/1`|`192.168.35.73`|`255.255.255.252` `/30`|
|`Gi1/0/2`|||
|`Gi1/0/3`|||
|`Gi1/0/4`|`192.168.35.77`|`255.255.255.252` `/30`|
|`Gi1/0/5`|||
|`Gi1/0/6`|||

* SW300:
    - LACP: `Fa0/1-3` - `Port-Channel1`
    - LACP: `Fa0/4-6` - `Port-Channel3`

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Fa0/1`|`192.168.35.74`|`255.255.255.252` `/30`|
|`Fa0/2`|||
|`Fa0/3`|||
|`Fa0/4`|`192.168.35.81`|`255.255.255.252` `/30`|
|`Fa0/5`|||
|`Fa0/6`|||
|`Fa0/7`|`192.168.35.85`|`255.255.255.252` `/30`|
|`Fa0/8`|`192.168.35.89`|`255.255.255.252` `/30`|
|`Fa0/9`|`192.168.35.93`|`255.255.255.252` `/30`|

* SW301:
    - LACP: `Fa0/1-3` - `Port-Channel2`
    - LACP: `Fa0/4-6` - `Port-Channel3`

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Fa0/1`|`192.168.35.78`|`255.255.255.252` `/30`|
|`Fa0/2`|||
|`Fa0/3`|||
|`Fa0/4`|`192.168.35.82`|`255.255.255.252` `/30`|
|`Fa0/5`|||
|`Fa0/6`|||
|`Fa0/7`|`192.168.35.97`|`255.255.255.252` `/30`|
|`Fa0/8`|`192.168.35.101`|`255.255.255.252` `/30`|
|`Fa0/9`|`192.168.35.105`|`255.255.255.252` `/30`|

* SW31:

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Fa0/1`|`192.168.35.86`|`255.255.255.252` `/30`|
|`Fa0/2`|`192.168.35.98`|`255.255.255.252` `/30`|
|`Fa0/3`|`192.168.35.109`|`255.255.255.252` `/30`|
|`Fa0/4`|`192.168.35.113`|`255.255.255.252` `/30`|

* SW32:

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Fa0/1`|`192.168.35.90`|`255.255.255.252` `/30`|
|`Fa0/2`|`192.168.35.102`|`255.255.255.252` `/30`|
|`Fa0/3`|`192.168.35.117`|`255.255.255.252` `/30`|
|`Fa0/4`|`192.168.35.121`|`255.255.255.252` `/30`|

* SW33:

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Fa0/1`|`192.168.35.94`|`255.255.255.252` `/30`|
|`Fa0/2`|`192.168.35.106`|`255.255.255.252` `/30`|
|`Fa0/3`|`192.168.35.125`|`255.255.255.252` `/30`|
|`Fa0/4`|`192.168.35.129`|`255.255.255.252` `/30`|

* R311:

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Gi0/0`|`192.168.35.110`|`255.255.255.252` `/30`|

* R312:

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Gi0/0`|`192.168.35.114`|`255.255.255.252` `/30`|

* R321:

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Gi0/0`|`192.168.35.118`|`255.255.255.252` `/30`|

* R322:

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Gi0/0`|`192.168.35.122`|`255.255.255.252` `/30`|

* R331:

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Gi0/0`|`192.168.35.126`|`255.255.255.252` `/30`|

* R332:

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Gi0/0`|`192.168.35.130`|`255.255.255.252` `/30`|

#### LACP
* SW3
```sh
enable
configure terminal
ip routing
interface range Gi1/0/1-3
channel-group 1 mode active
exit
interface Port-channel1
no switchport
ip address 192.168.35.73 255.255.255.252
no shutdown
exit
interface range Gi1/0/4-6
channel-group 2 mode active
exit
interface Port-channel2
no switchport
ip address 192.168.35.77 255.255.255.252
no shutdown
exit
exit
wr
```

* SW300
```sh
enable
configure terminal
ip routing
interface range Fa0/1-3
channel-group 1 mode active
exit
interface Port-channel1
no switchport
ip address 192.168.35.74 255.255.255.252
no shutdown
exit
interface range Fa0/4-6
channel-group 3 mode active
exit
interface Port-channel3
no switchport
ip address 192.168.35.81 255.255.255.252
no shutdown
exit
interface Fa0/7
no switchport
ip address 192.168.35.85 255.255.255.252
no shutdown
exit
interface Fa0/8
no switchport
ip address 192.168.35.89 255.255.255.252
no shutdown
exit
interface Fa0/9
no switchport
ip address 192.168.35.93 255.255.255.252
no shutdown
exit
exit
wr
```

* SW301
```sh
enable
configure terminal
ip routing
interface range Fa0/1-3
channel-group 2 mode active
exit
interface Port-channel2
no switchport
ip address 192.168.35.78 255.255.255.252
no shutdown
exit
interface range Fa0/4-6
channel-group 3 mode active
exit
interface Port-channel3
no switchport
ip address 192.168.35.82 255.255.255.252
no shutdown
exit
interface Fa0/7
no switchport
ip address 192.168.35.97 255.255.255.252
no shutdown
exit
interface Fa0/8
no switchport
ip address 192.168.35.101 255.255.255.252
no shutdown
exit
interface Fa0/9
no switchport
ip address 192.168.35.105 255.255.255.252
no shutdown
exit
exit
wr
```

#### OSPF
* SW3
```sh
enable
configure terminal
ip routing
router ospf 30
network 192.168.35.72 0.0.0.3 area 1
network 192.168.35.76 0.0.0.3 area 1
exit
exit
wr
```

```sh
enable
configure terminal
ip routing
router ospf 30
redistribute bgp 300 subnets
exit
exit
wr
```

* SW300
```sh
enable
configure terminal
ip routing
router ospf 30
network 192.168.35.72 0.0.0.3 area 1
network 192.168.35.80 0.0.0.3 area 1
network 192.168.35.84 0.0.0.3 area 1
network 192.168.35.88 0.0.0.3 area 1
network 192.168.35.92 0.0.0.3 area 1
exit
exit
wr
```

* SW301
```sh
enable
configure terminal
ip routing
router ospf 30
network 192.168.35.76 0.0.0.3 area 1
network 192.168.35.80 0.0.0.3 area 1
network 192.168.35.96 0.0.0.3 area 1
network 192.168.35.100 0.0.0.3 area 1
network 192.168.35.104 0.0.0.3 area 1
exit
exit
wr
```

* SW31
```sh
enable
configure terminal
ip routing
interface Fa0/1
no switchport
ip address 192.168.35.86 255.255.255.252
no shutdown
exit
interface Fa0/2
no switchport
ip address 192.168.35.98 255.255.255.252
no shutdown
exit
interface Fa0/3
no switchport
ip address 192.168.35.109 255.255.255.252
no shutdown
exit
interface Fa0/4
no switchport
ip address 192.168.35.113 255.255.255.252
no shutdown
exit
router ospf 30
network 192.168.35.84 0.0.0.3 area 1
network 192.168.35.96 0.0.0.3 area 1
network 192.168.35.108 0.0.0.3 area 1
network 192.168.35.112 0.0.0.3 area 1
exit
exit
wr
```

* SW32
```sh
enable
configure terminal
ip routing
interface Fa0/1
no switchport
ip address 192.168.35.90 255.255.255.252
no shutdown
exit
interface Fa0/2
no switchport
ip address 192.168.35.102 255.255.255.252
no shutdown
exit
interface Fa0/3
no switchport
ip address 192.168.35.117 255.255.255.252
no shutdown
exit
interface Fa0/4
no switchport
ip address 192.168.35.121 255.255.255.252
no shutdown
exit
router ospf 30
network 192.168.35.88 0.0.0.3 area 1
network 192.168.35.100 0.0.0.3 area 1
network 192.168.35.116 0.0.0.3 area 1
network 192.168.35.120 0.0.0.3 area 1
exit
exit
wr
```

* SW33
```sh
enable
configure terminal
ip routing
interface Fa0/1
no switchport
ip address 192.168.35.94 255.255.255.252
no shutdown
exit
interface Fa0/2
no switchport
ip address 192.168.35.106 255.255.255.252
no shutdown
exit
interface Fa0/3
no switchport
ip address 192.168.35.125 255.255.255.252
no shutdown
exit
interface Fa0/4
no switchport
ip address 192.168.35.129 255.255.255.252
no shutdown
exit
router ospf 30
network 192.168.35.92 0.0.0.3 area 1
network 192.168.35.104 0.0.0.3 area 1
network 192.168.35.124 0.0.0.3 area 1
network 192.168.35.128 0.0.0.3 area 1
exit
exit
wr
```

* R311
```sh
enable
configure terminal
interface Gi0/0
ip address 192.168.35.110 255.255.255.252
no shutdown
exit
router ospf 30
network 192.168.35.64 0.0.0.7 area 1
network 192.168.35.108 0.0.0.3 area 1
exit
exit
write memory
```

* R312
```sh
enable
configure terminal
interface Gi0/0
ip address 192.168.35.114 255.255.255.252
no shutdown
exit
router ospf 30
network 192.168.35.64 0.0.0.7 area 1
network 192.168.35.112 0.0.0.3 area 1
exit
exit
write memory
```

* R321
```sh
enable
configure terminal
interface Gi0/0
ip address 192.168.35.118 255.255.255.252
no shutdown
exit
router ospf 30
network 192.168.35.0 0.0.0.15 area 1
network 192.168.35.32 0.0.0.15 area 1
network 192.168.35.116 0.0.0.3 area 1
exit
exit
write memory
```

* R322
```sh
enable
configure terminal
interface Gi0/0
ip address 192.168.35.122 255.255.255.252
no shutdown
exit
router ospf 30
network 192.168.35.0 0.0.0.15 area 1
network 192.168.35.32 0.0.0.15 area 1
network 192.168.35.120 0.0.0.3 area 1
exit
exit
write memory
```

* R331
```sh
enable
configure terminal
interface Gi0/0
ip address 192.168.35.126 255.255.255.252
no shutdown
exit
router ospf 30
network 192.168.35.16 0.0.0.15 area 1
network 192.168.35.48 0.0.0.15 area 1
network 192.168.35.124 0.0.0.3 area 1
exit
exit
write memory
```

* R332
```sh
enable
configure terminal
interface Gi0/0
ip address 192.168.35.130 255.255.255.252
no shutdown
exit
router ospf 30
network 192.168.35.16 0.0.0.15 area 1
network 192.168.35.48 0.0.0.15 area 1
network 192.168.35.128 0.0.0.3 area 1
exit
exit
write memory
```

#### HSRP
* R311
```sh
enable
configure terminal
interface gi0/1
no shutdown
interface gi0/1.335
encapsulation dot1q 335
ip address 192.168.35.66 255.255.255.240
standby 1 ip 192.168.35.65
standby 1 priority 150
standby 1 preempt
exit
exit
wr
```

* R312
```sh
enable
configure terminal
interface gi0/1
no shutdown
interface gi0/1.335
encapsulation dot1q 335
ip address 192.168.35.67 255.255.255.240
standby 1 ip 192.168.35.65
exit
exit
wr
```

* R321
```sh
enable
configure terminal
interface gi0/1
no shutdown
interface gi0/1.315
encapsulation dot1q 315
ip address 192.168.35.2 255.255.255.240
ip helper-address 192.168.15.100
standby 1 ip 192.168.35.1
standby 1 priority 150
standby 1 preempt
exit
interface gi0/1.325
encapsulation dot1q 325
ip address 192.168.35.34 255.255.255.240
ip helper-address 192.168.15.100
standby 2 ip 192.168.35.33
standby 2 priority 150
standby 2 preempt
exit
exit
wr
```

* R322
```sh
enable
configure terminal
interface gi0/1
no shutdown
interface gi0/1.315
encapsulation dot1q 315
ip address 192.168.35.3 255.255.255.240
ip helper-address 192.168.15.100
standby 1 ip 192.168.35.1
exit
interface gi0/1.325
encapsulation dot1q 325
ip address 192.168.35.35 255.255.255.240
ip helper-address 192.168.15.100
standby 2 ip 192.168.35.33
exit
exit
wr
```

* R331
```sh
enable
configure terminal
interface gi0/1
no shutdown
interface gi0/1.315
encapsulation dot1q 315
ip address 192.168.35.18 255.255.255.240
ip helper-address 192.168.15.100
standby 1 ip 192.168.35.17
standby 1 priority 150
standby 1 preempt
exit
interface gi0/1.325
encapsulation dot1q 325
ip address 192.168.35.50 255.255.255.240
ip helper-address 192.168.15.100
standby 2 ip 192.168.35.49
standby 2 priority 150
standby 2 preempt
exit
exit
wr
```

* R332
```sh
enable
configure terminal
interface gi0/1
no shutdown
interface gi0/1.315
encapsulation dot1q 315
ip address 192.168.35.19 255.255.255.240
ip helper-address 192.168.15.100
standby 1 ip 192.168.35.17
exit
interface gi0/1.325
encapsulation dot1q 325
ip address 192.168.35.51 255.255.255.240
ip helper-address 192.168.15.100
standby 2 ip 192.168.35.49
exit
exit
wr
```

#### VLAN
|Área|Nombre|ID|
|-|-|-|
|Soporte|`SOPORTE`|315|
|Seguridad|`SEGURIDAD`|325|
|Web Servers|`WEB_SERVERS`|325|

* SW310, SW320, SW330
```sh
enable
configure terminal
interface range Fa0/1-3
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan all
exit
exit
wr
```

* SW310, SW3100
```sh
enable
configure terminal
vlan 335
name WEB_SERVERS
exit
exit
wr
```

* SW320, SW330, SW3200, SW3300
```sh
enable
configure terminal
vlan 315
name SOPORTE
exit
vlan 325
name SEGURIDAD
exit
exit
wr
```

* SW3100
```sh
enable
configure terminal
interface Fa0/11
switchport access vlan 335
no shutdown
exit
exit
wr
```

* SW3200, SW3300
```sh
enable
configure terminal
interface Fa0/11
switchport access vlan 315
no shutdown
exit
interface Fa0/12
switchport access vlan 325
no shutdown
exit
exit
wr
```

### Core
#### Subnetting
* Red Principal: `172.5.0.0/16`

|Hosts|ID Red|Primera IP Utilizable|Última IP Utilizable|Broadcast|Máscara de Subred|
|-|-|-|-|-|-|
|2|`172.5.0.0`|`172.5.0.1`|`172.5.0.2`|`172.5.0.3`|`255.255.255.252` `/30`|
|2|`172.5.0.4`|`172.5.0.5`|`172.5.0.6`|`172.5.0.7`|`255.255.255.252` `/30`|
|2|`172.5.0.8`|`172.5.0.9`|`172.5.0.10`|`172.5.0.11`|`255.255.255.252` `/30`|

#### Enrutamiento
##### Interfaces
* SW1

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Gi1/1/1`|`172.5.0.1`|`255.255.255.252` `/30`|
|`Gi1/1/2`|`172.5.0.10`|`255.255.255.252` `/30`|

* SW2

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Gi1/1/1`|`172.5.0.5`|`255.255.255.252` `/30`|
|`Gi1/1/2`|`172.5.0.2`|`255.255.255.252` `/30`|

* SW3

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|`Gi1/1/1`|`172.5.0.9`|`255.255.255.252` `/30`|
|`Gi1/1/2`|`172.5.0.6`|`255.255.255.252` `/30`|

#### BGP
* SW1
```sh
enable
conf t
ip routing
interface Gi1/1/1
no switchport
ip address 172.5.0.1 255.255.255.252
no shutdown
exit
interface Gi1/1/2
no switchport
ip address 172.5.0.10 255.255.255.252
no shutdown
exit
router bgp 100
bgp log-neighbor-changes
neighbor 172.5.0.2 remote-as 200
neighbor 172.5.0.9 remote-as 300
network 172.5.0.0 mask 255.255.255.252
network 172.5.0.8 mask 255.255.255.252
exit
exit
wr
```

```sh
enable
conf t
ip routing
router bgp 100
redistribute eigrp 10
exit
exit
wr
```

* SW2
```sh
enable
conf t
ip routing
interface Gi1/1/1
no switchport
ip address 172.5.0.5 255.255.255.252
no shutdown
exit
interface Gi1/1/2
no switchport
ip address 172.5.0.2 255.255.255.252
no shutdown
exit
router bgp 200
bgp log-neighbor-changes
neighbor 172.5.0.1 remote-as 100
neighbor 172.5.0.6 remote-as 300
network 172.5.0.0 mask 255.255.255.252
network 172.5.0.4 mask 255.255.255.252
exit
exit
wr
```

```sh
enable
conf t
ip routing
router bgp 200
redistribute eigrp 20
exit
exit
wr
```

* SW3
```sh
enable
conf t
ip routing
interface Gi1/1/1
no switchport
ip address 172.5.0.9 255.255.255.252
no shutdown
exit
interface Gi1/1/2
no switchport
ip address 172.5.0.6 255.255.255.252
no shutdown
exit
router bgp 300
bgp log-neighbor-changes
neighbor 172.5.0.10 remote-as 100
neighbor 172.5.0.5 remote-as 200
network 172.5.0.8 mask 255.255.255.252
network 172.5.0.4 mask 255.255.255.252
exit
exit
wr
```

```sh
enable
conf t
ip routing
router bgp 300
redistribute ospf 30
exit
exit
wr
```