# Administració amb interfície web

## Introducció

Encara que un servidor no tingui interfície gràfica, existeixen molts **programes** que permeten **configurar un servidor de forma gràfica utilitzant una interfície web** (navegador d'Internet).

Només cal saber com instal·lar-los i fer, si cal, alguna configuració bàsica, i com accedir a través del navegador (en alguns casos es fa a través d'un port específic, en altres cal utilitzar https, per utilitzar alguns cal tenir instal·lat un servidor de pàgines web com Apache).

## Webmin

**Webmin** és un programa que permet **administrar un servidor** de forma remota a través d'una interfície web gràfica que fa més fàcil la seva configuració.

Entre altres coses, permet administrar els usuaris, els serveis, la instal·lació de paquets i l'actualització del sistema, els sistemes de fitxers locals i remots, RAID i LVM, les quotes de disc, les còpies de seguretat, programar tasques, compartició de carpetes, permisos, configuració de xarxa, tallafocs, monitoratge...

La millor forma d'**instal·lar**-ho és seguir les instruccions de [la seva web](http://www.webmin.com/deb.html) per afegir **_Webmin_** als repositoris. D'aquesta forma, s'actualitzarà automàticament quan s'actualitzi el sistema.

Per **accedir només cal obrir un navegador** en el client, utilitzar https i posar l'adreça del servidor i el **port 10000**:

`https://IP_servidor:10000`

Possiblement indicarà què s'està accedint a un lloc segur sense certificació reconeguda però s'ha de permetre l'accés.
Finalment demanarà un usuari administrador (que pugui fer sudo) i la seva contrasenya.

![](/assets/uf2-webmin.png)

[http://www.webmin.com/](http://www.webmin.com/)

## ntop

**Ntop** és un programa que serveix per **monitoritzar la xarxa**. Ens permet triar quines interfícies es vol monitoritzar i mostra en gràfics i en taules estadístiques tota la informació de la xarxa. Es pot filtrar en funció dels diversos protocols.

Es troba en els repositoris d'Ubuntu i per tant es pot instal·lar amb **apt**.
Demanarà quines interfícies es vol monitoritzar. S'han d'introduir separades per comes, per exemple: eth0,wlan0....
També demanarà una contrasenya per l'administrador.

Per **accedir a través d'un navegador web** cal escriure l'adreça del servidor i el **port 3000**:

`IP_servidor:3000`

L'usuari administrador de **ntop** per defecte es diu **admin**.

![](/assets/uf2-ntop.png)

## Nagios

**Nagios** és un sistema de **monitoratge d'equips i serveis de xarxa** que permet tenir un complet control de la disponibilitat de serveis, processos i recursos d'equips.

[https://www.nagios.org/](https://www.nagios.org/)

## Cacti

**Cacti** és una potent **eina de monitorització** que permet recollir tot tipus de dades de l'ordinador: ventiladors, temperatures, utilització de disc i de memòria... i representar-los a través d'una interfície web en forma gràfica amb diferents escales temporals.

[https://www.cacti.net/](https://www.cacti.net/)

## Documentació i recursos

* **Apunts SOX Pere Sánchez: Administració amb interfície web** [http://moodlecf.sapalomera.cat/apunts/smx/sox/?cap=1.5.15](http://moodlecf.sapalomera.cat/apunts/smx/sox/?cap=1.5.15)