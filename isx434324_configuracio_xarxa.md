Tania Gabriela Bonilla Alvarenga        Isx434324              28 sept. 2016

## Configurar adreca amb la comanda ip, comprovar que es veuen.

a) ip address add 172.16.0.5/16 broadcast 255.255.255.255 dev enp5s0
b) ping 172.16.0.6

## Descobrir l'adreça mac d'un altre dispositiu de la nostra xarxa.

a) arp 172.16.0.6
b)
Address                  HWtype  HWaddress           Flags Mask            Iface
172.16.0.6               ether   40:8d:5c:e4:1d:e0   C                     enp5s0

## Canviar el nom d'una interfície de xarxa amb la comanda ip

ip link set enp5s0 down
ip link set name nova_interficie enp5s0
ip a s

## Arrancar servidor netperf
netserver

## Executem script amb la ip del servidor
./script.sh 
91.35 inbound
91.42 outbound

## Canviar la MTU de les interfícies de xarxa
ip link set nova_interficie mtu 9000
ifconfig
 
--executem script amb la ip del server un altre cop
338.93 inbound
305.33 outbound

--la velocitat es gairabe el doble o triple de la velocitat inicial
--perque cada mtu es mes gran, per tant la transferencia es mes rapida.

##Configuració estàtica d'adreces IP amb la comanda nmcli
nmcli connection add con-name "static_meu" ifname enp5s0 type ethernet ip4 172.10.0.5/16

--on static-meu es el nom de la conexio que estic fent, enp5s0 es el nom de la interfici
--i ethernet es el tipus de conexio

##Configuració de servidors de noms de domini
less /etc/resolv.conf

##Configuració estàtica d'adreces IP de manera permanent (amb nmcli)
nmcli connection up static_meu
ip a s

## Configuració estàtica d'adreces IP de manera permanent (arxiu)
vim /etc/udev/rules.d/70-persistent-net.rules

SUBSYSTEM=="net", ACTION=="add", DRIVERS=="?*", ATTR{address}=="48:fc:4j:c5:b4:a6", ATTR{type=="1", KERNEL=="e*", NAME="mi-nova-interface"

## Traduïr un nom de domini per la seva adreca IP
dig www.escoldadeltreball.org

## Trobar el nom de domini a partir d'una adreça IP
dig -x 85.192.81.129
