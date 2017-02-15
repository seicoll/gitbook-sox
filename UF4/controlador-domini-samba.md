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
Version 4.3-Ubuntu
```

A continuació, fem un còpia de l'arxiu de configuració de Samba `/etc/samba/smb.conf` per conservar-lo ja que el procés de creació del domini crearà un arxiu nou.

  `sudo mv /etc/samba/smb.conf  /etc/samba/smb.conf.bak`

## Crear un domini amb Samba

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

`sudo samba-tool domain provision --use-rfc2307 --interactive`

Finalment, i **molt important**, cal fer que el servidor s'apunti a sí mateix com a **servidor DNS** (recordeu que un controlador de domini de Active Directory utilitza el servei DNS).

Així doncs, canviem la configuració de la xarxa editant l'arxiu `/etc/network/interfaces` per indicar els servidor DNS.

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

La segona línia `dns-search elteunom.local` serveix per facilitar les cerques dins del domini. * Per exemple, en comptes d'haver d'escriure la comanda  `nslookup server.elteunom.local` per obtenir l'adreça del servidor, n'hi haurà prou posant `nslookup server`.

Per actualitzar tots els serveis que s'han configurat, el més fàcil és reiniciar el servidor:

 `sudo reboot`

## Comprovació del servei Samba com a controlador de domini

