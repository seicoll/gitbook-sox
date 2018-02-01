# Compartició d'arxius i carpetes en GNU/Linux

## Introducció

En els sistemes operatius lliures hi ha diversos protocols i aplicacions que ens permeten compartir recursos en xarxa, com el **protocol NFS** i el paquet de programari **Samba**.

### Protocol NFS \(Network File System\)

> El **protocol NFS \(**_**Network File System**_**\)** és un protocol que s’utilitza en l’àmbit de els xarxes local per compartir fitxers entre màquines de la mateixa xarxa.

El **protocol NFS** fa possible que diversos sistemes GNU/Linux connectats a una mateixa xarxa puguin accedir a fitxers en altres equips de la xarxa, com si es tractés de fitxers locals.

El **protocol NFS** pot ser utilitzat amb múltiples finalitats:

* Un **servidor NFS** pot **exportar més d’un directori** i atendre simultàniament diversos clients.
* Un **client NFS** pot **muntar directoris remots** exportats per diferents servidors i accedir-hi.

> Qualsevol sistema GNU/Linux pot ser alhora client i servidor NFS.

### Usos típics de l’NFS

En podem destacar les utilitats tradicionals següents:

* **Centralització dels directoris de connexió dels usuaris \(home directory\)**.
  * Si volem que els usuaris puguin treballar en qualsevol màquina del domini, cal posar els directoris de tots els usuaris en una mateixa màquina i fer que les altres muntin aquests directoris mitjançant NFS. 
  * Si aquest ús es combina amb l’autenticació d’usuaris en xarxa per mitjà de l’LDAP, es pot implementar quelcom similar a un domini del Windows.

* **Compartició de directoris d’ús comú.**

  * Permetre que diversos usuaris des de diferents màquines treballin amb els mateixos arxius.

* **Compartició per mitjà de la xarxa de dispositius d’emmagatzematge.**

  * Podem compartir dispositius com ara particions de discos durs, etc.    

### Incovenients NFS

> **Alerta!** Amb NFS **no hi ha cap procés d’acreditació d’usuaris** en l’NFS, de manera que l’administrador ha de decidir amb cautela a quins ordinadors exporta un determinat directori.

La manca d’autenticació d’usuaris és un dels majors inconvenients del protocol NFS i per aquesta raó cada vegada s’utilitzen més altres sistemes de compartició de fitxers com, per exemple, el **Samba**.

Veurem **Samba **en la propera Unitat Formativa.

### Funcionament de l’NFS

En el sistema **client**, el funcionament es basa en la capacitat de traduir els accessos de les aplicacions a un sistema d’arxius en peticions al servidor. 

* Aquesta funcionalitat del client està programada en el nucli de GNU/Linux, de manera que no necessita cap tipus d’instal·lació ni configuració.

Respecte al **servidor**, l’NFS s’implementa mitjançant dos serveis de xarxa, el **mountd** i l’**nfsd**.

* El servei **mountd** s’encarrega d’atendre les peticions remotes de muntatge, efectuades per l’ordre mount del client. 
* El servei **nfsd** s’encarrega d’atendre i resoldre les peticions d’accés del client als arxius que hi ha en el directori.

## Instal·lació i configuració del servidor NFS

### Instal·lació del servei NFS

El **paquet** que cal instal·lar en qualsevol ordinador que hagi de compartir carpetes amb el sistema NFS és **nfs-kernel-server**.

Per instal·lar-lo cal executar la comanda:

```
sudo apt update
sudo apt install nfs-kernel-server
```

### Configuració del servei NFS

> Una vegada actius els serveis NFS, el servidor ha d'indicar quins directoris vol que **s'exportin (compartir)**, a quines màquines s'han d'exportar i amb quines opcions s'ha de fer. 

El primer que cal fer és **crear les carpetes** que es volen compartir (si no són carpetes que ja existeixen).

Normalment, quan es comparteixen carpetes, es creen dins de `/srv`, i totes les d'un mateix servei s'agrupen dins d'una carpeta amb el nom del servei, en aquest cas `nfs`:

```
sudo mkdir -p /srv/nfs/compartit1
sudo mkdir -p /srv/nfs/compartit2
```

Després cal **configurar els propietaris i permisos locals** adequats en cada carpeta.

Finalment, per **exportar (compartir) les carpetes**, s'ha de definir al fitxer `/etc/exports` indicant quines carpetes es volen compartir i els permisos per cada una.

Cada línia del fitxer `/etc/exports` especifica un directori a exportar i una llista d’autoritzacions.


  ```
  /srv/nfs/compartit1   *(rw)
  /srv/nfs/compartit2   172.30.0.0/16(ro)
  ```

* En la **primera línia** compartim la carpeta `/srv/nfs/comptartit1` per a tots els equips de la xarxa (** * **) amb permissos de lectura i escriptura (**rw**).
* En la **segona línia** compartim la carpeta `/srv/nfs/comptartit2` per a tots els equips de tota la xarxa **172.30.0.0/16** amb permissos de només de lectura [_read only_] (**ro**).

Cada vegada que es modifica aquest fitxer, el **servidor NFS s’ha d’actualitzar** a fi que s’activin els canvis amb l’ordre: 

```
sudo exportfs –ra
```

O també podem **reiniciar el servei NFS** per tal que s'actualitzin els canvis:

```
sudo service nfs-kernel-server reload
```

### Opcions de compartició

> Els **permisos** que tindrà un usuari quan accedeix a una carpeta compartida seran els **més restrictius** entre els permisos locals i els permisos de compartició, però també dependrà d'un **sistema de transformació d'usuaris** que pot realitzar el sistema NFS.

El sistema de transformació d'usuari s'indica com a paràmetre al configurar el fitxer `/etc/exports`.

  ```
  /srv/nfs/compartit1   *(rw,no_root_squash,no_subtree_check,no_wdelay,sync)
  ```

Aquest sistema de transformació d'usuaris es realitza en dos passos:

**Transformació a usuari anònim**
Només es pot posar un dels següents paràmetres:
* **root_squash** (per defecte): indica que si s'accedeix amb l'usuari root, aquest es transforma en l'usuari anònim (usuari **nobody**, grup **nogroup**).
* **no_root_squash**: ningú es transformarà en usuari anònim.
* **all_squash**: tothom es transforma en usuari anònim (usuari **nobody**, grup **nogroup**).

> **ATENCIÓ**: no és recomanable posar **no_root_squash**, ja que el root d'una màquina no té perquè ser el mateix que en una altra, però igualment tindrà tots els privilegis!

**Transformació de l'usuari anònim en un usuari/grup concret**

Es pot posar un dels dos paràmetres, tots dos o cap:

* **anonuid=nnnn**: transforma l'usuari anònim en l'usuari amb l'identificador nnnn
* **anongid=nnnn**: transforma el grup anònim en el grup amb l'identificador nnnn

> **ATENCIÓ**: aquest identificador fa referència a un usuari o grup del servidor, però el mateix usuari o grup pot tenir un identificador diferent en el client. Si es tracta d'usuaris LDAP (domini), això no té importància: tots els usuaris tenen el mateix indicador en totes les màquines.

### Veure les carpetes que s'estan compartint

Es pot fer amb la comanda `exportfs` o, si s'ha instal·lat el client nfs, amb la comanda `showmount -e localhost`:

```bash+theme:dark
usuari@usxxx:~$ sudo exportfs
/srv/nfs/compartit1
        <world>
/srv/nfs/compartit2
        172.30.0.0/16

usuari@usxxx:~$ showmount -e localhost
Export list for localhost:
/srv/nfs/compartit1      *
/srv/nfs/compartit2      172.30.0.0/16
````

## Instal·lació i configuració del client NFS

### Instal·lació del client NFS

En cada equip **client** des del qual es vulgui accedir a una carpeta remota (compartida), haurem de instal·lar el paquet **nfs-common**:

```
sudo apt update
sudo apt install nfs-common
```

Amb la comanda **showmount** es poden veure les carpetes que comparteix el servidor:

```bash+theme:dark
usuari@ucxxx:~$ showmount -e 172.30.0.20
Export list for 172.30.0.20:
/srv/nfs/compartit1     *
/srv/nfs/compartit2     172.30.0.0/16
```



### Muntar carpetes compartides

Primer **creem la carpeta** que farem servir després com a **punt de muntatge** per a la carpeta compartida amb el servidor. 

Això es fa normalment dins de la carpeta `/mnt` en una carpeta amb el nom del servei, en aquest cas, `nfs`:

```
sudo mkdir -p /mnt/nfs/compartit1
```

Després cal muntar less carpetes remotes compartides dins d'aquestes carpetes locals.
Es poden **muntar de forma manual** mitjançant la comanda `mount`

```
sudo mount -t nfs 172.30.0.20:/srv/nfs/compartit1 /mnt/nfs/compartit1
```

### Muntar carpetes compartides de forma automàtica

També es pot fer servir el fitxer `/etc/fstab` si es vol que el directori es **munti automàticament** al iniciar sessió.

```
172.30.0.20:/srv/nfs/compartit1 /mnt/nfs/compartit1 nfs rw 0 0
```

Per muntar automàticament els recussos definits a `/etc/fstab` sense necessitat de reiniciar el sistema podeu executar.

```
sudo mount -a
```

### Comprovar que s'ha muntat una carptera compartida

Per comprovar si s'han muntat correctament les carpetes es pot utilitzar la comanda **mount**.

```bash+theme:dark
usuari@ucxxx:~$ mount
...
172.30.0.20:/srv/nfs/compartit1 on /mnt/nfs/compartit1 type nfs (rw, ... ,_netdev)
...
```

O també es pot fer:

```bash+theme:dark
usuari@ucxxx:~$ df -h --type=nfs
S.ficheros                      Tamaño Usados  Disp Uso% Montado en
172.30.0.20:/srv/nfs/compartit1   9,8G   1,6G  7,7G  17% /mnt/nfs/compartit1
172.30.0.20:/srv/nfs/compartit2   9,8G   1,6G  7,7G  17% /mnt/nfs/compartit2
```

>A partir d'aquest moment, quan s'accedeix a aquestes carpetes locals, en realitat s'estarà accedint a les carpetes remotes compartides.

Amb la comanda `ls -l` es poden veure els propietaris i permisos de les carpetes remotes:

```bash+theme:dark
usuari@ucxxx:~$ ls -l /mnt/nfs
drwxrwxr-x 3 root     profes   4096 ene 29 11:01 compartit1
drwxrwxr-x 2 alumne   alumnes  4096 ene 29 11:01 compartit2
```

## Documentació i recursos

* **Apunts SOX (Pere Sánchez): Compartició de carpetes en Linux**     
  [http://moodlecf.sapalomera.cat/apunts/smx/sox/index.html?cap=2.8.7 ](http://moodlecf.sapalomera.cat/apunts/smx/sox/index.html?cap=2.8.7)

* **NFS: Sistema de archivos de red**
  [http://recursostic.educacion.es/observatorio/web/gl/software/software-general/733-nfs-sistema-de-archivos-de-red](http://recursostic.educacion.es/observatorio/web/gl/software/software-general/733-nfs-sistema-de-archivos-de-red)
  
* **Compartir carpetas NFS**
  [https://waytoit.wordpress.com/2013/03/17/compartir-carpetas-nfs/](https://waytoit.wordpress.com/2013/03/17/compartir-carpetas-nfs/)




