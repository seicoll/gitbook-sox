# Gestió d'usuaris i grups locals en Linux

## Introducció

Linux és un sistema **multiusuari**, és a dir, està pensat perquè diversos usuaris treballin a la vegada, i cadascun disposa del seu propi espai d'emmagatzematge per desar els seus arxius.

Per accedir a un sistema Linux,** s'ha de tenir un compte d'usuari**, és a dir, una parella **login/password** que l’administrador del sistema ha d’haver donat d’alta.

Només l'usuari **_root_**, també anomenat **superusuari**, que en Linux és l'administrador del sistema, pot crear, eliminar o administrar els comptes d'usuari.


## Tipus d'usuaris

Existeix 3 tipus d'usuaris:

1. **Usuari Normal**
  * Cada usuari té la seva carpeta personal.
  * El seu directori arrel és `/home/<username>`.
  * Exemples: raul, sergi, mrodriguez, etc. 

2. ** Usuaris de Sistema**
  * Són usuaris propis del sistema necessaris per algunes tasques que ha de realitzar el SO.
  * Aquest tipus d'usuari no pot ingressar al sistema amb un login normal. 
  * Exemples: mail, ftp, bin, sys, proxy, etc. 

3. **Usuari root (superusuari)**
  * Tot sistema operatiu GNU/Linux té un superusuari.
  * Té els màxims privilegis que li permetran efectuar qualsevol operació sobre el sistema.
  * És més segur treballar habitulament amb un usuari normat.
  * El seu directori **arrel** és `/root` i el seu número d’usuari (**_UID_**) és 0.


## Creació d'usuaris

### adduser

La comanda `adduser` serveix per **crear usuaris**.

* El nom d'usuari no pot començar amb un número ni incloure accents ni determinats símbols.
Si es vol evitar aquestes restriccions, es pot afegir el paràmetre `--force-badname`.

* Per defecte, quan es crea un usuari també **es crea un grup amb el seu mateix nom** i se li assigna com a **grup principal**.

  > Tot usuari ha de pertànyer, almenys, a un grup, encara que pot ser de més d'un.

* La **carpeta de l'usuari** no es crea fins que l'usuari es valida per primera vegada.
Per defecte, les carpetes d'usuari es creen dins de `/home` i se li copia el contingut de la carpeta `/etc/skel`.

Per **crear un usuari**:

`sudo adduser <usuari>`

**_--ingroup_**: Per crear un usuari i assignar-li el grup principal (el grup ha d'existir):

`sudo adduser <usuari> --ingroup <grup>`

**_-d, --home_**: Per assignar un directori $HOME a l'usuari:

`sudo adduser <usuari> --home <directori_home>`

## Eliminació d'usuaris

### deluser

La comanda `deluser` serveix per **eliminar usuaris**.

Per defecte, **no esborra la carpeta de l'usuari.** Si es vol esborrar cal afegir el paràmetre `--remove-home`.

Per **eliminar un usuari**:

`sudo deluser <usuari>`

**_--remove-home_**: Per eliminar un usuari i el seu directori:

`sudo deluser --remove-home <usuari>`

## Creació de grups

### addgroup

La comanda `addgroup` serveix per **crear grups**.

Per crear un grup:

`sudo addgroup <grup>`

## Eliminació e grups

### delgroup

La comanda `delgroup` serveix per **eliminar grups**.

Per eliminar un grup:

`sudo delgroup <grup>`

## Assignar usuaris a grups

### adduser

Per **afegir un grup secundari a un usuari**

> **ATENCIÓ**: l'usuari i el grup han d'existir.

`sudo adduser <usuari> <grup>`

### usermod

Serveix per **canviar la configuració** del compte d'usuari.

Per exemple, es pot canviar el nom del compte (**login**), el grup principal, afegir o treure grups secundaris, canviar i/o moure el directori personal, canviar l'identificador, l'intèrpret de comandes per defecte (**shell**)...

**_-g_**: Per **canviar el grup principal** de l'usuari.

`sudo usermod -g <grup> <usuari>`

**_-aG_**: Per afegir l'usuari a **grups secundaris**:

`sudo usermod -aG <grup> [grup ...] <usuari>`

**_-m_**: Per **canviar el directori personal** i moure els seus arxius al nou directori:

`sudo usermod -m -d /home/nou_dir <usuari>`

**_-l_**: Per **canviar el nom del compte (login)**:

`sudo usermod -l nou_login <usuari>`

**_-u_**: Per **canviar l'identificador del compte (UID)**; `nou_id` no ha d'existir i ha de ser un número positiu:

`sudo usermod -u nou_id <usuari>`

## Canviar contrassenyes

### passwd

La comanda `passwd` serveix per assignar o canviar contrasenyes.

> **ATENCIÓ:** un usuari que no tingui contrasenya no pot accedir al sistema.

Per **canviar la pròpia contrasenya** (la de l'usuari amb el què s'està treballant):

`passwd`

Per **canviar la contrasenya d'un usuari** (si no es posa usuari, s'aplica al root):

`sudo passwd <usuari>`

Per **eliminar la contrasenya d'un usuari i desactivar el compte** (si no es posa usuari, s'aplica al root):

`sudo passwd -l <usuari>`

Per **reactivar un compte d'usuari** que ha estat desactivat.

`sudo passwd -u <usuari>`

## Iniciar sessió

**Iniciar sessió amb un altre usuari**

Per **canviar a l'usuari root**:

`sudo su`

Per **canviar a un altre usuari**:

`sudo login <usuari>`

Per **tancar sessió** i tornar a la sessió del l'usuari anterior:

`exit`

Per saber en **quin usuari hem iniciat la secció actual**.

`whoami`


## Veure informació sobre usuaris i grups

### Per comandes

**id [usuari]**

Mostra l'**identificador de l'usuari (_UID_)** i els **grups al que pertany** un usuari juntament amb l'idenficacio de cada grup (_GID_).

```bash+theme:dark
usuari@ucxxx:~$ id
uid=1000(usuari) gid=1000(usuari) grupos=1000(usuari),4(adm),27(sudo),46(plugdev)...
```

**groups [usuari]**

Mostra els **noms dels grups als que pertany** un usuari.

> **NOTA**: El primer grup que apareix és el grup principal.

```bash+theme:dark
usuari@ucxxx:~$ groups
usuari adm cdrom sudo dip plugdev lpadmin sambashare
```

**getent passwd **

Mostra **informació dels usuaris**. Pot mostrar tant usuaris locals com de domini (LDAP).

```bash+theme:dark
usuari@ucxxx:~$ getent passwd
root:x:0:0:root:/root:/bin/bash
...
usuari:x:1000:1000:usuari,,,:/home/usuari:/bin/bash
alumne:x:1001:1001:alumne,,,,:/home/alumne:/bin/bash
profe:x:1002:1002:profe,,,,:/home/profe:/bin/bash
director:x:1003:1003:,,,:/home/director:/bin/bash
```

Per mostrar la **informació només d'un usuari**: 

`getent passwd <usuari>`

**getent group **

Mostra **informació dels grups**. Pot mostrar tant grups locals com de domini (LDAP).

```bash+theme:dark
usuari@ucxxx:~$ getent group
root:x:0:
sudo:x:27:usuari
...
usuari:x:1000:
alumnes:x:1001:
profes:x:1002:usuari,director
director:x:1003:
```

Per mostrar la **informació només d'un grup**:

`getent group <grup>`


### A través de fitxers especials

Hi ha diversos **fitxers de text** en Linux que contenen informació referent als usuaris i als grups d'usuaris donats d'alta en el sistema.

**/etc/passwd**
Conté la informació dels usuaris del sistema (nom, directori home, etc.)

**/etc/shadow**
Conté la les contrasenyes xifrades dels usuaris.

**/etc/group**
Conté la informació dels grups.

* Informació de cada línia del fitxer

  `nomgrup:password:GID:Llista_Usuaris`




