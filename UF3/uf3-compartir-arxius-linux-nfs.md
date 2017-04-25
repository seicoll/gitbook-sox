# Compartició d'arxius i carpetes en GNU/Linux

## Introducció

### Conceptes bàsics

En els sistemes operatius lliures hi ha diversos protocols i aplicacions que ens permeten compartir recursos en xarxa, com el **protocol NFS** i el paquet de programari **Samba**.

### Protocol NFS \(Network File System\)

El **protocol NFS \(**_**Network File System**_**\)** és un protocol que s’utilitza en l’àmbit de els xarxes local per compartir fitxers entre màquines de la mateixa xarxa.

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

El paquet que cal instal·lar en qualsevol ordinador que hagi de compartir carpetes amb el sistema NFS és **nfs-kernel-server**. 
Per instal·lar-lo cal executar la comanda:

```
sudo apt-get install nfs-kernel-server
```

### Configuració del servei NFS

Una vegada actius els serveis NFS, el servidor ha d’indicar quins directoris vol que **s’exportin (compartir)**, a quines màquines s’han d’exportar i amb quines opcions s’ha de fer. 

Tot això es defineix al fitxer ```/etc/exports``` indicant quines carpetes es volen compartir i els permisos per cada una.

```bash
/srv/nfs/compartit   172.21.1.0/16(rw)
```

Cada línia del fitxer ```/etc/exports``` especifica un directori a exportar i una llista d’autoritzacions.
* En aquest **exemple** compartim la carpeta /srv/nfs/comptartit per a tots els equips de la xarxa 172.21.1.0/16 amb permissos de lectura i escriptura (rw).

Cada vegada que es modifica aquest fitxer, el **servidor NFS s’ha d’actualitzar** a fi que s’activin els canvis amb l’ordre: 

```
sudo exportfs –ra
```

O també podem **reiniciar el servei NFS** per tal que s'actualitzin els canvis:

```
sudo service nfs-kernel-server reload
```

### Veure les carpetes que s'estan compartint

Es pot fer amb la comanda sudo exportfs o, si s'ha instal·lat el client nfs, amb la comanda showmount -e localhost:

```
usuari@ubuntu:~$ sudo exportfs
/srv/nfs/Compartit
        <world>
/srv/nfs/Compartit2
        172.21.1.0/16

usuari@ubuntu:~$ showmount -e localhost
Export list for localhost:
/srv/nfs/Compartit       *
/srv/nfs/Compartit2      172.21.1.0/16
````



## Instal·lació i configuració del client NFS

### Instal·lació client NFS

En cada equip **client** des del qual es vulgui accedir a una carpeta remota, haurem de instal·lar el paquet **nfs-common**:

```
sudo apt-get install nfs-common
```

A continuació, creem la carpeta que farem servir després com a punt de muntatge per a la carpeta compartida amb el servidor.

```
sudo mkdir /mnt/nfs/compartit
```

### Muntar carpetes compartides

Els directoris remots es poden **muntar de forma manual** mitjançant l’ordre `mount`

```
sudo mount -t nfs 172.21.1.1:/srv/nfs/compartit /mnt/nfs/compartit
```

Per comprovar si s'han muntat correctament les carpetes es pot utilitzar la comanda mount.

```bash
usuari@ubuntu:~$ mount
...
172.21.1.1:/srv/nfs/compartit on /mnt/nfs/compartit type nfs (rw, ... ,_netdev)
...
```

### Muntar carpetes compartides de forma automàtica

També es pot fer servir el fitxer `/etc/fstab` si es vol que el directori es munti automàticament al iniciar sessió.

```
172.21.1.1:/srv/nfs/compartit /mnt/nfs/compartit nfs rw 0 0
```

Per muntar automàticament els recussos definits a `/etc/fstab` sense necessitat de reiniciar el sistema podeu executar.

```
sudo mount -a
```

### Comprovar que s'ha muntat un directori remot

A partir d'aquest moment, quan s'accedeix a aquestes carpetes locals, en realitat s'estarà accedint a les carpetes remotes compartides.

Amb la comanda `ls -l` es poden veure els propietaris i permisos de les carpetes remotes:

```
usuari@ubuntu:~$ ls -l /mnt/nfs
drwxrwxr-x 3 root     profes   4096 ene 29 11:01 Compartit
drwxrwxr-x 2 alumne   alumnes  4096 ene 29 11:01 Compartit2
```

## Documentació i recursos

* NFS: Sistema de archivos de red  [http://recursostic.educacion.es/observatorio/web/gl/software/software-general/733-nfs-sistema-de-archivos-de-red](http://recursostic.educacion.es/observatorio/web/gl/software/software-general/733-nfs-sistema-de-archivos-de-red)
  
* Cómo montar un sistema de ficheros NFS (Cliente Linux)
  [http://rm-rf.es/como-montar-sistema-ficheros-nfs/](http://rm-rf.es/como-montar-sistema-ficheros-nfs/)
  
* Compartir carpetas NFS
  [https://waytoit.wordpress.com/2013/03/17/compartir-carpetas-nfs/](https://waytoit.wordpress.com/2013/03/17/compartir-carpetas-nfs/)




