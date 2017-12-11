<!-- notoc -->

# Introducció als dominis en Linux

En Linux, el **protocol** que s'encarrega de crear, modificar i accedir a informació en un directori és **LDAP**.

**LDAP **són les sigles de **_lightweight directory access protocol_** o protocol d’accés lleuger a directoris.

El **LDAP** és un protocol obert.
* De fet, l'Active Directory de Windows també utilitza LDAP per gestionar la informació del domini.

En Linux, un dels programes que permet gestionar la informació d'un directori LDAP és **OpenLDAP**.

## Ús de LDAP

L’objectiu principal és permetre l’**autenticació** en xarxa.

És un sistema ideal per **centralitzar l’administració d’usuaris** en un únic lloc.

Es pot utilitzar de manera conjunta amb una gran quantitat d’**aplicacions que disposen de suport per a l’LDAP**, com:

* Sistemes d’autenticació per a pàgines web: alguns dels gestors de continguts permeten autenticació a través de LDAP.
* Sistemes de correu electrònic.
* Sistemes d’allotjament de pàgines web i FTP.

En general, el LDAP s’utilitza quan es vol accedir a una base de dades i cal autenticar-se des de **diferents plataformes** i des de múltiples ordinadors o aplicacions ubicats en una xarxa.

El servei de directori LDAP té una **arquitectura client-servidor**.
