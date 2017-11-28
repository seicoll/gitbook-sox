# Instal·lació de paquets i actualització del sistema

## Paquets de programari

> Un **paquet de programari** és un arxiu que conté una sèrie de fitxers que es distribueixen conjuntament i permeten la instal·lació d’un programa 

Hi ha diversos tipus de paquets: 
* Els **paquets binaris** són paquets construïts (o complilats) específicament per a uma distribució.
Els més comuns són:
  * Els **.rpm**, que els utilitzen **_Red Hat_**, **_Suse_** i derivats
  * Els **.deb**, que els utilitzen **_Debian_**, **_Ubuntu_** i derivats. 
  

* Els **paquets font** són senzillament paquets que inclouen codi font.
  * Es poden utilitzar qualsevol tipus de màquina si el codi es compilen correctament. 
  * Els trobem empaquetats i comprimits amb formats com .tar.gz o tar.bz2. 
  
## Repositoris
  
Els paquets els trobarem als repositoris. 

> **Repositori:** lloc centralitzat on s’emmagatzema i es manté informació digital, habitualment bases de dades o arxius informàtics. 

Els repositoris des d'on es poden descarregar, instal·lar i actualitzar paquets es troben definits a l'arxiu `/etc/apt/sources.list`

  * També en altres arxius dins de `/etc/apt/sources.list.d/`.
  
## Gestors de paquets

> Els **gestors de paquets** són aplicacions que permeten gestionar paquets. 

Faciliten les tasques més habituals relacionades amb la gestió de paquets (instal·lació, cerques, eliminacions, etc.)

* El programa principal utilitzat per gestionar aquest tipus de fitxers és el dpkg (abreviatura de Debian package), 

* Normalment s’utilitzen els frontals (front ends) com **apt** i **aptitude**. 

* També podeu utilitzar **interfícies gràfiques** com el Synaptic, el PackageKit o el Gdebi. 

* Els fitxers .deb dels paquets instal·lats els podem trobar en la carpeta /var/cache/apt/archives  