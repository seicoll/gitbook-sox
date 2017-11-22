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

* Per defecte, quan es crea un usuari també **es crea un grup amb el seu mateix nom** i se li assigna com a grup principal.

* La **carpeta de l'usuari** no es crea fins que l'usuari es valida per primera vegada.
Per defecte, les carpetes d'usuari es creen dins de `/home` i se li copia el contingut de la carpeta `/etc/skel`.

Per crear un usuari:
`sudo adduser usuari`

Per crear un usuari i assignar-li el grup principal (el grup ha d'existir):
`sudo adduser usuari --ingroup grup`

##