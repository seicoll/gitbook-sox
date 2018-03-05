# Compartir arxius i carpetes amb SAMBA

## Introducció

En temes anteriors van compartir carpetes utilitzant el protocol **NFS**.

Amb **NFS**, no hi ha cap procés d’acreditació d’usuaris per accedir al recursos compartits.

* L’administrador ha de decidir amb cautela a quins ordinadors exporta un determinat directori.

La **manca d’autenticació d’usuaris** és un dels majors inconvenients del protocol **NFS**.

* Només podem **restringir els permisos dels usuaris** utilitzant mecanisme habitual de permisos en sistema de fitxers Linux.

Per aquesta raó cada vegada s’utilitzen més altres sistemes de compartició de fitxers com, per exemple, el **Samba**.

## Què és Samba?

> El **Samba** és un paquet de programari per **Linux** que permet compartir recursos \(carpetes i impressores\) utilitzant el protocol de comunicació **SMB/CIFS** que és el protocol  utilitzat per sistemes operatius **Windows** per compartir carpetes i impressores.

Samba té com a **objectiu** oferir una alternativa **lliure** perquè els sistemes "_no Microsoft_" puguin intercanviar arxius i impressores amb sistemes Microsoft.

* Això fa possible que es pugui accedir a **recursos compartits amb Linux** des de clients **Windows**.

* I també es podrà accedir a aquests recursos compatits des de Linux si es té instal·lat el client **smbclient**.

> Gràcies al **Samba**, en una xarxa hi pot haver equips amb Windows i equips amb Linux que intercanviïn informació en carpetes compartides i comparteixin impressores.

El nom **_Samba_** prové d'afegir dues vocals al nom del protocol estàndard usat pel sistema de xarxa de Microsoft Windows, **_SMB_** (no que estava registrat). 

## Instal·lació i configuració de Samba

### Instal·lació del servidor Samba

El paquet de programari **Samba** es compon de moltes aplicacions i molts paquets amb diverses finalitats.

Els **paquets** més utilitzats són els següents:

* **samba**: servidor d'arxius i impressores de xarxa local per a Unix/GNU/Linux.
* **smbclient**: client simple de xarxa local per a Unix/GNU/Linux.
* **samba-common**: arxius comuns del Samba que utilitzen els clients i els servidors.
* **samba-doc**: documentació del Samba.
* **cifs-utils**: ordres per muntar i desmuntar unitats de xarxa Samba.

Per **instal·lar** el servei Samba a l'Ubuntu.

```
sudo apt install samba cifs-utils
```

### Configuració del servidor Samba

La configuració del servidor **Samba** es fa, principalment, a partir del **fitxer de configuració** `/etc/samba/smb.conf`.

```
[global]
    workgroup = WORKGROUP
    server role = standalone server
...
[homes]
...
[printers]
    comment = All Printers
    path = /var/spool/samba
```

Editant aquest fitxer, es poden configurar més de tres-cents paràmetres.

El fitxer està dividit en **tres seccions** principals \(_**global, homes i printers**_\) que estableixen el valor d’uns quants paràmetres i determinen quines són les carpetes i les impressores compartides.

* **\[global\]**. Defineix els** paràmetres generals** del servidor Samba.
* **\[homes\]**. Ens permet **compartir les carpetes home** de cada usuari del servidor SAMBA. S’utilitza per crear **perfils mòbils** per tal que cada usuari pugui accedir a la seva carpeta home en qualsevol equip de la xarxa.
* **\[printers\]**. Ens permet compartir **impressores**.

### Recomanacions durant la configuració del Samba

És **important** crear una **còpia de seguretat** de l’arxiu `/etc/samba/smb.conf` abans de fer cap canvi per poder tornar a l’estat anterior en cas que fem una modificació incorrecta que impedeixi que el servei arrenqui.

`sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.bak`

Per **comprovar** que el nostre arxiu `/etc/samba/smb.conf` és **correcte**, és recomenable utilitzar l’ordre `testparm` per localitzar-hi errors.

<!--
### Nivells de seguretat

**Samba** es pot configurar en diversos nivells de seguretat.

* _**security=share**_: Permet que els clients es connectin als recursos compartits sense proporcionar cap nom d'usuari ni contrasenya.
  
* _**security=user**_: És l'opció per defecte i és la més simple. Es requereix un usuari i contrasenya per accedir a un recurs compartit.

* _**security=domain**_: el servidor Samba actua com un controlador de domini.

-->

## Configurar Samba com a servidor d'arxius

Una de les formes de compartir axius en xarxa amb equips **Ubuntu i Windows** és configurar **Samba com a servidor d'arxius**.

El servidor es configurarà per **compartir arxius amb qualsevol client de la xarxa sense sol·licitar cap contrasenya**.

En la secció **\[global\]** del fitxer de configuració de samba `/etc/samba/smb.conf` hi ha un paràmetre anomenat **workgroup **on hi posarem el nom de la nostra xarxa.

<!--
I definirem el paràmetre **security = share** per què no demani usuari i contrasenya per entrar a la carpeta compartida.
-->

```
workgroup = BOSCCOMA
```

## Compartir un nou recurs amb Samba

Per compartir un recurs \(arxiu o carpeta\), hem d'editar el fitxer `/etc/samba/smb.conf` i crear un **nova secció amb un nom entre claudàtors** que serà el **nom que el recurs compartit** tindrà a la xarxa. 

> Normalment aquesta nova secció es posa al final del fitxer.

**Exemple 1:** si volem compartir la carpeta `srv/samba/public` i anomenar al recurs _**public**_ crearem una secció _**\[public\]**_ on es configurarà amb els paràmetres específics.

1. Si volem que es permeti l'accés als **usuaris convidats** sense necessitat d'introduir una contrasenya d'accés, configurament el recurs compartit de la següent forma:

  ```
  # Carpeta comuna public
  [public] 
  path = /srv/samba/public     ; carpeta a compartir
  read only = no                ; es permet l'escriptura, també es pot posar writeable=yes
  browsable = yes               ; la carpeta serà visible quan accedir a \\IP_servidor
  guest ok = yes                ; s'admet l'usuari convidat de Linux per accedir al recurs
  guest only = yes              ; tots els accessos al recurs s'accepten en mode convidat
  ```
  
  Els principals **paràmetres** que s'han de configurar per un recurs compartit són:

  * **Nom** del recurs compartit: No cal que sigui el mateix nom que té l'arxiu o carpeta que es vol compartir. 
  * **Path**: Ruta local on es troba l'arxiu o carpeta que es vol compartir.
  * **Mode de compartició**: si tindrà permís de lectura i/o escriptura \(_**read only**_ o _**writeable**_\).
    * Només es pot posar un d'aquests dos últims paràmetres: tots dos serveixen per indicar el mode de compartició però amb l'efecte contrari un de l'altre \(_**writeable = no**_ seria el mateix que _**read only = yes**_\).
  * **Visibilitat**: si serà visible de forma remota \(_**browsable**_\).
  * **Accessibilitat**: si serà accessible per tothom o només per alguns usuaris o grups.

2. Creem la carpeta al servidor i canviem els seus permisos.

  ```
  sudo mkdir -p /srv/samba/public
  sudo chown nobody:nogroup /srv/samba/public
  ```
 
3. I reiniciem Samba.

  `service smbd restart`
  
> **Recordeu**, com tots els serveis de Linux, sempre que fem un canvi en els arxius de configuració del Samba, cal **reiniciar el servei smbd**.

## Gestió d'usuaris Samba

> El **Samba** disposa de la seva **pròpia base de dades d’usuaris** Samba que podran accedir als recursos compartits.

Per tant, el **Samba** és un servei que **requereix l’administració dels usuaris** per poder-ne gestionar els permisos.

En funció de l’usuari que hi accedeixi, el **Samba** es comportarà d’una manera o d’una altra.

> Per poder accedir a recursos compartits amb Samba, s'han d'utilitzar els usuaris Samba, **no els de Linux**.

### Relació entre usuaris Linux i usuaris Samba

**Samba** té un arxiu que relaciona usuaris de Samba amb usuaris de Linux:

* Cada usuari Samba ha d'estar relacionat amb un usuari Linux, però no té perquè tenir el mateix nom
* Diversos usuaris Samba poden estar relacionats amb un mateix usuari Linux.

| **Usuari Samba** | **Usuari Linux** |  |
| --- | --- | --- |
| alumne | alumne | L'usuari Samba _**alumne**_ es transformarà en l'usuari Linux _**alumne**_ |
| professorESO | professor | L'usuri Samba i l'usuari Linux no tenen perquè tenir el mateix nom |
| professorCF | professor | L'usuari Linux _**professor**_ té més d'un usuari Samba relacionat |

> Per poder ser usuari del Samba, cal disposar d’un compte d'usuari Samba i d'un compte d’usuari a GNU/Linux que hi estigui relacionat.

Aquestes relacions es poden modificar editant l'arxiu `/etc/samba/smbusers`.

La **gestió d’usuaris Samba** \(crear, eliminar, canviar contrassenya, etc\) es fa amb la comanda.

`smbpasswd`

### Creació d’usuaris Samba

1. Haurem de **crear l’usuari** a l’Ubuntu amb l’ordre següent:

  `sudo adduser alumne`

2. **Habilitar l’usuari** al Samba, executant aquesta ordre:

  `sudo smbpasswd -a alumne`

  `-a` vol dir que Samba afegirà l'usuari a la llista d’usuaris Samba.

### Eliminació d’usuaris Samba

`sudo smbpasswd -x alumne`

> L’usuari desapareixerà immediatament de la base de dades d’usuaris Samba, però **continuarà essent un usuari de GNU/Linux**.

### Llistar usuaris Samba

* Mostrar la llista d'usuaris Samba:  

  `sudo pdbedit -L`

* Mostrar la llista d'usuaris Samba amb més detalls:  

  `sudo pdbedit -Lv`

### Altres opcions de gestió d'usuaris

L’ordre `smbpasswd` disposa d’altres opcions interessants:

  * **-d**: deshabilitar un usuari.

  * **-i**: habilitar un usuari.

  * **-n**: establir un usuari sense contrasenya.
  Necessita paràmetre null `passwords = yes` en secció [GLOBAL] de l’arxiu de configuració del Samba.

## Permisos Samba

> Un **permís** és una marca associada a cada recurs de xarxa \(fitxers, directoris, impressores, etc.\) que regula quins usuaris i de quina manera hi tenen accés.

La gestió de grups, usuaris i permisos és diferent en sistemes GNU/Linux i en sistemes Microsoft Windows.

* En els **sistemes GNU/Linux**, la gestió dels permisos que els usuaris i els grups tenen sobre els arxius es fa mitjançant un esquema senzill de tres tipus de permisos (lectura, escriptura i execució) aplicables a tres tipus d'usuaris (propietari, grup propietari i resta d'usuaris).

* En els **sistemes Windows**, la gestió dels permisos que els usuaris i els grups tenen sobre els arxius es fa mitjançant un esquema complex de llistes de control d'accés (access control lists, ACL) per a cada directori i arxiu.

El sistema **ACL** té l'avantatge de ser molt més flexible que el sistema GNU/Linux, ja que es poden establir més tipus de permisos, donar permisos només a uns quants usuaris i grups, denegar permisos, etc.

En la majoria de casos n'hi ha prou amb les prestacions del sistema GNU/Linux.

Per defecte, el **Samba** utilitza el sistema de permisos de GNU/Linux. Tot i que també pot implementar el sistema ACL i gestionar les llistes mitjançant l'ordre `smbcacls`.

> Per fer la gestió d’usuaris, grups i permisos, es recomana fer servir els **permisos GNU/Linux**, els quals permeten assignar permisos de lectura, escriptura i execució \(rwx\) a l’usuari propietari de l’arxiu, al grup propietari de l’arxiu i a la resta d’usuaris del sistema.

### Comparició d'arxius i carpetes amb Samba

Una forma senzilla de configurar els permisos desitjats és posar tots els permisos en els permisos locals, i en la configuració de Samba indicar els usuaris que tenen accés i amb quins permisos.

**Exemple:** Compartim el recurs _**apunts**_ i voleu que:

* Tot i que el recurs hem compartit el recurs amb permisos només de lectura i \(_**writeable=no**_\), volem donar permisos només d'escriptura al grup d'usuaris anomenat _**profes**_ i a l'usuari _**root**_.
* Restringir l’accés a l'usuari _**alumne1**_.

Creem la carpeta i assignem els permisos locals:

```bash+theme:dark
# ls -l /srv/samba/apunts
drwxrwx--- 2 root profes 4096 apunts
```

Compartim la carpeta configurant el fitxer `/etc/samba/smb.conf`.

* Si es vol definir un **grup** en el fitxer de configuració del Samba, `/etc/samba/smb.conf`, cal posar "**@**" davant del nom del grup.

```
# Carpeta comuna apunts
[apunts] 
path = /srv/samba/apunts      ; carpeta a compartir
browsable = yes               ; la carpeta serà visible quan accedir a \\IP_servidor
writeable = no                ; no es permet l'escriptura, també es pot posar read only=yes
guest ok = no                 ; no s'admet l'usuari convidat
invalid users = alumne1
read list = @alumnes
write list = @profes, root
```

* **valid users**: Llista d'usuaris que poden accedir al recurs. 
* **invalid users**: Llista d'usuaris que no poden accedir al recurs. 
* **read list**: Llista d'usuaris que només tindran permisos de lectura en el recurs. Si el paràmetre és _**read only = yes**_, per defecte tots els usuaris només tindran permís de lectura.
* **write list**: Llista d'usuaris que tindran permís de lectura i escriptura en el recurs. Ignora l'opció _**read only = yes**_. 

> **ATENCIÓ**: els usuaris i grups que es posen en aquests paràmetres, han de ser **usuaris i grups de Linux**, no de Samba.
>
> Si es configuren els paràmetres **valid users** i **write list**, els usuaris de **write list** també han d'estar a **valid users**.
>
> Quan s'accedix a un recurs compartit amb Samba, cal utilitzar l'identificador i la contrasenya configurats en la base de dades d'usuaris de Samba, no amb usuaris locals.


### Determinar els permisos efectius

Ens podem trobar que els **permisos GNU/Linux** es contradiguin amb els **permisos Samba**.

Per **exemple**, podem tenir un directori compartit anomenat **share** amb permisos GNU/Linux de lectura, escriptura i execució per a **tots els usuaris** del sistema.  
Però si en l’arxiu de configuració del Samba aquest recurs compartit té el paràmetre **read only = yes**, no s’hi podran efectuar canvis, ja que està compartit amb permís només de lectura.

Per **determinar els permisos que tindrà l'usuari**, Samba realitza les següents comprovacions:

1. **Comprova** si l'usuari es troba a la llista d'**usuaris Samba**.

2. **Comprova** si l'usuari té **permís per accedir al recurs compartit** i quin tipus de permís \(només lectura o lectura i escriptura\)

3. **Converteix l'usuari** Samba en l'usuari local relacionat.

4. **Determina els permisos triant els més restrictius** entre els permisos que té l'usuari Samba sobre el recurs compartit i els permisos que té l'usuari local sobre la carpeta local

> Quan els permisos GNU/Linux es contradiuen amb els permisos Samba, el permís efectiu és el **més restrictiu**.

Podem fer un símil amb l'accés a una vivenda. Els permisos de Samba serien la valla i els permisos locals la porta de casa.

![](/assets/samba-permisos.png)

## Accedir a recursos compartit Samba des de Windows

<!-- Si, hem configurat els servidor Samba en mode `security=share`, cal afegir el client **Windows** al **grup de treball**:

* Botó dret a l’icona de _**Equip &gt; propietats**_
* I afegim l’equip al grup de treball que hem creat en el server.

-->

### Accedir a carpetes compartides de forma gràfica

Es fa de la mateixa forma que per accedir a una carpeta compartida en un altre Windows:
[Com accedir a una carpeta compartida](https://seicoll.gitbooks.io/sox/content/UF3/uf3-compartir-arxius-windows.html#accedir-a-carpetes-compartides)

> Quan es creen arxius o carpetes des del client, en el servidor es crearan amb l'usuari Linux relacionat amb l'usuari Samba. 

### Accedir connectant una unitat de xarxa a través de comandes

Es fa de la mateixa forma que per connectar una carpeta compartida en un altre Windows:

[Com connectar una unitat de xarxa a una carpeta compartida](https://seicoll.gitbooks.io/sox/content/UF3/uf3-compartir-arxius-windows.html#connectar-una-unitat-de-xarxa-a-trav%C3%A9s-de-comandes)

## Accedir a recursos compartits Samba des de Linux

[Apunts accedir a recursos compartits amb Windows o Samba (mitjançant el protocol SMB/CIFS).](https://seicoll.gitbooks.io/sox/content/UF4/uf4-compartir-de-windows-a-linux.html)

## Documentació i recursos

* **Més informació: **[https://help.ubuntu.com/lts/serverguide/samba-fileprint-security.html](https://help.ubuntu.com/lts/serverguide/samba-fileprint-security.html)

* [Ite Educacion](http://www.ite.educacion.es/formacion/materiales/85/cd/linux/m4/instalacin_y_configuracin_de_samba.html)



