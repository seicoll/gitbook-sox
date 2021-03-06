# Introducció als sistemes operatius en xarxa

## Introducció als Sistemes Operatius en Xarxa

Quan existeix un conjunt de dispositius informàtics connectats en xarxa \(ordinadors, impressores, ...\) i volem realitzar una gestió centralitzada d'aquests recursos, necessitem un equip amb un **Sistema Operatiu en Xarxa** instal·lat.

Els recursos de la xarxa \(impressores, documents\) es gestionaran sempre de forma centralitzada des d’aquest equip que s'anomena **Servidor**.

### Servidors

> Els **servidors** són els equips encarregats de proporcionar recursos als clients.

Disposen de programes específics \(**serveis**\) per oferir-los als clients:

* Servei de fitxers
* Servei d'impressió.
* Servei de correu.
* Servei de domini.
* Servei DNS.
* Servei DHCP.
* Etc.

### Clients

Els altres equips de la xarxa, actuen com a **clients** sol·licitant recursos al servidor.

> Els **clients** es connecten i validen al servidor per poder tenir accés als recursos de la xarxa. Solen tenir instal·lat un **Sistema Operatiu Monolloc** que ja venen preparats per poder-se connectar amb servidors.

Aquest model de treball es coneix com **arquitectura client/servidor**.

![](../../.gitbook/assets/clientservidor.png)

## Funcions dels Sistemes Operatius en Xarxa

Les funcions principals són:

* **Compartir recursos**.
  * Gestiona els recursos \(documents, impressores, etc.\) disponibles pels usuaris de la xarxa.
  * Optimitzar la utilització dels recursos.
* **Gestionar usuaris:** el mateix mateix usuari i contrasenya ha de servir per accedir als recursos de la xarxa.
  * Afegir, modificar i eliminar usuaris i grups.
  * Controlar quins usuaris o grups poden accedir als recursos de la xarxa.
* **Gestionar la xarxa.**
  * Controlar el comportament de la xarxa i detectar problemes.

## Inconvenients de l'arquitectura client/servidor

El principal inconvenient és la **dependència del servidor**.

Tota la xarxa està construïda al voltant del servidor i si aquest deixa de funcionar, afectarà a tota la infraestructura.

Aquest inconvenient es pot superar gràcies a sistemes com els **servidors redundants**.

## Sistemes Operatius més freqüents en un infraestructura client/servidor

En el costat del **servidor**, els sistemes més habituals són:

* **Microsoft Windows Server** \(versions 2003, 2008, 2012, 2016 i 2019\)
* **GNU/Linux Server** \(distribucions com Red Hat, Ubuntu Server, CentOS, etc\)
* **Apple OS X Server**

En el costat del **client**, també anomenats "_sistemes d'escriptori_", els sistemes més habituals són:

* **Microsoft Windows** \(Vista, 7, 8, 10, etc\).
* **GNU/Linux Desktop** \(Ubuntu Desktop, Fedora, Debian, etc\)
* **Apple OS X**

