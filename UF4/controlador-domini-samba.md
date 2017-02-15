# Samba 4 com a controlador de domini (DC)

## Introducció

Un dels rols més importants que pot fer un servidor **Samba** és actuar com a **controlador primari de domini** de forma similar al Active Directory de Windows.

En aquesta tema, veurem la configuració d’un servidor **Samba** com a controlador primari de domini en un **domini heterogeni**. 

És a dir, un domini on s’autenticaran i compartiran recursos màquines Windows i GNU/Linux.

## Samba 4

**Active Directory** és la característica més important alhora de decantar-se per **Windows Server** com a Sistema Operatiu en Xarxa. 
* El conjunt de serveis i utilitats que ofereix per la gestió dels usuaris i equips permet ser molt productiva especialment en clients Windows. 

Entre les principals millores de la **versió 4 de Samba** podem esmentar el suport a **Microsoft Active Directory** que permet la implementació d’un Controlador de Domini basat en Active Directory.
* Podent actuar tant com a client com a servidor de dominis Active Directory .

Aquest fet suposa un millora molt atractiva ja que permet a moltes organitzacions **estalviar diners** en la compra de llicències Microsoft Windows Server.

## Instal·lació de Samba 4

**Samba 4** s'instal·la amb la comanda:

  `sudo apt-get install samba`
  
Un cop instal·lat, podem comprovar que tenim instal·lada la versió 4 executant la comanda:
   
```bash
root@server# samba -V
Version 4.3.8-Ubuntu
```

A continuació, fem un còpia de l'arxiu de configuració de Samba `/etc/samba/smb.conf` per conservar-lo ja que el procés de creació del domini crearà un arxiu nou.

  `sudo mv /etc/samba/smb.conf  /etc/samba/smb.conf.bak`

## Crear un domini amb Samba

Un cop tenim instal·lat Samba, podem **crear el domini** utilitzant la comanda.

  `sudo samba-tool domain provision --use-rfc2307 --interactive`
  
Les dades que cal introduir són les següents (excepte la contrasenya, si s'han fet les configuracions anteriors correctament, només caldrà confirmar l'opció per defecte amb la tecla Intro):
* **Realm** (Nom del domini): **_ELTEUNOM_.LOCAL** (tot en majúscules)
* **Domain** (Nom NetBIOS del domini): _**ELTEUNOM**_
* **Server Role** (Funció de Samba): **dc** (controlador de domini)
* **DNS backend** (Servidor DNS): **SAMBA_INTERNAL** (per fer que Samba gestioni el servei DNS). 
* **DNS forwarder IP address** (Reenviador de DNS): **8.8.8.8** (servidor DNS de Google, del centre o d'un altre servidor extern). 
* **Administrator password** (Contrasenya per l'usuari _Administrator_): **\*\*\*\*\*\*** (ha de complir els criteris de complexitat de Windows)

![](/assets/saba-domain.png)
  
Si el procés s'ha realitzat **correctament**, ens apareixerà un missatge domant informació del domini creat.

![](/assets/saba-domain2.png)

Si es produeix un algun **error **en la creació del domini, cal esborrar l'arxiu de configuració de Samba.

 `sudo rm /etc/samba/smb.conf`
 
I tornar a crear el domini amb la comanda anterior.

`sudo samba-tool domain provision --use-rfc2307 --interactive --use-ntvfs`

Finalment, i **molt important**, cal fer que el servidor s'apunti a sí mateix com a **servidor DNS** (recordeu que un controlador de domini de Active Directory utilitza el servei DNS).

Així doncs, canviem la configuració de la xarxa editant l'arxiu `/etc/network/interfaces` per indicar com a primer servidor DNS el propi equip.

```bash
# The primary network interface
auto enp0s3
iface enp0s3 inet static
address x.x.x.x
netmask x.x.x.x
gateway x.x.x.x

dns-nameservers 127.0.0.1
dns-search elteunom.local
```

La segona línia `dns-search elteunom.local` serveix per facilitar les cerques dins del domini. 
* Per exemple, en lloc d'haver d'escriure la comanda  `nslookup server.elteunom.local` per obtenir l'adreça del servidor, n'hi haurà prou posant `nslookup server`.

Per actualitzar tots els serveis que s'han configurat, el més fàcil és reiniciar el servidor:

 `sudo reboot`

## Comprovació del servei Samba com a controlador de domini

### Comprovació que el servei Samba està funcionant

```bash
root@server:~# service samba status
 * samba is running
```

Si Samba no està funcionant, es pot mirar l'arxiu de registre de Samba `/var/log/samba/log.samba` per saber el motiu.

### Comprovació que Samba resol correctament els DNS necessaris

Comprovem que el servei DNS funciona correctament i mirem si el servei ldap i el servidor es resolen a través del serveis de noms DNS.

```bash
root@server:~# host -t SRV _ldap._tcp.elteunom.local.
_ldap._tcp.elteunom.local has SRV record 0 100 389 server.elteunom.local.

root@server:~# host -t A server.elteunom.local.
server.elteunom.local has address 172.21.0.10
```


## Instal·lació del client de Kerberos

> **Kerberos** és un dels protocols d'autenticació entre ordinadors d'una xarxa perquè tant el client com el servidor puguin comprovar de forma fiable la identitat de l'altre. 
> És un dels protocols utilitzat pel Active Directory de Windows.

Instal·larem els **client kerberos** al sevidor per poder comprovar si funciona correctament aquest servei crític pel Active Directory.
 
  `sudo apt-get install krb5-user`

En el procés d'instal·lació ens demana el nom del Real, on cal introduir el que hem utilitzat per el nostre domini **_ELTEUNOM.LOCAL_** . **Molt important en MAJÚSCULES!!**

![](/assets/kerberos1.png)

Finalment, fem la comprovació del servei.

  `kinit administrator@ELTEUNOM.LOCAL`
  
> **Recorda** que l'usuari administrador de Samba es diu _**administrator**_.

![](/assets/kerberos2.png)

Si et cal reconfigurar els kerberos, utilitza la comanda.

`dpkg-reconfigure krb5-config`

## Instal·lació del servei NTP (Network Time Protocol)

> **El servei NTP** serveix per sincronitzar els rellotges de les màquines del domini amb precisió. 

El funcionament de Kerberos, per defecte, no accepta errors de més de 5 minuts entre el servidor i el client que està validant.

`apt-get install ntp`


## Unir client Windows al domini Samba

Es fa de la mateixa forma que per unir-lo a un domini Windows:

1. Si el client està unit a un domini, primer cal desconnectar-lo del domini i reiniciar.

2. A la configuració de xarxa, canviar els servidors DNS posant com a **DNS principal** la IP del servidor de domini.

  ![](/assets/samba4_unir_client1.jpg)

3. Connectar-lo al nou domini: _**Panel de control > Sistema > Cambiar configuración > Dominio**_

  Caldrà posar el nom del domini (_ELTEUNOM_ o _elteunom.local_) i quan demani un usuari, s'ha de posar **_Administrator_**, que és l'usuari administrador del domini fet amb Samba.

  ![](/assets/samba4_unir_client2.jpg)
  
## Instal·lació de les eines per administrar el domini (RSAT)

Per administrar el domini Samba, utilitzarem un conjunt d’eines d’administració gratuïtes que ofereix Microsoft anomenades **_RSAT_** (_Remote Server Administration Tool_).

Aquestes eines s'instal·len en un **client Windows** i ens permetran gestionar el domini de forma idèntica a un domini amb Windows Server.

**_RSAT_** està disponible per diferents versions de Windows:

* Windows 10: https://www.microsoft.com/en-us/download/details.aspx?id=45520
* Windows 8.1: http://www.microsoft.com/en-us/download/details.aspx?id=39296
* Windows 8: http://www.microsoft.com/en-us/download/details.aspx?id=28972
* Windows 7: http://www.microsoft.com/en-us/download/details.aspx?id=7887

Un cop instal·lades, activarem a **_Características de Windows_** les eines d’administració necessàries (Administració Bàsica de l’Active Directory)



Un cop activades les eines, obrim **_Administrador del servidor > Herramientas administrativas > Usuarios y equipos de Active Directory_** i podrem **gestionar el domini** tal i com realitzaven amb Windows Server.

> Per poder administrar el domini (afegir usuaris, grups...) cal iniciar sessió amb el **compte** d'administrador de Samba (**_Administrator_**).

## Documentació i recursos

* [Samba Wiki](https://wiki.samba.org/index.php/Setting_up_Samba_as_an_Active_Directory_Domain_Controller)

* [Somebooks](http://somebooks.es/capitulo-12-integracion-de-redes-mixtas-con-windows-y-linux/7/)