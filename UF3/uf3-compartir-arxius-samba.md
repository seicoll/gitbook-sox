# Compartir arxius i carpetes amb SAMBA

## Introducció

En el tema anterior van compartir carpetes utilitzant el protocol **NFS**.

Amb **NFS**, no hi ha cap procés d’acreditació d’usuaris per accedir al recursos compartits.

L’administrador ha de decidir amb cautela a quins ordinadors exporta un determinat directori.

La **manca d’autenticació d’usuaris** és un dels majors inconvenients del protocol **NFS**.

Només podem **restringir els permisos dels usuaris** utilitzant mecanisme habitual de permisos en sistema de fitxer Linux.

Per aquesta raó cada vegada s’utilitzen més altres sistemes de compartició de fitxers com, per exemple, el **Samba**.

## Què és Samba?

El **Samba** és un paquet de programari per **Linux** que permet compartir recursos (arxius, carptes i impressores) utilitzant el protocol de comunicació **SMB/CIFS** que és el protocol  utilitzat per sistemes operatius **Windows** per compartir carpetes i impressores. 

Això fa possible que es pugui accedir a recursos compartits amb **Linux** des de clients **Windows**.

També es podrà accedir a aquests recursos des de Linux si es té instal·lat el client **smbclient**.

> Gràcies al **Samba**, en una xarxa hi pot haver equips amb Windows i equips amb Linux que intercanviïn informació en carpetes compartides i comparteixin impressores.

## Instal·lació Samba

El paquet de programari **Samba** es compon de moltes aplicacions i molts paquets amb diverses finalitats.

Els paquets més utilitzats són els següents:
* **samba**: servidor d'arxius i impressores de xarxa local per a Unix/GNU/Linux.
* **smbclient**: client simple de xarxa local per a Unix/GNU/Linux.
* **samba-common**: arxius comuns del Samba que utilitzen els clients i els servidors.
* **swat**: eina d'administració del Samba via web.
* **samba-doc**: documentació del Samba.
* **cifs-utils**: ordres per muntar i desmuntar unitats de xarxa Samba.

Per instal·lar el servei i el client Samba a l'Ubuntu

`apt-get install samba smbclient cifs-utils`

## Configuració del servidor Samba

La configuració del servidor **Samba** es fa, principalment, a partir del **fitxer de configuració** `/etc/samba/smb.conf`.

```
[global]
    workgroup = WORKGROUP
    server string = %h server (Samba, Ubuntu)
    server role = standalone server
...
[homes]
...
[printers]
    comment = All Printers
    path = /var/spool/samba
```

Editant aquest fitxer, es poden configurar més de tres-cents paràmetres.

El fitxer està dividit en **tres seccions** principals (_**global, homes i printers**_) que estableixen el valor d’uns quants paràmetres i determinen quines són les carpetes i les impressores compartides.
* **[global]**. Defineix els** paràmetres generals** del servidor Samba.
* **[homes]**. Ens permet **compartir les carpetes home** de cada usuari del servidor SAMBA. S’utilitza per crear **perfils mòbils** per tal que cada usuari pugui accedir a la seva carpeta home en qualsevol equip de la xarxa.
* **[printers]**. Ens permet compartir **impressores**.

## Configurar Samba com a servidor d'arxius

Una de les formes de compartir axius en xarxa amb equips **Ubuntu i Windows** és configurar **Samba com a servidor d'arxius**. 

El servidor es configurarà per **compartir arxius amb qualsevol client de la xarxa sense sol·licitar cap contrasenya**. 

En la secció **[global]** del fitxer de configuració de samba hi ha un paràmetre anomenat **workgroup **on hi posarem el nom de la nostra xarxa.

I definirem el paràmetre **security = share** per què no demani usuari i contrassenya per entrar a la carpeta compartida.

```
workgroup = BOSCCOMA
...
security = user
```


