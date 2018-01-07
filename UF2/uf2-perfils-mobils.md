# Perfils mòbils

## Introducció

> Configurar **perfils mòbils** serveix per evitar que cada cop que un usuari canviï de màquina, hagi de tornar a configurar el seu entorn de treball.

A més, amb els perfils mòbils, els **documents** que l'usuari guardi a la seva carpeta personal, també **els trobarà en qualsevol màquina** a la que vagi a treballar.

Però també hi ha un **inconvenient**: 
* Si hi ha molts clients o els clients tenen moltes dades, pot augmentar molt la càrrega del servidor i de la xarxa.

En **Linux**, per poder utilitzar perfils mòbils cal fer els següents passos:

1. Crear una **carpeta** en el servidor on es guardaran els **perfils dels usuaris** del domini.
2. **Compartir** aquesta carpeta de forma que s'hi pugui accedir des dels clients.
3. En els **clients**, s'ha de fer que **montin automàticament aquesta carpeta** remota cada cop que arrenqui el sistema.

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

**Nota**: El paràmetre **_-p_** crea tots els directoris anidats si no existeixen.

### Enllaçar la carpeta compartida amb la carpeta local d'usuaris del domini

Si s'ha configurat el servidor per fer que es puguin validar usuaris del domini, també s'han de fer les següents configuracions:

1. **Crear la carpeta** `/home/ldapxxx` (si no està ja creada):

  `sudo mkdir /home/ldapxxx`

2. **Enllaçar la carpeta** que es vol compartir (`/srv/nfs/ldapxxx`) amb el directori on es troben les carpetes dels usuaris del domini (`/home/ldapxxx`).
Per fer que s'enllacin automàticament cada cop que arrenqui el servidor, afegirem la següent línia al final de l'arxiu `/etc/fstab` (és similar a muntar una partició en una carpeta, però el tipus de format és none i l'única opció que posarme és bind):

  ```
  # Enllaçar la carpeta d'usuaris de LDAP amb la carpeta compartida amb NFS
  /home/ldapxxx      /srv/nfs/ldapxxx      none      bind      0      4
  ```

3. I per **enllaçar immediatament**, sense haver de reiniciar:

   `sudo mount -a`

### Configurar el servei per compartir la carpeta dels usuaris del domini

El **servei NFS** es configura en l'arxiu `/etc/exports`.

S'ha d'afegir la següent línia que serveix per **compartir la carpeta** on es troben els perfils dels usuaris:

  ```
  /srv/nfs/ldapxxx   *(rw,no_root_squash,no_subtree_check,no_wdelay,sync)
  ```

Com sempre que es modifica la configuració d'un servei, cal **reiniciar-lo** i comprovar que no hi hagi errors:

```bash+theme:dark
usuari@usxxx:~$ sudo service nfs-kernel-server restart
```

Per **comprovar** que s'està compartint la carpeta:

```bash+theme:dark
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

1. Si en LDAP s'ha configurat que **el directori dels usuaris** del domini sigui `/home/ldapxxx`, el primer que s'ha de fer és **crear** aquesta **carpeta** (a no ser que ja existeixi):

  `sudo mkdir /home/ldapxxx`

2. Després s'ha de fer que es **munti automàticament** cada cop que s'engegui la màquina, afegint la següent línia a l'arxiu `/etc/fstab`:

  ```
  # Muntar la carpeta remota d'usuaris en el servidor
  172.30.A.20:/srv/nfs/ldapxxx   /home/ldapxxx   nfs    _netdev,auto  0  4
  ```

3. Per **muntar la carpeta remota immediatament**, sense haver de reiniciar (cal comprovar que no doni cap error):

  `sudo mount -a`

## Comprovació dels perfils mòbils en els clients

### Comprovar des de la consola

Comprovar que **es pot validar un usuari** (la primera vegada es crea la seva carpeta personal):

```bash+theme:dark
usuari@ucxxx:~$ sudo login conserge
Contraseña:
Welcome to Ubuntu 16.04.1 LTS (GNU/Linux 4.4.0-45-generic x86_64)
...
conserge@ucxxx:~$
```

Comprovar que l'usuari **pot crear un arxiu**:

  ```bash+theme:dark
  conserge@ucxxx:~$ touch prova
  ```

**Des del servidor**, comprovar que existeix la carpeta d'aquest usuari i que s'ha creat l'arxiu amb el propietari i grup correctes:

```bash+theme:dark
usuari@usxxx:~$ ls -l /home/ldapxxx/conserge
total 0
-rw-r--r-- 1 conserge administratius 0 nov 19 19:46 prova
```

### Comprovar des de l'entorn gràfic

En el client, tancar la sessió de l'usuari actual i intentar validar un usuari del domini (no cal indicar el domini).

Es pot mostrar el nom de l'usuari al costat del botó d'apagada anant a **_Configuración del sistema_** → **_Cuentas de usuario _**i marcant la casella **_Mostrar mi nombre de usuario en la barra de menús_**.

**Des del servidor**, comprovar quins arxius s'han creat en la seva carpeta personal (carpeta del perfil):

```bash+theme:dark
usuari@usxxx:~$ ls -l /home/ldapxxx/pverde/
total 8
drwxr-xr-x 2 conserge administratius 1024 nov 19 20:03 Descargas
drwxr-xr-x 2 conserge administratius 1024 nov 19 20:03 Documentos
drwxr-xr-x 2 conserge administratius 1024 nov 19 20:03 Escritorio
drwxr-xr-x 2 conserge administratius 1024 nov 19 20:03 Imágenes
drwxr-xr-x 2 conserge administratius 1024 nov 19 20:03 Música
drwxr-xr-x 2 conserge administratius 1024 nov 19 20:03 Plantillas
-rw-r--r-- 1 conserge administratius    0 nov 19 19:46 prova
drwxr-xr-x 2 conserge administratius 1024 nov 19 20:03 Público
drwxr-xr-x 2 conserge administratius 1024 nov 19 20:03 Vídeos
```

## Deshabilitar els perfils mòbils

### En els clients

1. En l'arxiu `/etc/fstab`, **comentar o eliminar la línia que munta la carpeta remota** dels usuaris del domini:

  ```
  # 172.30.A.20:/srv/nfs/ldapxxx   /home/ldapxxx   nfs    _netdev,auto  0  4
  ```

2. **Desmuntar aquesta carpeta** sense haver de reiniciar el sistema:

  `sudo umount /home/ldapxxx`

3. Es pot **comprovar** que aquesta carpeta ja no està muntada utilitzant la comanda mount.

> A partir d'aquest moment, els perfils es crearan en els clients en lloc de fer-ho en el servidor.

### En el servidor

1. En l'arxiu `/etc/exports`, **comentar o eliminar la línia que comparteix la carpeta** en el sistema NFS:

  ```
  # /srv/nfs/ldapxxx   *(rw,no_root_squash,no_subtree_check,no_wdelay,sync)
  ```

2. **Reiniciar el sistema NFS**:

  `sudo service nfs-kernel-server reload`

3. Amb la comanda `exportfs` es pot **comprovar** que ja no s'està compartint aquesta carpeta:

  ```bash+theme:dark
  usuari@usxxx:~$ sudo exportfs
  usuari@usxxx:~$
  ```

4. En l'arxiu `/etc/fstab`, **comentar o eliminar la línia que enllaça la carpeta dels usuaris amb la carpeta compartida** amb el sistema NFS:

  ```
  # /home/ldapxxx      /srv/nfs/ldapxxx      none      bind      0      4
  ```

5. **Desenllaçar aquestes carpetes** sense haver de reiniciar el sistema:

  `sudo umount /srv/nfs/ldapxxx`

6. Es pot **comprovar** que aquestes carpetes ja no estan enllaçades utilitzant la comanda mount.
