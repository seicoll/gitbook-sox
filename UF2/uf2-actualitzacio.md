# Instal·lació de paquets i actualització del sistema

## Instal·lació de paquets

### Paquets de programari

> Un **paquet de programari** és un arxiu que conté una sèrie de fitxers que es distribueixen conjuntament i permeten la instal·lació d’un programa 

Hi ha diversos tipus de paquets: 
* Els **paquets binaris** són paquets construïts (o complilats) específicament per a uma distribució.
Els més comuns són:
  * Els **.rpm**, que els utilitzen **_Red Hat_**, **_Suse_** i derivats
  * Els **.deb**, que els utilitzen **_Debian_**, **_Ubuntu_** i derivats. 

* Els **paquets font** són senzillament paquets que inclouen codi font.
  * Es poden utilitzar qualsevol tipus de màquina si el codi es compilen correctament. 
  * Els trobem empaquetats i comprimits amb formats com .tar.gz o tar.bz2. 
  
### Gestors de paquets

> Els **gestors de paquets** són aplicacions que permeten gestionar paquets. 

Faciliten les tasques més habituals relacionades amb la gestió de paquets (instal·lació, cerques, eliminacions, etc.)

* El programa principal utilitzat per gestionar aquest tipus de fitxers és el **_dpkg_** (abreviatura de Debian package), 

* Normalment s'utilitzen els frontals (front ends) com **apt** i **aptitude**. 

### Repositoris
  
Els paquets els trobarem als **repositoris**. 

> **Repositori:** lloc centralitzat on s’emmagatzema i es manté informació digital, habitualment bases de dades o arxius informàtics. 

Els repositoris des d'on es poden descarregar, instal·lar i actualitzar paquets es troben definits a l'arxiu `/etc/apt/sources.list`

  * També en altres arxius dins de `/etc/apt/sources.list.d/`.
  
### Actualitzar repositoris

Abans d'actualitzar el sistema o instal·lar paquets és recomanable **actualitzar els repositoris** per tal que el sistema sàpiga si ha hagut canvis (nous paquets, actualitzacions, canvis de dependències...).

* Per **actualitzar els repositoris**:

  `sudo apt-get update` 

  o bé

  `sudo apt update` 

### Gestió de paquets

* **Per veure els paquets instal·lats:**

  `dpkg -l`

* **Per instal·lar paquets**:

  `sudo apt install <nom_paquet>`

* **Per desinstal·lar paquets:**

  `sudo apt remove <nom_paquet>` 

* Per **desinstal·lar** paquets i eliminar els fitxers de configuració associats al paquet desinstal·lat:

  `sudo apt purge <nom_paquet>`

* Per **desinstal·lar paquets** del sistema que ja no s’utilitzen: 

  `sudo apt autoremove`

* Per **esborrar els paquets d'instal·lació** i guanyar espai en el disc dur: 

  `sudo apt autoclean`
  

### Afegir repositoris externs

> Els repositoris externs es diuen **PPA** (**_Personal Package Archives_**).

Podeu trobar diferents PPA per Internet.

**Exemple d'instal·lació de VirtualBox:**

1. Per **afegir un PPA** dins de l'arxiu de repositoris es pot:

  * **Editar l'arxiu** `/etc/apt/sources.list` i afegir una línia com la següent:

   `deb http://download.virtualbox.org/virtualbox/debian trusty contrib`

  * O bé amb la **comanda** `apt-add-repository`:

  `sudo apt-add-repository "deb http://download.virtualbox.org/virtualbox/debian trusty contrib"`

2. Abans de poder instal·lar el programa, normalment, cal fer alguna operació més, com ara **descarregar i instal·lar una clau de seguretat**:

  `wget -q https://www.virtualbox.org/download/oracle_vbox.asc -O- | sudo apt-key add -`

3. La **instal·lació** (i desinstal·lació) d'aquests paquets es fa de la forma habitual:

  `sudo apt update`

  `sudo apt install virtualbox-5.0`

4. Si es vol **eliminar un repositori afegit** amb aquests mètodes, es pot editar l'arxiu `/etc/apt/sources.list` i esborrar la línia corresponent.
 
## Actualització del sistema operatiu
  
* Per **actualitzar tots els paquets** a les últimes versions que hi ha en els repositoris i sense canviar de versió del sistema:

  `sudo apt update` 
  
  `sudo apt upgrade`
  
* Per **actualitzar el sistema a una versió superior**.

  `sudo apt update`

  `sudo apt dist-upgrade` 
  
  
## Instal·lació de paquets i actualitzacions amb entorn gràfic

* **Centro de software de Ubuntu:** serveix per instal·lar i desinstal·lar programes i paquets que hi ha en els repositoris d'Ubuntu.

* **Software i actualizaciones:** serveix per configurar les actualitzacions del sistema i del programari (triar els repositoris, la periodicitat...). També mostra i permet seleccionar possibles controladors de hardware, tant lliures com privatius (per exemple, els de la targeta gràfica).

* **Actualización de software:** permet comprovar manualment si hi ha actualitzacions i triar quins paquets es volen actualitzar.