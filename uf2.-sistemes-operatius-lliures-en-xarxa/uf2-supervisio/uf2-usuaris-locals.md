# Gestió d'usuaris i grups

## Introducció

Linux és un sistema **multiusuari**, és a dir, està pensat perquè diversos usuaris treballin a la vegada, i cadascun disposa del seu propi espai d'emmagatzematge per desar els seus arxius.

Per accedir a un sistema Linux, **s'ha de tenir un compte d'usuari**, és a dir, una parella **login/password** que l’administrador del sistema ha d’haver donat d’alta.

Només l'usuari _**root**_, també anomenat **superusuari**, que en Linux és l'administrador del sistema, pot crear, eliminar o administrar els comptes d'usuari.

## Tipus d'usuaris

Existeix 3 tipus d'usuaris:

1. **Usuari Normal**
   * Cada usuari té la seva carpeta personal.
   * El seu directori arrel és `/home/<username>`.
   * Exemples: raul, sergi, mrodriguez, etc. 
2.  **Usuaris de Sistema**
   * Són usuaris propis del sistema necessaris per algunes tasques que ha de realitzar el SO.
   * Aquest tipus d'usuari no pot ingressar al sistema amb un login normal. 
   * Exemples: mail, ftp, bin, sys, proxy, etc. 
3. **Usuari root \(superusuari\)**
   * Tot sistema operatiu GNU/Linux té un superusuari.
   * Té els màxims privilegis que li permetran efectuar qualsevol operació sobre el sistema.
   * És més segur treballar habitulament amb un usuari normat.
   * El seu directori **arrel** és `/root` i el seu número d’usuari \(_**UID**_\) és 0.

## Creació d'usuaris

### adduser

La comanda `adduser` serveix per **crear usuaris**.

* El nom d'usuari no pot començar amb un número ni incloure accents ni determinats símbols. Si es vol evitar aquestes restriccions, es pot afegir el paràmetre `--force-badname`.
* Per defecte, quan es crea un usuari també **es crea un grup amb el seu mateix nom** i se li assigna com a **grup principal**.

  > Tot usuari ha de pertànyer, almenys, a un grup \(**grup principal**\), encara que pot ser de més d'un.

* La **carpeta de l'usuari** no es crea fins que l'usuari es valida per primera vegada. Per defecte, les carpetes d'usuari es creen dins de `/home` i se li copia el contingut de la carpeta `/etc/skel`.

Per **crear un usuari**:

`sudo adduser <usuari>`

_**--ingroup**_: Per crear un usuari i assignar-li el grup principal \(el grup ha d'existir\):

`sudo adduser <usuari> --ingroup <grup>`

_**-d, --home**_: Per assignar un directori $HOME a l'usuari:

`sudo adduser <usuari> --home <directori_home>`

## Eliminació d'usuaris

### deluser

La comanda `deluser` serveix per **eliminar usuaris**.

Per defecte, **no esborra la carpeta de l'usuari.** Si es vol esborrar cal afegir el paràmetre `--remove-home`.

Per **eliminar un usuari**:

`sudo deluser <usuari>`

_**--remove-home**_: Per eliminar un usuari i el seu directori:

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

Serveix per **canviar la configuració** del compte d'usuari, així com bloquejar i desbloquejar un compte.

Per exemple, es pot canviar el nom del compte \(**login**\), el grup principal, afegir o treure grups secundaris, canviar i/o moure el directori personal, canviar l'identificador, l'intèrpret de comandes per defecte \(**shell**\)...

_**-g**_: Per **canviar el grup principal** de l'usuari.

`sudo usermod -g <grup> <usuari>`

_**-aG**_: Per afegir l'usuari a **grups secundaris**:

`sudo usermod -aG <grup> [, grup ...] <usuari>`

_**-m**_: Per **canviar el directori personal** i moure els seus arxius al nou directori:

`sudo usermod -m -d /home/nou_dir <usuari>`

_**-l**_: Per **canviar el nom del compte \(login\)**:

`sudo usermod -l nou_login <usuari>`

_**-L**_: Per **deshabilitar temporalment un usuari**:

`sudo usermod -L <usuari>`

_**-u**_: Per **canviar l'identificador del compte \(UID\)**; `nou_id` no ha d'existir i ha de ser un número positiu:

`sudo usermod -u nou_id <usuari>`

## Canviar contrassenyes

### passwd

La comanda `passwd` serveix per assignar o canviar contrasenyes.

> **ATENCIÓ:** un usuari que no tingui contrasenya no pot accedir al sistema.

Per **canviar la pròpia contrasenya** \(la de l'usuari amb el què s'està treballant\):

`passwd`

Per **canviar la contrasenya d'un usuari** \(si no es posa usuari, s'aplica al root\):

`sudo passwd <usuari>`

Per **eliminar la contrasenya d'un usuari i desactivar el compte** \(si no es posa usuari, s'aplica al root\):

`sudo passwd -l <usuari>`

Per **reactivar un compte d'usuari** que ha estat desactivat.

`sudo passwd -u <usuari>`

### chage

La comanda `chage` modifica el nombre de dies entre canvis de contrasenya i la data de l'últim canvi de contrasenya.

Per **obtenir informació sobre el 'temps de vida' de la contrasenya** d'un usuari:

`sudo chage -l <usuari>`

\[IMATGE\]

Per definir que l'usuari hagi de **canviar la contrasenya cada cert temps** \(per exemple 90 dies\):

`sudo chage -M 90 <usuari>`

Per **definir la data de caducitat de la contrasenya** \(per exemple el proper 17/03/2020\):

`sudo chage -E 2020-03-17 <usuari>`

Per **comprovar que els canvis s'han fet** efectius:

`sudo chage -l <usuari>`

\[IMATGE\]

## Iniciar sessió amb un altre usuari

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

#### id \[usuari\]

Mostra l'**identificador de l'usuari \(**_**UID**_**\)** i els **grups al que pertany** un usuari juntament amb l'idenficacio de cada grup \(_GID_\).

```text
usuari@ucxxx:~$ id
uid=1000(usuari) gid=1000(usuari) grupos=1000(usuari),4(adm),27(sudo),46(plugdev)...
```

#### groups \[usuari\]

Mostra els **noms dels grups als que pertany** un usuari.

> **NOTA**: El primer grup que apareix és el grup principal.

```text
usuari@ucxxx:~$ groups
usuari adm cdrom sudo dip plugdev lpadmin sambashare
```

#### getent passwd

Mostra **informació dels usuaris**. Pot mostrar tant usuaris locals com de domini \(LDAP\).

```text
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

#### getent group

Mostra **informació dels grups**. Pot mostrar tant grups locals com de domini \(LDAP\).

```text
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

> **ATENCIÓ**: aquests arxius no s'haurien d'editar mai manualment! Per fer qualsevol modificació s'han d'utilitzar les comandes corresponents.

#### /etc/passwd

Conté la informació dels usuaris del sistema \(nom, directori home, etc.\). Cada línia és un usuari i cada camp està separat per dos punts \(:\).

`usuari:x:1000:2000:usuari local,,,:/home/usuari:/bin/bash`

* **usuari** és el nom del compte d'usuari \(_login_\)
* Una **x** en el segon camp indica que la contrasenya es troba en l'arxiu /etc/shadow.
* El tercer camp \(**1000**\) és l'identificador d'usuari.
* El quart camp \(**2000**\) és l'identificador del grup principal.
* Nom complet de l'usuari i altres informacions.
* `/home/usuari` és el directori personal de l'usuari.
* `/bin/bash` és l'intèrpret de comandes per defecte.

Només el _**root**_ té permís d'escriptura. La resta d'usuaris i grups només el poden llegir.

#### /etc/shadow

Conté la les contrasenyes xifrades dels usuaris i altres informacions, com per exemple l'última data en què es va canviar la contrasenya.

Només l'usuari _**root**_ té permís d'escriptura. Només el grup _**shadow**_ té permís de lectura. La resta d'usuaris i grups no tenen cap permís.

#### /etc/group

Conté la informació dels grups. Cada camp està separat per `:`

`profes:x:2000:usuari,director`

* **profes** és el  nom del grup.
* Una **x** en el segon camp indica que la contrasenya es troba en l'arxiu /etc/gshadow.
* El tercer camp \(**2000**\) és l'identificador del grup.
* El quart camp conté els noms dels usuaris que tenen aquest grup com a grup secundari.

Només el _**root**_ té permís d'escriptura. La resta d'usuaris i grups només el poden llegir.

#### /etc/gshadow

Conté les contrasenyes encriptades dels grups.

Només l'usuari _**root**_ té permís d'escriptura. Només el grup _**shadow**_ té permís de lectura.

#### /etc/sudoers

Conté informació sobre els drets i privilegis dels usuaris.

La seva principal utilitat és afegir grups o usuaris que puguin actuar com a administradors \(que puguin utilitzar la comanda `sudo`\).

Només el _**root**_ pot llegir-lo. La resta d'usuaris i grups no tenen cap permís.

Per editar-lo cal utilitzar la comanda `visudo`:

`sudo visudo`

```text
# User privilege specification
root    ALL=(ALL:ALL) ALL

# Allow members of group sudo to execute any command
%sudo    ALL=(ALL:ALL) ALL
```

## Referències

* **Apunts SOX Pere Sánchez:** [Arxius de Linux relacionats amb els usuaris i grups locals](http://moodlecf.sapalomera.cat/apunts/smx/sox/index.html?cap=92&ref=2023)
* **Apunts SOX Pere Sánchez:** [Crear i eliminar usuaris locals](http://moodlecf.sapalomera.cat/apunts/smx/sox/index.html?cap=120&ref=2321)

