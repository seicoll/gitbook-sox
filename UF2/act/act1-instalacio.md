<!-- notoc -->

# Activitat 1. Instal·lació d’Ubuntu Server.

> imatge

## 1. Instal·lació

Crea una màquina virtual amb les característiques recomanades per instal·lar** Ubuntu Server 16.04**.

1.1 Configura la màquina virtual amb **xarxa NAT** anomenada **_SOX_**.

1.2 El nom de la màquina ha de ser **ubuntu-server**, i l’usuari principal administrador.

1.3 Instal·leu el sistema operatiu amb la següent estructura de particions.

| Punt de muntatge        | Tipus partició           | Mida  | Sistema de fitxers |
| ------------- |:-------------:| -----:|-------:|
| root partition (/)      | Primària | 10 Gb | ext4 |
| home partition (/home)      | Primària      |   1 Gb | ext4 |
| swap partition | Lògica      |    1 Gb | intercanvi |


1.4 Busca informació sobre què emmagatzemarà a cada partició? 

1.5 No instal·lis cap programari ni actualització.

## 2. Configurar la xarxa

Primer, amb la comanda `ifconfig -a` cal comprovar quina és la targeta de xarxa que s'ha de configurar.

Antigament s'utilitzaven els noms eth0, eth1... en funció de l'ordre en què es trobaven les interfícies.

Actualment s'utilitza el sistema _[Predictable Network Interface Names](https://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames/)_ que assigna sempre el mateix nom a una interfície de xarxa.

En aquest sistema els noms depenen, entre altes coses, del tipus i d'on està instal·lada (si és Ethernet o Wireless, si està integrada a la placa base, en un port PCI, en  un port USB...).
* Interfícies **en**....: corresponen a targetes Ethernet (amb cable).
* Interfícies **wl**...: corresponen a targetes Wireless LAN (sense cable).
* Interfície **lo**: correspon a la interfície de loopback.

En Ubuntu Server, la xarxa es configura editant l'arxiu /etc/network/interfaces.
Un servidor ha de tenir una adreça estàtica ja que els clients l'han de conèixer per poder utilitzar els seus serveis.

2.1 Configura l'adreça que ha de pertànyer a la xarxa on està connectada la màquina:

* **Adreça IP:** 172.21.A.20 (A és el teu número assignat)

* **Màscara:** 255.255.0.0 (de 16 bits, com la de la xarxa)

* **Porta d'enllaç (GW):** 172.21.0.1 (l'adreça del router virtual de la xarxa NAT)

* **Servidors DNS:** 8.8.8.8 i 8.8.4.4

```
# Interfície de bucle local (127.0.0.1)
auto lo
iface lo inet loopback

# Interfície de xarxa Ethernet
auto enp0s3
iface enp0s3 inet static
address 172.21.A.20
netmask 255.255.0.0
gateway 172.21.0.1
dns-nameservers 8.8.8.8 8.8.4.4
```

2.2 Reiniciar la targeta per què agafi la nova configuració:

```
sudo ip addr flush enp0s3
sudo service networking restart
```

2.3 Comprova la connectivitat a la xarxa fent ping a diferents adreces:

* Ping a la porta d'enllaç
* Ping als servidors DNS
* Ping a una adreça d'Internet, per exemple **google.com**

## Documentació i recursos

Configurar Red NAT VirtualBox: [http://fpg.x10host.com/VirtualBox/modo_red_nat.html#](http://fpg.x10host.com/VirtualBox/modo_red_nat.html#)

