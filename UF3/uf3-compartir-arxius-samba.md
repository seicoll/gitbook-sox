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

Per instal·lar el servei Samba a l'Ubuntu.

`sudo apt-get install samba cifs-utils`

## Configuració del servidor Samba

La configuració del servidor **Samba** es fa, principalment, a partir del **fitxer de configuració** `/etc/samba/smb.conf`.

```bash
[global]
    workgroup = WORKGROUP
    security = user
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

> **Recordeu**, com tots els serveis de Linux, sempre que fem un canvi en els arxius de configuració del Samba, cal **reiniciar el servei smbd**.

`service smbd restart`


### Recomanacions durant la configuració del Samba

És **important** crear una **còpia de seguretat** de l’arxiu `/etc/samba/smb.conf` abans de fer cap canvi per poder tornar a l’estat anterior en cas que fem una modificació incorrecta que impedeixi que el servei arrenqui. 

`sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.bak`

Per **comprovar** que el nostre arxiu `/etc/samba/smb.conf` és **correcte**, és recomenable utilitzar l’ordre `testparm` per localitzar-hi errors.

## Nivells de seguretat

**Samba** es pot configurar en diversos nivells de seguretat.

* **_security=share_**: Permet que els clients es connectin als recursos compartits sense proporcionar cap nom d'usuari ni contrasenya.
 
* **_security=user_**: És l'opció per defecte i és la més simple. Es requereix un usuari i contrasenya per accedir a un recurs compartit.

* **_security=domain_**: el servidor Samba actua com un controlador de domini.

## Configurar Samba com a servidor d'arxius

Una de les formes de compartir axius en xarxa amb equips **Ubuntu i Windows** és configurar **Samba com a servidor d'arxius**. 

El servidor es configurarà per **compartir arxius amb qualsevol client de la xarxa sense sol·licitar cap contrasenya**. 

En la secció **[global]** del fitxer de configuració de samba `/etc/samba/smb.conf` hi ha un paràmetre anomenat **workgroup **on hi posarem el nom de la nostra xarxa.

I definirem el paràmetre **security = share** per què no demani usuari i contrasenya per entrar a la carpeta compartida.

```
workgroup = BOSCCOMA

```

## Compartir un nou recurs amb Samba

Per compartir un recurs (arxiu o carpeta), hem d’editar el fitxer `/etc/samba/smb.conf` i crear un **nova secció amb un nom entre claudàtors** que serà el **nom que el recurs compartit** tindrà a la xarxa. Normalment aquesta nova secció es posa al final del fitxer.

Per **exemple**, si volem compartir la carpeta `/home/samba/alumnes` i anomenar al recurs **_alumnes_**, crearem una secció **_[alumnes]_** on es configurarà amb els paràmetres específics.

Els principals **paràmetres** que s'han de configurar per un recurs compartit són:
* **Nom** del recurs compartit: No cal que sigui el mateix nom que té l'arxiu o carpeta que es vol compartir. 
* **Path**: Ruta local on es troba l'arxiu o carpeta que es vol compartir.
* **Mode de compartició**: si tindrà permís de lectura i/o escriptura (**_read only_** o **_writeable_**).
   * Només es pot posar un d'aquests dos últims paràmetres: tots dos serveixen per indicar el mode de compartició però amb l'efecte contrari un de l'altre (_**writable = no**_ seria el mateix que _**read only = yes**_).
* **Visibilitat**: si serà visible de forma remota (_**browsable**_).
* **Accessibilitat**: si serà accessible per tothom o només per alguns usuaris o grups.


En aquest **exemple** compartim el recurs _**alumnes**_ de manera que es permeti l'accés als usuaris convidats sense necessitat d'introduir una contrasenya d'accés. 

```
# Carpeta comuna alumnes
[alumnes] 
path = /home/samba/alumnes    ; carpeta a compartir
browsable = yes               ; la carpeta serà visible quan accedir a \\IP_servidor
read only = no                ; es permet l'escriptura
guest ok = yes                ; s'admet l'usuari convidat
guest account = nobody        ; els usuaris convidats utilitzaran el compte d'usuari nobody de Linux per accedir al recurs
guest only = yes              ; tots els accessos al recurs s'accepten en mode convidat
```

Creem la carpeta al servidor i canviem els seus permisos.

`sudo mkdir -p /home/samba/alumnes`

`sudo chown nobody:nogroup /home/samba/alumnes`

I reiniciem Samba.

`service smbd restart`

## Accedir a recursos compartit Samba des de Windows

Si, hem configurat els servidor Samba en mode `security=share`, cal afegir el client **Windows** al **grup de treball**:
  * Botó dret a l’icona de **_Equip > propietats_**
  * I afegim l’equip al grup de treball que hem creat en el server.

### Accedir a carpetes compartides de forma gràfica

Si volem accedir al recurs compartit a través de l'**interfície gràfica**, anem al explorador d’arxius i dintre de xarxes cerquem el nostre equip i la nostra carpeta compartida.

### Accedir a carpetes compartides amb comandes

Si volem accedir al recurs compartit a través de **comandes**:

`net use X: \\servidor\recurs`

## Accedir a recursos compartits Samba des de Linux

Per accedir a un recurs compartit amb Samba en l'Ubuntu cal instal·lar el **client Samba (paquet smbclient)**:

`apt-get install smbclient cifs-utils`

La comanda `smbclient` ens permet accedir a un recurs del servidor com si es tractés d’una mena d’accés FTP.

Per **exemple**, si volem accedir a la carpeta compartida 'alumnes' del 'servidor', executarem:

`smbclient //servidor/alumnes`

També permet **llistar els recursos compartits** d’una màquina remota:

`smbclient -L servidor`

### Accedir a carpetes compartides de forma gràfica

L’Ubuntu ens permet accedir **gràficament **als recursos disponibles dels grups de treball del Samba amb el navegador Nautilus, per mitjà del menú **_Llocs > Xarxa_**.

### Muntar carpetes compartides

També hi ha la **possibilitat de muntar les unitats de xarxa** en carpetes del nostre sistema com si es tractés d'una carpeta local. 
  * És igual com en els recursos **NFS**.
  * La **diferència **entre **NFS** i **SMB **és que NFS no requereix que l’usuari que fa la connexió s’autentifiqui i amb SMB sí cal autentificació.
  * **Per exemple**, si volem accedir des de l’equip d’un professor a una carpeta compartida amb el nom de professors al servidor, executarem:
 
`mount –t cifs //servidor/professors /professors –o username=usuari,password=pass`

Si el servidor no requereix que l’usuari s’autentiqui (permet accés a convidats), els paràmetres username, password i workgroup es poden obviar. 

`mount –t cifs //servidor/professors /professors`

### Muntar carpetes compartides de forma automàtica

Si volem que una carpeta compartida **es connecti sempre de forma automàtica** quan iniciem el nostre Linux, cal afegir a l'arxiu `/etc/fstab` una línia com:

Si el recurs compartit permet l’accés a convidats (guests):

`//servidor/professors  /professors  cifs  guest,uid=1000  0  0`

Si el recurs compartit està protegit per contrassenya:

`//servidor/professors /professors cifs  username=usuari,password=constrasenya,sec=ntlm  0  0`

Per muntar automàticament els recussos definits a `/etc/fstab` sense necessitat de reiniciar el sistema podeu executar.

`sudo mount -a`

Per comprovar si s'han muntat correctament les carpetes es pot utilitzar la comanda `mount`.

[Més informació:](https://wiki.ubuntu.com/MountWindowsSharesPermanently)

## Gestió d'usuaris Samba

El **Samba** és un servei que **requereix l’administració dels usuaris** per poder-ne gestionar els permisos.

El **Samba** disposa de la seva **pròpia base de dades d’usuaris** Samba que podran accedir als recursos compartits.
 
En funció de l’usuari que hi accedeixi, el Samba es comportarà d’una manera o d’una altra.

> Per poder accedir a recursos compartits amb Samba, s'han d'utilitzar els usuaris Samba, **no els de Linux**.

Com que els usuaris utilitzen altres recursos del servidor, com carpetes i impressores, cal que aquests usuaris també estiguin creats en el sistema GNU/Linux.

> Per poder ser usuari del Samba, cal disposar d’un compte d’usuari a GNU/Linux i d’un compte d’usuari al Samba

La **gestió d’usuaris Samba** (crear, eliminar, canviar contrassenya, etc) es fa amb la comanda.

`smbpasswd`

### Creació d’usuaris Samba

1. Haurem de crear l’usuari a l’Ubuntu amb l’ordre següent:

`sudo adduser alumne`

2. Habilitar l’usuari al Samba, executant aquesta ordre:

`sudo smbpasswd -a alumne`

`-a` vol dir que Samba afegirà l’usuari a la llista d’usuaris Samba

### Eliminació d’usuaris Samba

`sudo smbpasswd -x alumne`

> L’usuari desapareixerà immediatament de la base de dades d’usuaris Samba, però **continuarà essent un usuari de GNU/Linux**.

### Llistar usuaris Samba

Mostrar la llista d'usuaris Samba:
`sudo pdbedit -L`

Mostrar la llista d'usuaris Samba amb més detalls:
`sudo pdbedit -Lv`

### Altres opcions de gestió d'usuaris

L’ordre `smbpasswd` disposa d’altres opcions interessants:

-d: deshabilitar un usuari.

-i: habilitar un usuari.

-n: establir un usuari sense contrasenya.

(Necessita paràmetre null **passwords = yes** en secció GLOBAL de l’arxiu de configuració del Samba).

## Permisos Samba

Un **permís** és una marca associada a cada recurs de xarxa (fitxers, directoris, impressores, etc.) que regula quins usuaris i de quina manera hi tenen accés.

Per fer la gestió d’usuaris, grups i permisos, es recomana fer servir els **permisos GNU/Linux**, els quals permeten assignar permisos de lectura, escriptura i execució (rwx) a l’usuari propietari de l’arxiu, al grup propietari de l’arxiu i a la resta d’usuaris del sistema.

### Configurar propietaris i permisos locals, i usuaris i permisos Samba
Una forma senzilla de configurar els permisos desitjats és posar tots els permisos en els permisos locals, i en la configuració de Samba indicar els usuaris que tenen accés i amb quins permisos.

Per **exemple**, per compartir la carpeta alumnes i donar permisos de lectura, escriptura i execució a tots els usuaris del grup alumnes.

```
# ls -l /home/samba/
drwxrwx--- 2 root alumnes 4096 alumnes
```

Si es vol definir un **grup** en el fitxer de configuració del Samba, `/etc/samba/smb.conf`, cal posar "**@**" davant del nom del grup.

**Per exemple**, si heu definit una carpeta compartida del Samba anomenada **share** i desitgeu:
* Tot i que el recurs hem comparit el recurs amb permisos de lectura i escriptura (**_read only=no_**), volem donar permisos només de  lectura al grup d'usuaris anomenat **_alumnes_**. 
* Restringir l’accés a l’usuari **_alumne1_**.
* Permetre l'escriptura al grup anomenat **_professors_** i a l'usuari **_sergi_**.

```
# Carpeta comú alumnes
[share] 
path = /home/samba/alumnes
browsable = yes
read only = no
invalid users = alumne1
read list = @alumnes
write list = @professors, sergi
```

* **valid users**: Llista d'usuaris que poden accedir al recurs. 
* **invalid users**: Llista d'usuaris que no poden accedir al recurs. 
* **read list**: Llista d'usuaris que només tindran permisos de lectura en el recurs. Si el paràmetre és **_read only = yes_**, per defecte tots els usuaris només tindran permís de lectura.
* **write list**: Llista d'usuaris que tindran permís de lectura i escriptura en el recurs. Ignora l'opció _**read only = yes**_. 

> **ATENCIÓ**: els usuaris i grups que es posen en aquests paràmetres, han de ser **usuaris i grups de Linux**, no de Samba.

> Si es configuren els paràmetres **valid users** i **write list**, els usuaris de **write list** també han d'estar a **valid users**.

> Quan s'accedix a un recurs compartit amb Samba, cal utilitzar l'identificador i la contrasenya configurats en la base de dades d'usuaris de Samba, no amb usuaris locals.

### Determinar els permisos efectius

Ens podem trobar que els **permisos GNU/Linux** es contradiguin amb els **permisos Samba**.

Per **exemple**, podem tenir un directori compartit anomenat **share** amb permisos GNU/Linux de lectura, escriptura i execució per a **tots els usuaris** del sistema.

Però si en l’arxiu de configuració del Samba aquest recurs té el paràmetre **read only = yes**, no s’hi podran efectuar canvis, ja que està compartit amb permís només de lectura.

> Quan els permisos GNU/Linux es contradiuen amb els permisos Samba, el permís efectiu és el **més restrictiu**.

Per determinar els permisos que tindrà l'usuari, Samba realitza les següents comprovacions:

1. Comprova si l'usuari es troba a la llista d'usuaris Samba

2. Comprova si l'usuari té permís per accedir al recurs compartit i quin tipus de permís (només lectura o lectura i escriptura)

3. Converteix l'usuari Samba en l'usuari local relacionat.

4. Determina els permisos triant els **més restrictius** entre els permisos que té l'usuari Samba sobre el recurs compartit i els permisos que té l'usuari local sobre la carpeta local

## Documentació i recursos

* Més informació: https://help.ubuntu.com/lts/serverguide/samba-fileprint-security.html

* [Ite Educacion](http://www.ite.educacion.es/formacion/materiales/85/cd/linux/m4/instalacin_y_configuracin_de_samba.html)

