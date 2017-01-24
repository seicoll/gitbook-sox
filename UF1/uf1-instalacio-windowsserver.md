# Instal·lació Windows Server 2012 R2

## Opcions d'instal·lació

* **Opció Instal·lació Servidor amb GUI _[Grafic User Interface]_**

  * S’instal·la la interfície d’usuari estàndard.
  
* **Opció Instal·lació Server Core. **

  * No s’instal·la la interfície d’usuari estàndard i el servidor s’administra amb la línia de comandes (Windows PowerShell) o bé remotament.
  * És l’opció predeterminada i recomanada per Micrososft. 
  * **Avantatges**: requereix menys espai de disc (uns 4GB menys) i s’augmenta la seguretat.

> **Es pot passar d’una opció a l’altra** en qualsevol moment.

> Podem instal·lar l’opció Servidor amb GUI al principi, utilitzar les eines gràfiques per configurar el servidor, i després, canviar a l’opció instal·lació Server Core.

## Minimal Server Interface

La possibilitat de passar d’una instal·lació a una altra, crea una instal·lació intermitja anomenda **Mininal Server Interface**.

Aquesta interface és el resultat d’iniciar amb una instal·lació** Servidor amb GUI** i després canviar a una instal·lació **Server Core**. 

Amb **Minimal Server Interface**, la Consola d’Administració Microsoft _[Microsoft Management Console (MMC)]_, l’Administrador del Servidor i una part del Tauler de Control, continuen instal·lats.

![Minimal Server Interface](/assets/WindowsServerMinimal.png)

## Tipus d’instal·lació

Una vegada escollit l’opció d’instal·lació, cal que decidiu si fareu una instal·lació des de zero o bé optareu per actualitzar el vostre sistema.

* **Instal·lació des de zero: **El sistema operatiu que hi hagi a l’equip se substituirà completament, de manera que les configuracions i les aplicacions es perdran.
* **Actualització:** el sistema operatiu s’instal·la i es fa una migració de les configuracions, els documents i les aplicacions.

> Si durant el procés d’instal·lació en falta alguna informació que necessitem per continuar. En el moment que es demana On es vol instal·lar Windows? es pot accedir a la línia de comandes prement Majúscules i F10.

## Post-instal·lació

Una vegada s’ha instal·lat el sistema operatiu caldrà proporcionar la informació següent a l’equip:
* Establir **zona horària**.
* Canviar el **nom de l’equip**.
* Configuració de la **Xarxa**. 
* **Actualització **del sistema operatiu (SO). 

## Post instal·lació. Funcionalitats i característiques

Instal·lar noves funcionalitats o noves característiques: 
* **Funcions de servidor o rols:** Conjunt de programes que fan una funció específica per diferents usuaris o altres equips d'una xarxa. Un servidor pot realitzar més d'una funció o rol.
  * Servidor de fitxers. 
  * Servidor d'aplicacions. 
  * Servidor de correu. 
  * Terminal server: permet l’administració remota del servidor des d’un altre equip de la xarxa. 
 * Control de domini. 
  * Servidor DNS: realitza la resolució de noms del domini. 
  * Servidor DHCP: realitza l’assignació direccions IP automàtiques.
  * etc.
* **Serveis de funcions** (serveis de rol): afegeixen més funcionalitat a un servidor. 
  * Alguns rols, com per exemple el de servidor de DNS, només tenen una funcionalitat, i per tant no tenen serveis de rol disponibles. 
  * Altres, com per exemple el de servidor d'escriptori remot, tenen diferents serveis de rol que es poden afegir en funció de les necessitats de l'empresa.
* **Característiques:** són programes per complementar o augmentar la funcionalitat del servidor però no tenen cap relació amb els rols que desenvolupa. 
  * Client TFTP
  * Client Telnet

> Un servidor es pot especialitzar en una única funció o en diverses.

## Administrador del Servidor _[Server Manager]_

* Permet instal·lar **rols i característiques** _[roles and features]_ del Servidor.

* En Server 2012 el **_Server Manager_** a part de gestionar el servidor local, permet gestionar múltiples servidors.

![Server Manager](/assets/ServerManager.png)
