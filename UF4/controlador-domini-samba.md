# Samba 4 com a controlador de domini (DC)

## Introducció

Un dels rols més importants que pot fer un servidor **Samba** és actuar com a **controlador primari de domini** de forma similar al Active Directory de Windows.

En aquesta tema, veurem la configuració d’un servidor **Samba** com a controlador primari de domini en un **domini heterogeni**. 

És a dir, un domini on s’autenticaran i compartiran recursos màquines Windows i GNU/Linux.

### Samba 4

**Active Directory** és la característica més important alhora de decantar-se per **Windows Server** com a Sistema Operatiu en Xarxa. 

* El conjunt de serveis i utilitats que ofereix per la gestió dels usuaris i equips permet ser molt productiva especialment en clients Windows. 

Entre les principals millores de la **versió 4 de Samba** cal destacar el suport a **Microsoft Active Directory** que permet la implementació d’un Controlador de Domini basat en Active Directory.

Aquest fet suposa un millora molt atractiva ja que permet a moltes organitzacions **estalviar diners** en la compra de llicències Microsoft Windows Server i utilitzar Samba com a controlador de domini.

### Conceptes previs

Abans de començar cal saber que el servei d'**Active Directory (AD)** necessita d'altres serveis per funcionar correctament. 
  * Quan instal·lem un controlador de domini en un Windows Server, aquests serveis ja estan instal·lats o s'instal·len de forma automàtica, però en Linux s'ha de fer manualment.

Primer de tot, el programa que ens proporcionarà el servei d'AD per Linux és el **Samba**, però ha de ser com a mínim la **versió 4**.

I els serveis que necessita Samba per fer de servidor d'AD són els següents:

* **Servei DNS**: permet obtenir informació sobre els objectes del domini a partir del seu nom dins del domini (per exemple, l'adreça IP d'una màquina a partir del seu nom). En un cas senzill com el nostre, el mateix Samba farà de servidor DNS.

* **Servei Kerberos**: és un protocol d'autenticació entre ordinadors d'una xarxa perquè tant el client com el servidor puguin comprovar de forma fiable la identitat de l'altre.

* **Servei NTP**: serveix per sincronitzar els rellotges de les màquines del domini amb precisió. Kerberos, per defecte, no accepta errors de més de 5 minuts entre el servidor i el client que està validant.

### Resum de passos a seguir

1. Instal·lar el servei Samba.
2. Crear el domini Samba.
3. Instal·lar Kerberos.
4. Instal·lar el servei NTP.

## Instal·lació de Samba 4

**Samba 4** s'instal·la amb la comanda:

  `sudo apt-get install samba`
  
Un cop instal·lat, podem comprovar que tenim instal·lada la versió 4 executant la comanda:
   
```bash+theme:dark
root@server# samba -V
Version 4.3.11-Ubuntu
```

A continuació, fem un còpia de l'arxiu de configuració de Samba `/etc/samba/smb.conf` per conservar-lo ja que el procés de creació del domini crearà un arxiu nou.

  `sudo mv /etc/samba/smb.conf  /etc/samba/smb.conf.old`

## Creació d'un domini amb Samba

Un cop tenim instal·lat Samba, podem **promoure l'equip com a controlador de domini** Samba que actua com un substitut complet d'un servidor de domini de _Active Directory_.

**Crearem el domini** utilitzant la comanda.

  `sudo samba-tool domain provision --use-rfc2307 --interactive`
  
Les dades que cal introduir són les següents (es pot confirmar l'opció per defecte amb la tecla Intro):

* **Realm** (Nom del domini): **_SAMBAXXX_.LOCAL** (tot en majúscules) (XXX són les teves inicials)
* **Domain** (Nom _NetBIOS_ del domini): _**SAMBAXXX**_
* **Server Role** (Funció de Samba): **dc** (controlador de domini)
* **DNS backend** (Servidor DNS): **SAMBA_INTERNAL** (els sevidor DNS serà el propi Samba). 
* **DNS forwarder IP address** (Reenviador de DNS): **8.8.8.8** (servidor DNS al que es preguntarà quan no es pugui resoldre un nom, posem el de Google, el del centre o un altre servidor extern). 
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
dns-search sambaxxx.local
```

La segona línia `dns-search sambaxxx.local` serveix per facilitar les cerques dins del domini. 
* Per exemple, en lloc d'haver d'escriure la comanda  `nslookup server.sambaxxx.local` per obtenir l'adreça del servidor, n'hi haurà prou posant `nslookup server`.

Per actualitzar tots els serveis que s'han configurat, el més fàcil és reiniciar el servidor:

 `sudo reboot`

## Comprovació del servei Samba com a controlador de domini

### Comprovació que el servei Samba està funcionant

```bash+theme:dark
root@server:~# service smbd status
 * smbd.service - LSB: start Samba SMB/CIFS daemon (smbd)
 Loaded: loaded
 Active: active (exited)
 ...
```

Si Samba no està funcionant, es pot mirar l'arxiu de registre de Samba `/var/log/samba/log.samba` per saber el motiu.

### Comprovació que Samba resol correctament els DNS necessaris

Perquè Samba funcioni correctament és necessari que els servidor DNS associat també funcioni.

Per tant, comprovem que el servei DNS funciona correctament comprovant si el servei ldap i el servidor es resolen a través del servei de noms DNS.

```bash+theme:dark
root@server:~# host -t SRV _ldap._tcp.sambaxxx.local.
_ldap._tcp.sambaxxx.local has SRV record 0 100 389 server.sambaxxx.local.

root@server:~# host -t A server.sambaxxx.local.
server.sambaxxx.local has address 172.21.0.10
```

### Comprovació del servidor de fitxers

Per llistar tots els recursos compartits del controlador de domini (DC) executa:

```bash+theme:dark
root@server:~# smbclient -L localhost -U%
Domain=[ELTEUNOM] OS=[windows 6.1] Server=[Samba 4.3.11-Ubuntu]

    Sharename       Type      Comment
    ---------       ----      -------
    netlogon        Disk     
    sysvol          Disk     
    IPC$            IPC       IPC Service (Samba 4.3.11-Ubuntu)
Domain=[SAMBAXXX] OS=[windows 6.1] Server=[Samba 4.3.11-Ubuntu]

    Server               Comment
    ---------            -------

    Workgroup            Master
    ---------            -------
```

Us hauria de sortir dos recursos de Windows (netlogon, sysvol) que s'han compartit.

**Alerta**: Si al fer `smbclient -L localhost -U%` et surt un error que diu: 

`session setup failed: NT_STATUS_OBJECT_NAME_NOT_FOUND`

És necessari que instal·lis el paquet `winbind`

`sudo apt-get install winbind` 


## Instal·lació del client de Kerberos

> **Kerberos** és un dels protocols d'autenticació entre ordinadors d'una xarxa perquè tant el client com el servidor puguin comprovar de forma fiable la identitat de l'altre. 
> És un dels protocols utilitzat pel Active Directory de Windows.

Instal·larem els **client kerberos** al sevidor per poder comprovar si funciona correctament aquest servei crític pel Active Directory.
 
  `sudo apt-get install krb5-user`

En el procés d'instal·lació ens demana el nom del Real, on cal introduir el que hem utilitzat per el nostre domini **_ELTEUNOM.LOCAL_** . **Molt important en MAJÚSCULES!!**

![](/assets/kerberos1.png)

Finalment, fem la comprovació del servei kerberos.

  `kinit administrator@SAMBAXXX.LOCAL`
  
> **Recorda** que l'usuari administrador de Samba es diu _**administrator**_ i vam assignar-li una contrasenya durant la creació del domini.

![](/assets/kerberos2.png)

Si tot va bé, `Kinit` ens respon amb la data i hora que caducarà la contrasenya que acaben d'introduir.

També podem utilitzar la comanda `klist` per consultar les autenticacions que hi ha guardades actualment a la caché de Kerberos.

Si et cal reconfigurar els kerberos, utilitza la comanda.

`dpkg-reconfigure krb5-config`

## Instal·lació del servei NTP (Network Time Protocol)

> **El servei NTP** serveix per sincronitzar el rellotge intern del sistema amb algun servidor horari disponible a Internet.

En el nostre cas, l'utilitzarem per sincronitzar els rellotges de les màquines del domini amb precisió ja que el funcionament de **_Kerberos_**, per defecte, no accepta errors de més de 5 minuts entre el servidor i el client que està validant.

Així doncs, cal instal·lar el paquet **_ntp_**.

```bash
sudo apt-get install ntp
sudo service ntp stop
sudo ntpdate ntp.ubunbu.com
sudo service ntp start
```

> **ATENCIÓ**: un cop units els clients al domini, si alguna vegada dóna error de validació d'usuaris (fins i tot amb l'administrador), és possible que sigui degut a què la data i/o l'hora siguin diferents en el client i en el servidor. Un dels motius de què passi això és que s'hagi configurat incorrectament la zona horària d'alguna de les màquines. Si el problema es troba en el servidor Linux, es pot corregir amb la comanda `sudo dpkg-reconfigure tzdata`.

## Unir client Windows al domini Samba

Es fa de la mateixa forma que per unir-lo a un domini Windows:

1. Si el client està unit a un domini, primer cal desconnectar-lo del domini i reiniciar.

2. A la configuració de xarxa, canviar els servidors DNS posant com a **DNS principal** la IP del servidor de domini.

  ![](/assets/samba4_unir_client1.jpg)

3. Connectar-lo al nou domini: _**Panel de control > Sistema > Cambiar configuración > Dominio**_

  Caldrà posar el nom del domini (_SAMBAXXX_ o _sambaxxx.local_) i quan demani un usuari, s'ha de posar **_Administrator_**, que és l'usuari administrador del domini fet amb Samba.

  ![](/assets/samba4_unir_client2.jpg)
  

## Documentació i recursos

* [Samba Wiki: Setting up Samba as an Active Directory Domain Controller](https://wiki.samba.org/index.php/Setting_up_Samba_as_an_Active_Directory_Domain_Controller)

* [Somebooks: Crear un controlador de dominio de Active Directory con Samba 4](http://somebooks.es/capitulo-12-integracion-de-redes-mixtas-con-windows-y-linux/7/)