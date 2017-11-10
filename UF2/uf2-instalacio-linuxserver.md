# Instal·lació Ubuntu Server

## Planificació de la instal·lació

### Comprovar els requeriments de maquinari

S'ha de comprovar a la web oficial, tant del sistema operatiu com de les aplicacions què s'han d'instal·lar, quins són els requeriments de maquinari.

### Preparar el programari a instal·lar i les dades a configurar

S'ha de tenir preparat tot el programari i les dades necessàries: CDs, controladors, claus d'activació...

### Crear la màquina virtual

S'ha de crear una màquina virtual amb les característiques recomanades per instal·lar **_Ubuntu Server 64 bits_**:

* El nom de la màquina pot ser **_SOX Ubuntu Server_**.
* Es recomana que l'espai del disc es reservi de forma dinàmica.
* Es pot posar més d'un processador.
* Connecta la MV a la [** xarxa NAT SOX**](http://moodlecf.sapalomera.cat/apunts/smx/sox/uf0/A012-VBoxPlus.html#config_nat_network).

Després de la instal·lació, la memòria RAM es pot reduir fins a 512 MB.

## Instal·lar el sistema operatiu

### Paràmetres bàsics de configuració

* Triar l'idioma i altres dades regionals (país, teclat...).
* **Nom de la  màquina**: **_usxxx_** (**_xxx_** són les teves inicials en minúscules).
* **Nom de l'usuari** (es pot posar nom i cognoms).
* **Nom del compte d'usuari** (una sola paraula, lletres minúscules o números...).
* **Contrasenya** (preferiblement que segueixi els criteris de seguretat).
* No cal encriptar la carpeta personal.
* Seleccionar la zona horària.

### Planificar el disc

Cal planificar la utilització del disc, decidir les particions necessàries i el sistema de fitxers a utilitzar.

* Primer s'ha de seleccionar el particionat manual, triar el disc i crear la taula de particions.
  * En l'espai lliure, crear una partició nova de 6 GB.
  * Crear-la com a partició primària, al principi del disc i amb el format ext4.
  * El punt de muntatge ha de ser l'arrel del sistema (/).
  * No cal afegir cap opció addicional de muntatge.

* Repetir els passos anteriors per crear una partició primària de 2 GB per la carpeta d'usuaris (/home).
* Finalment, crear una altra partició primària amb la resta de l'espai per a la swap (àrea d'intercanvi).

Abans de confirmar, comprovar les particions creades:

![](/assets/US-Instalacio-particions.png)

### Altres paràmetres

* No cal configurar un proxy.
* No cal activar les actualitzacions automàtiques.
* Instal·lar el servei **SSH** (seleccionar/deseleccionar serveis amb la tecla ESPAI).
* Instal·lar GRUB (el gestor d'arrencada) en el disc principal.

## Post-instal·lació

### Canviar el nom de l'equip

Si es vol canviar el nom d'una màquina Linux, cal fer-ho en els arxius `/etc/hostname` i `/etc/hosts` i reiniciar el sistema.

### Configurar la xarxa

Primer, amb la comanda `ifconfig -a` cal comprovar quina és la targeta de xarxa que s'ha de configurar.

Antigament s'utilitzaven els noms **_eth0_**, **_eth1_**... en funció de l'ordre en què es trobaven les interfícies.

Actualment s'utilitza el sistema [Predictable Network Interface Names](https://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames/) que assigna sempre el mateix nom a una interfície de xarxa.

En aquest sistema els noms depenen, entre altes coses, del tipus i d'on està instal·lada (si és Ethernet o Wireless, si està integrada a la placa base, en un port PCI, en  un port USB...).
* Interfícies **en**....: corresponen a targetes Ethernet (amb cable).
* Interfícies **wl**...: corresponen a targetes Wireless LAN (sense cable).
* Interfície **lo**: correspon a la interfície de **loopback**.

```sh
usuari@usxxx:~$ ifconfig -a
enp0s3    Link encap:Ethernet  direcciónHW 08:00:27:79:94:29
           Direc. inet:172.30.0.20  Difus.:172.30.255.255  Másc:255.255.0.0
          ...
wlp2s0    Link encap:Ethernet  direcciónHW 00:13:f7:40:1c:a6  
          Direc. inet:192.168.1.128  Difus.:192.168.1.255  Másc:255.255.255.0
          ...
lo        Link encap:Bucle local  
          Direc. inet:127.0.0.1  Másc:255.0.0.0
          ...
```

Un servidor ha de tenir una **adreça estàtica** ja que els clients l'han de conèixer per poder utilitzar els seus serveis.

L'adreça ha de pertànyer a la xarxa on està connectada la màquina.

En **_Ubuntu Server_**, la xarxa es configura editant l'arxiu `/etc/network/interfaces`.

* **Adreça IP**: `172.30.A.20` (**_A_** és el teu número d'alumne)
* **Màscara**: `255.255.0.0` (de 16 bits, com la de la xarxa)
* **Porta d'enllaç (GW)**: `172.30.0.1` (l'adreça del router virtual de la xarxa NAT)
* **Servidors DNS**: `172.30.0.1` i `8.8.8.8` (la mateixa porta d'enllaç de VirtualBox pot fer de servidor DNS).

> **ATENCIÓ**: en Ubuntu, per configurar l'adreça dels servidors DNS no s'ha d'editar l'arxiu `/etc/resolv.conf`

```
# Interfície de bucle local (127.0.0.1)
auto lo
iface lo inet loopback

# Interfície de xarxa Ethernet
auto enp0s3
iface enp0s3 inet static
address 172.30.A.20
netmask 255.255.0.0
gateway 172.30.0.1
dns-nameservers 172.20.0.1 8.8.8.8
```

**Reiniciar la targeta** per què agafi la nova configuració:

```
sudo ip addr flush enp0s3
sudo service networking restart
```


### Actualitzar el sistema

La comanda per actualitzar Linux és `apt-get upgrade`, però abans s'ha d'executar `apt-get update` per saber quins paquets cal actualitzar:

```
sudo apt-get update
sudo apt-get upgrade
```
En el cas d'**_Ubuntu Server_**, el nucli del sistema Linux no s'actualitza automàticament perquè cal reiniciar la màquina, i això és preferible que sigui l'administrador qui decideixi quan s'ha fer.

Quan sigui possible actualitzar el nucli i reiniciar el servidor, es pot utilitzar la comanda `apt-get dist-upgrade`:

```
sudo apt-get update
sudo apt-get dist-upgrade
sudo reboot
```



