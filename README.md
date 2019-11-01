enable
configure terminal
hostname SW-01
enable secret senha20
username ruthbraga privilege 15 secret bolo
ip domain-name rede1.local
crypto key generate rsa general-keys modulus 1024
line vty 0 15
login local
transport input ssh
exec-timeout 5
exit
line console 0
password senha20
login
exit
service password-encryption
interface fastEthernet 0/1
switchport mode access
switchport access vlan 10
description PC 01
interface fastEthernet 0/2
switchport mode access
switchport access vlan 20
description PC 02
interface gigabitEthernet 0/1
switchport mode trunk
switchport trunk native vlan 99
switchport trunk allowed vlan 10,20,99,100
interface vlan 100
ip address 192.168.254.254 255.255.255.0
description INTERFACE DE GERENCIAMENTO
no shutdown
exit
ip default-gateway 192.168.254.1
do wr




enable
configure terminal
hostname RT-01
enable secret senha20
username ruthbraga privilege 15 secret bolo
ip domain-name rede1.local
crypto key generate rsa general-keys modulus 1024
security passwords min-length 8
login block-for 240 attempts 7 within 10
line vty 0 15
login local
transport input ssh
exec-timeout 5
exit
line console 0
password senha20
login
exit
service password-encryption
interface gigabitEthernet 0/1
no shutdown
interface gigabitEthernet 0/1.10
encapsulation dot1q 10
ip address 192.168.10.1 255.255.255.0
description VLAN 10
interface gigabitEthernet 0/1.20
encapsulation dot1q 20
ip address 192.168.20.1 255.255.255.0
description VLAN 20
interface gigabitEthernet 0/1.100
encapsulation dot1q 100
ip address 192.168.254.1 255.255.255.0
description VLAN 100
no shutdown

ip address 200.18.189.10 255.255.255.252
description CONEXÃO COM O RT-31
no shutdown
exit

enable
configure terminal
interface serial 0/0/0
ip address 200.200.100.1 255.255.255.252
no shutdown
do wr
ip route 192.168.30.0 255.255.255.0 200.200.100.2
ip route 192.168.40.0 255.255.255.0 200.200.100.2
ip route 192.168.253.0 255.255.255.0 200.200.100.2
