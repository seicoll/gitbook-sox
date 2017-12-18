# Perfils mòbils

## Introducció

Configurar **perfils mòbils** serveix per evitar que cada cop que un usuari canviï de màquina, hagi de tornar a configurar el seu entorn de treball.

A més, amb els perfils mòbils, els documents que l'usuari guardi a la seva carpeta personal, també els trobarà en qualsevol màquina a la que vagi a treballar.

Però també hi ha un **inconvenient**: si hi ha molts clients o els clients tenen moltes dades, pot augmentar molt la càrrega del servidor i de la xarxa.

En **Linux**, per poder utilitzar perfils mòbils cal fer els següents passos:

1. Crear una carpeta en el servidor on es guardaran els perfils dels usuaris del domini.
2. Compartir aquesta carpeta de forma que s'hi pugui accedir des dels clients.
3. En els clients, s'ha de fer que montin automàticament aquesta carpeta remota cada cop que arrenqui el sistema.

## Configuració del servidor

### Instal·lar el servei de compartició de carpetes en xarxa (NFS)

El servei **NFS** és el sistema que utilitza Linux per compartir carpetes en xarxa.

El paquet que s'ha d'instal·lar és el **_nfs-kernel-server_**:

```
sudo apt update
sudo apt install nfs-kernel-server
```

### Crear la carpeta que s'ha de compartir

El primer que cal fer és **crear el directori** que servirà de base pel sistema NFS i la carpeta on es guardaran els perfils dels usuaris del domini. 

Si en **LDAP** s'ha configurat que el directori dels usuaris del domini sigui `/home/ldapxxx`, s'ha de crear la carpeta `ldapxxx` dins del directori base de NFS:

`sudo mkdir -p /srv/nfs/ldapxxx`

### Enllaçar la carpeta compartida amb la carpeta local d'usuaris del domini

Si s'ha configurat el servidor per fer que es puguin validar usuaris del domini, també s'han de fer les següents configuracions:

* Crear (si no està ja creada) la carpeta `/home/ldapxxx`:

`sudo mkdir /home/ldapxxx`

* Enllaçar la carpeta que es vol compartir (`/srv/nfs/ldapxxx`) amb el directori on es troben les carpetes dels usuaris del domini (`/home/ldapxxx`).
Per fer que s'enllacin automàticament cada cop que arrenqui el servidor, afegirem la següent línia a l'arxiu /etc/fstab (és similar a muntar una partició en una carpeta, però el tipus de format és none i l'única opció és bind):

```
# Enllaçar la carpeta d'usuaris de LDAP amb la carpeta compartida amb NFS
/home/ldapxxx      /srv/nfs/ldapxxx      none      bind      0      4
```

* I per enllaçar immediatament, sense haver de reiniciar:

`sudo mount -a`

### Configurar el servei per compartir la carpeta dels usuaris del domini

El servei NFS es configura en l'arxiu `/etc/exports`.
S'ha d'afegir la següent línia que serveix per compartir la carpeta on es troben els perfils dels usuaris:

```
/srv/nfs/ldapxxx   *(rw,no_root_squash,no_subtree_check,no_wdelay,sync)
```

Com sempre que es modifica la configuració d'un servei, cal reiniciar-lo i comprovar que no hi hagi errors:

```sh
usuari@usxxx:~$ sudo service nfs-kernel-server restart
```

Per comprovar que s'està compartint la carpeta:

```sh
usuari@usxxx:~$ sudo exportfs
/srv/nfs/ldapxxx
        <world>
usuari@usxxx:~$
```

## Configuració de les màquines clients

### Instal·lar el client del servei NFS

Per utilitzar el **servei NFS** (accedir a carpetes compartides en xarxa) cal instal·lar el paquet client de NFS, **_nfs-common_**:

`sudo apt install nfs-common`

### Crear la carpeta on s'ha de muntar la carpeta remota

Si en LDAP s'ha configurat que el directori dels usuaris del domini sigui `/home/ldapxxx`, el primer que s'ha de fer és crear aquesta carpeta (a no ser que ja existeixi):

`sudo mkdir /home/ldapxxx`

Després s'ha de fer que es munti automàticament cada cop que s'engegui la màquina, afegint la següent línia a l'arxiu `/etc/fstab`:

```
# Muntar la carpeta remota d'usuaris en el servidor
172.30.A.20:/srv/nfs/ldapxxx   /home/ldapxxx   nfs    _netdev,auto  0  4
```

Per muntar la carpeta remota sense haver de reiniciar (cal comprovar que no doni cap error):

`sudo mount -a`

## Comprovació dels perfils mòbils en els clients

### Comprovar des de la consola

Comprovar que es pot validar un usuari (la primera vegada es crea la seva carpeta personal):

```sh
usuari@ucxxx:~$ sudo login pverde
Contraseña:
Welcome to Ubuntu 16.04.1 LTS (GNU/Linux 4.4.0-45-generic x86_64)
...
pverde@ucxxx:~$
```

Comprovar que l'usuari pot crear un arxiu:

```sh
pverde@ucxxx:~$ touch prova
```

**Des del servidor**, comprovar que existeix la carpeta d'aquest usuari i que s'ha creat l'arxiu amb el propietari i grup correctes:

```sh
usuari@usxxx:~$ ls -l /home/ldapxxx/pverde
total 0
-rw-r--r-- 1 pverde profes 0 nov 19 19:46 prova
```

### Comprovar des de l'entorn gràfic

En el client, tancar la sessió de l'usuari actual i intentar validar un usuari del domini (no cal indicar el domini).
Es pot mostrar el nom de l'usuari al costat del botó d'apagada anant a Configuración del sistema → Cuentas de usuario i marcant la casella Mostrar mi nombre de usuario en la barra de menús.
Des del servidor, comprovar quins arxius s'han creat en la seva carpeta personal (carpeta del perfil):
usuari@usxxx:~$ ls -l /home/ldapxxx/pverde/
total 8
drwxr-xr-x 2 pverde profes 1024 nov 19 20:03 Descargas
drwxr-xr-x 2 pverde profes 1024 nov 19 20:03 Documentos
drwxr-xr-x 2 pverde profes 1024 nov 19 20:03 Escritorio
drwxr-xr-x 2 pverde profes 1024 nov 19 20:03 Imágenes
drwxr-xr-x 2 pverde profes 1024 nov 19 20:03 Música
drwxr-xr-x 2 pverde profes 1024 nov 19 20:03 Plantillas
-rw-r--r-- 1 pverde profes    0 nov 19 19:46 prova
drwxr-xr-x 2 pverde profes 1024 nov 19 20:03 Público
drwxr-xr-x 2 pverde profes 1024 nov 19 20:03 Vídeos

