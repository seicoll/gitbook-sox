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

En la secció **[global]** del fitxer de configuració de samba `/etc/samba/smb.conf` hi ha un paràmetre anomenat **workgroup **on hi posarem el nom de la nostra xarxa.

I definirem el paràmetre **security = share** per què no demani usuari i contrassenya per entrar a la carpeta compartida.

```
workgroup = BOSCCOMA
...
security = share
```
### Recomanacions durant la configuració del Samba

És convenient crear una còpia de seguretat de l’arxiu `/etc/samba/smb.conf` abans de fer cap canvi per poder tornar a l’estat anterior en cas que fem una modificació incorrecta que impedeixi que el servei arrenqui. 

Per **comprovar** que el nostre arxiu `/etc/samba/smb.conf` és **correcte**, podem utilitzar l’ordre `testparm` per localitzar-hi errors.

### Compartir un nou recurs (arxiu o carpeta) amb Samba

Per compartir una carpeta, hem d’editar el fitxer `/etc/samba/smb.conf` i crear un **nova secció amb un nom entre claudàtors** que serà els nom que el recurs compartit tindrà a la xarxa.

**Per exemple**, si volem compartir la carpeta `/home/samba/alumnes` i anomenar al recurs **_alumnes_**, crearem una secció **_[alumnes]_** on es configurarà amb els paràmetres específics.

```
# Carpeta comú alumnes
[alumnes] 
browsable = yes
read only = no
path = /home/samba/alumnes
guest ok = yes
guest account = nobody
guest only = yes
```

Creem la carpeta al servidor i canviem els seus permisos.

`sudo mkdir -p /home/samba/alumnes`

`sudo chown nobody:nogroup /home/samba/alumnes`

I reiniciem Samba.

`service smbd restart`

### Accedir recurs compartit SAMBA des de Windows

En un **Windows** hem d’afegir el nostre equip al **grup de treball**:
  * Botó dret a l’icona de **_“Equip” > propietats_**
  * I afegim l’equip al grup de treball que hem creat en el server.

Anem al explorador d’arxius i dintre de xarxes cerquem el nostre equip i la nostra carpeta compartida.

### Accedir a recursos compartits SAMBA des de Linux

En l'Ubuntu instal·lem el **client Samba**:

`apt-get install smbclient cifs-utils`

La comanda `smbclient` ens permet accedir a un recurs del servidor com si es tractés d’una mena d’accés FTP.

Per **exemple**, si volem accedir a la carpeta compartida 'alumnes' del 'servidor', executarem:

`smbclient //servidor/alumnes`

També permet **llistar els recursos compartits** d’una màquina remota:

`smbclient -L servidor`

#### Accedir de forma gràfica

L’Ubuntu ens permet accedir **gràficament **als recursos disponibles dels grups de treball del Samba amb el navegador Nautilus, per mitjà del menú **_Llocs > Xarxa_**.

#### Muntar carptes compartides

També hi ha la **possibilitat de muntar les unitats de xarxa** en carpetes del nostre sistema com si es tractés d'una carpeta local. 
  * És igual com en els recursos **NFS**.
  * La **diferència **entre **NFS** i **SMB **és que NFS no requereix que l’usuari que fa la connexió s’autentifiqui i amb SMB sí cal autentificació.
  * **Per exemple**, si volem accedir des de l’equip d’un professor a una carpeta compartida amb el nom de professors al servidor, executarem:
 
`mount –t cifs //servidor/professors /professors –o username=usuari,workgroup=MEUGRUP`

Si el servidor no requereix que l’usuari s’autentiqui (permet accés a convidats), els paràmetres username, password i workgroup es poden obviar. 

`mount –t cifs //servidor/professors /professors`

#### Connectar carpetes compartides de forma automàtica

Si volem que una carpeta compartida **es connecti sempre de forma automàtica** quan iniciem el nostre Linux, cal afegir a l'arxiu `/etc/fstab` una línia com:

Si el recurs compartit permet l’accés a convidats (guests):

`//servidor/professors  /professors  cifs  guest,uid=1000  0  0`

Si el recurs compartit està protegit per contrassenya:

`//servidor/professors /professors cifs  username=usuari,password=constrasenya,sec=ntlm  0  0`

![Més informació:](https://wiki.ubuntu.com/MountWindowsSharesPermanently)


![Ite Educacion](http://www.ite.educacion.es/formacion/materiales/85/cd/linux/m4/instalacin_y_configuracin_de_samba.html)

